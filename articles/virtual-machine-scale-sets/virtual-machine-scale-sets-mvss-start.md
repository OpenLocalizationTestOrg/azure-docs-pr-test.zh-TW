---
title: "aaaLearn 有關虛擬機器擴展集範本 |Microsoft 文件"
description: "了解 toocreate 最小的可行小數位數設定的虛擬機器擴展集的範本"
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
ms.openlocfilehash: b7a1cf6c03b22585e16db9c071d45795c8ae75df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="learn-about-virtual-machine-scale-set-templates"></a><span data-ttu-id="6c1f8-103">了解虛擬機器擴展集範本</span><span class="sxs-lookup"><span data-stu-id="6c1f8-103">Learn about virtual machine scale set templates</span></span>
<span data-ttu-id="6c1f8-104">[Azure 資源管理員範本](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment)是很好的方法 toodeploy 相關資源的群組。</span><span class="sxs-lookup"><span data-stu-id="6c1f8-104">[Azure Resource Manager templates](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) are a great way toodeploy groups of related resources.</span></span> <span data-ttu-id="6c1f8-105">此教學課程 數列會顯示最小的可行刻度 toocreate 設定範本以及如何 toomodify 這個範本 toosuit 各種案例。</span><span class="sxs-lookup"><span data-stu-id="6c1f8-105">This tutorial series shows how toocreate a minimum viable scale set template and how toomodify this template toosuit various scenarios.</span></span> <span data-ttu-id="6c1f8-106">所有範例皆來自這個 [GitHub 存放庫](https://github.com/gatneil/mvss)。</span><span class="sxs-lookup"><span data-stu-id="6c1f8-106">All examples come from this [GitHub repository](https://github.com/gatneil/mvss).</span></span> 

<span data-ttu-id="6c1f8-107">此範本是簡單的預定的 toobe。</span><span class="sxs-lookup"><span data-stu-id="6c1f8-107">This template is intended toobe simple.</span></span> <span data-ttu-id="6c1f8-108">如需更完整的範例，小數位數的設定範本，請參閱 hello [Azure 快速入門範本 GitHub 儲存機制](https://github.com/Azure/azure-quickstart-templates)和搜尋資料夾包含 hello 字串`vmss`。</span><span class="sxs-lookup"><span data-stu-id="6c1f8-108">For more complete examples of scale set templates, see hello [Azure Quickstart Templates GitHub repository](https://github.com/Azure/azure-quickstart-templates) and search for folders that contain hello string `vmss`.</span></span>

<span data-ttu-id="6c1f8-109">如果您已經熟悉如何建立範本，您可以如何略過 toohello 「 後續步驟 」 一節 toosee toomodify 此範本。</span><span class="sxs-lookup"><span data-stu-id="6c1f8-109">If you are already familiar with creating templates, you can skip toohello "Next steps" section toosee how toomodify this template.</span></span>

## <a name="review-hello-template"></a><span data-ttu-id="6c1f8-110">檢閱 hello 範本</span><span class="sxs-lookup"><span data-stu-id="6c1f8-110">Review hello template</span></span>

<span data-ttu-id="6c1f8-111">使用 GitHub tooreview 我們最小的可行小數位數設定範本， [azuredeploy.json](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json)。</span><span class="sxs-lookup"><span data-stu-id="6c1f8-111">Use GitHub tooreview our minimum viable scale set template, [azuredeploy.json](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json).</span></span>

<span data-ttu-id="6c1f8-112">在本教學課程中，我們會檢查 hello 差異比對 (`git diff master minimum-viable-scale-set`) toocreate hello 最小可行規模調整集合範本逐一。</span><span class="sxs-lookup"><span data-stu-id="6c1f8-112">In this tutorial, we examine hello diff (`git diff master minimum-viable-scale-set`) toocreate hello minimum viable scale set template piece by piece.</span></span>

## <a name="define-schema-and-contentversion"></a><span data-ttu-id="6c1f8-113">定義 $schema 和 contentVersion</span><span class="sxs-lookup"><span data-stu-id="6c1f8-113">Define $schema and contentVersion</span></span>
<span data-ttu-id="6c1f8-114">首先，我們會定義`$schema`和`contentVersion`hello 範本中。</span><span class="sxs-lookup"><span data-stu-id="6c1f8-114">First, we define `$schema` and `contentVersion` in hello template.</span></span> <span data-ttu-id="6c1f8-115">hello`$schema`元素都會定義 hello hello 範本語言版本和使用 Visual Studio 語法反白顯示和類似的驗證功能。</span><span class="sxs-lookup"><span data-stu-id="6c1f8-115">hello `$schema` element defines hello version of hello template language and is used for Visual Studio syntax highlighting and similar validation features.</span></span> <span data-ttu-id="6c1f8-116">hello`contentVersion`項目不由 Azure。</span><span class="sxs-lookup"><span data-stu-id="6c1f8-116">hello `contentVersion` element is not used by Azure.</span></span> <span data-ttu-id="6c1f8-117">相反地，它可協助您追蹤 hello 範本版本。</span><span class="sxs-lookup"><span data-stu-id="6c1f8-117">Instead, it helps you keep track of hello template version.</span></span>

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json",
  "contentVersion": "1.0.0.0",
```
## <a name="define-parameters"></a><span data-ttu-id="6c1f8-118">定義參數</span><span class="sxs-lookup"><span data-stu-id="6c1f8-118">Define parameters</span></span>
<span data-ttu-id="6c1f8-119">接著，我們會定義兩個參數：`adminUsername` 和 `adminPassword`。</span><span class="sxs-lookup"><span data-stu-id="6c1f8-119">Next, we define two parameters, `adminUsername` and `adminPassword`.</span></span> <span data-ttu-id="6c1f8-120">參數是您在部署的 hello 階段指定的值。</span><span class="sxs-lookup"><span data-stu-id="6c1f8-120">Parameters are values you specify at hello time of deployment.</span></span> <span data-ttu-id="6c1f8-121">hello`adminUsername`參數只是`string`型別，但是因為`adminPassword`是密碼，我們提供它的類型`securestring`。</span><span class="sxs-lookup"><span data-stu-id="6c1f8-121">hello `adminUsername` parameter is simply a `string` type, but because `adminPassword` is a secret, we give it type `securestring`.</span></span> <span data-ttu-id="6c1f8-122">更新版本中，這些參數會傳遞至 hello 小數位數設定的組態。</span><span class="sxs-lookup"><span data-stu-id="6c1f8-122">Later, these parameters are passed into hello scale set configuration.</span></span>

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
## <a name="define-variables"></a><span data-ttu-id="6c1f8-123">定義變數</span><span class="sxs-lookup"><span data-stu-id="6c1f8-123">Define variables</span></span>
<span data-ttu-id="6c1f8-124">資源管理員範本可讓您定義變數 toobe 稍後在 hello 範本中使用。</span><span class="sxs-lookup"><span data-stu-id="6c1f8-124">Resource Manager templates also let you define variables toobe used later in hello template.</span></span> <span data-ttu-id="6c1f8-125">我們的範例不使用任何變數，因此我們已經空白 hello JSON 物件。</span><span class="sxs-lookup"><span data-stu-id="6c1f8-125">Our example doesn't use any variables, so we've left hello JSON object empty.</span></span>

```json
  "variables": {},
```

## <a name="define-resources"></a><span data-ttu-id="6c1f8-126">定義資源</span><span class="sxs-lookup"><span data-stu-id="6c1f8-126">Define resources</span></span>
<span data-ttu-id="6c1f8-127">接下來是 hello hello 範本的資源 > 一節。</span><span class="sxs-lookup"><span data-stu-id="6c1f8-127">Next is hello resources section of hello template.</span></span> <span data-ttu-id="6c1f8-128">在這裡，您會定義您實際想 toodeploy。</span><span class="sxs-lookup"><span data-stu-id="6c1f8-128">Here, you define what you actually want toodeploy.</span></span> <span data-ttu-id="6c1f8-129">與 `parameters` 和 `variables` (這些是 JSON 物件) 不同，`resources` 是一個 JSON 物件的 JSON 清單。</span><span class="sxs-lookup"><span data-stu-id="6c1f8-129">Unlike `parameters` and `variables` (which are JSON objects), `resources` is a JSON list of JSON objects.</span></span>

```json
   "resources": [
```

<span data-ttu-id="6c1f8-130">所有資源都必須要有 `type`、`name`、`apiVersion` 及 `location` 屬性。</span><span class="sxs-lookup"><span data-stu-id="6c1f8-130">All resources require `type`, `name`, `apiVersion`, and `location` properties.</span></span> <span data-ttu-id="6c1f8-131">這個範例的第一個資源具有類型 `Microsft.Network/virtualNetwork`、名稱`myVnet`，和 apiVersion `2016-03-30`。</span><span class="sxs-lookup"><span data-stu-id="6c1f8-131">This example's first resource has type `Microsft.Network/virtualNetwork`, name `myVnet`, and apiVersion `2016-03-30`.</span></span> <span data-ttu-id="6c1f8-132">(toofind hello 最新 API 版本的資源類型，請參閱 hello [Azure REST API 文件](https://docs.microsoft.com/rest/api/)。)</span><span class="sxs-lookup"><span data-stu-id="6c1f8-132">(toofind hello latest API version for a resource type, see hello [Azure REST API documentation](https://docs.microsoft.com/rest/api/).)</span></span>

```json
     {
       "type": "Microsoft.Network/virtualNetworks",
       "name": "myVnet",
       "apiVersion": "2016-12-01",
```

## <a name="specify-location"></a><span data-ttu-id="6c1f8-133">指定位置</span><span class="sxs-lookup"><span data-stu-id="6c1f8-133">Specify location</span></span>
<span data-ttu-id="6c1f8-134">toospecify hello 位置 hello 虛擬網路，我們使用[資源管理員範本函式](../azure-resource-manager/resource-group-template-functions.md)。</span><span class="sxs-lookup"><span data-stu-id="6c1f8-134">toospecify hello location for hello virtual network, we use a [Resource Manager template function](../azure-resource-manager/resource-group-template-functions.md).</span></span> <span data-ttu-id="6c1f8-135">此函式必須括在引號和方括號內，如下所示︰`"[<template-function>]"`。</span><span class="sxs-lookup"><span data-stu-id="6c1f8-135">This function must be enclosed in quotes and square brackets like this: `"[<template-function>]"`.</span></span> <span data-ttu-id="6c1f8-136">在此情況下，我們使用 hello`resourceGroup`函式。</span><span class="sxs-lookup"><span data-stu-id="6c1f8-136">In this case, we use hello `resourceGroup` function.</span></span> <span data-ttu-id="6c1f8-137">它會接受任何引數，並傳回 JSON 物件要部署此部署的 hello 資源群組的相關中繼資料。</span><span class="sxs-lookup"><span data-stu-id="6c1f8-137">It takes in no arguments and returns a JSON object with metadata about hello resource group this deployment is being deployed to.</span></span> <span data-ttu-id="6c1f8-138">hello 資源群組部署的 hello 次由 hello 使用者設定。</span><span class="sxs-lookup"><span data-stu-id="6c1f8-138">hello resource group is set by hello user at hello time of deployment.</span></span> <span data-ttu-id="6c1f8-139">然後，我們使用此 JSON 物件中的索引`.location`tooget hello hello JSON 物件的位置。</span><span class="sxs-lookup"><span data-stu-id="6c1f8-139">We then index into this JSON object with `.location` tooget hello location from hello JSON object.</span></span>

```json
       "location": "[resourceGroup().location]",
```

## <a name="specify-virtual-network-properties"></a><span data-ttu-id="6c1f8-140">指定虛擬網路屬性</span><span class="sxs-lookup"><span data-stu-id="6c1f8-140">Specify virtual network properties</span></span>
<span data-ttu-id="6c1f8-141">每個資源管理員資源都有它自己`properties`設定特定 toohello 資源 > 一節。</span><span class="sxs-lookup"><span data-stu-id="6c1f8-141">Each Resource Manager resource has its own `properties` section for configurations specific toohello resource.</span></span> <span data-ttu-id="6c1f8-142">我們在此情況下，指定該 hello 虛擬網路應該有一個子網路使用私人 IP 位址範圍 hello `10.0.0.0/16`。</span><span class="sxs-lookup"><span data-stu-id="6c1f8-142">In this case, we specify that hello virtual network should have one subnet using hello private IP address range `10.0.0.0/16`.</span></span> <span data-ttu-id="6c1f8-143">擴展集一律是包含在一個子網路內。</span><span class="sxs-lookup"><span data-stu-id="6c1f8-143">A scale set is always contained within one subnet.</span></span> <span data-ttu-id="6c1f8-144">它不能跨子網路。</span><span class="sxs-lookup"><span data-stu-id="6c1f8-144">It cannot span subnets.</span></span>

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

## <a name="add-dependson-list"></a><span data-ttu-id="6c1f8-145">新增 dependsOn 清單</span><span class="sxs-lookup"><span data-stu-id="6c1f8-145">Add dependsOn list</span></span>
<span data-ttu-id="6c1f8-146">此外 toohello 需要`type`， `name`， `apiVersion`，和`location`屬性，每個資源可以有選擇性`dependsOn`的字串清單。</span><span class="sxs-lookup"><span data-stu-id="6c1f8-146">In addition toohello required `type`, `name`, `apiVersion`, and `location` properties, each resource can have an optional `dependsOn` list of strings.</span></span> <span data-ttu-id="6c1f8-147">這份清單會指定此部署中的哪些其他資源必須在部署此資源之前完成。</span><span class="sxs-lookup"><span data-stu-id="6c1f8-147">This list specifies which other resources from this deployment must finish before deploying this resource.</span></span>

<span data-ttu-id="6c1f8-148">在此情況下，在 hello 清單中，從上一個範例的 hello hello 虛擬網路沒有只有一個項目。</span><span class="sxs-lookup"><span data-stu-id="6c1f8-148">In this case, there is only one element in hello list, hello virtual network from hello previous example.</span></span> <span data-ttu-id="6c1f8-149">因為 hello 小數位數組需要 hello 網路 tooexist 建立任何 Vm 之前，我們會指定此相依性。</span><span class="sxs-lookup"><span data-stu-id="6c1f8-149">We specify this dependency because hello scale set needs hello network tooexist before creating any VMs.</span></span> <span data-ttu-id="6c1f8-150">如此一來，hello 規模集可以讓這些 Vm 私用 IP 位址從 hello 先前 hello 網路內容中指定的 IP 位址範圍。</span><span class="sxs-lookup"><span data-stu-id="6c1f8-150">This way, hello scale set can give these VMs private IP addresses from hello IP address range previously specified in hello network properties.</span></span> <span data-ttu-id="6c1f8-151">每個字串 hello dependsOn 清單中的 hello 格式是`<type>/<name>`。</span><span class="sxs-lookup"><span data-stu-id="6c1f8-151">hello format of each string in hello dependsOn list is `<type>/<name>`.</span></span> <span data-ttu-id="6c1f8-152">使用 hello 相同`type`和`name`先前 hello 虛擬網路的資源定義中使用。</span><span class="sxs-lookup"><span data-stu-id="6c1f8-152">Use hello same `type` and `name` used previously in hello virtual network resource definition.</span></span>

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
## <a name="specify-scale-set-properties"></a><span data-ttu-id="6c1f8-153">指定擴展集屬性</span><span class="sxs-lookup"><span data-stu-id="6c1f8-153">Specify scale set properties</span></span>
<span data-ttu-id="6c1f8-154">標尺集具有自訂 hello Vm hello 規模集中的許多屬性。</span><span class="sxs-lookup"><span data-stu-id="6c1f8-154">Scale sets have many properties for customizing hello VMs in hello scale set.</span></span> <span data-ttu-id="6c1f8-155">如需這些屬性的完整清單，請參閱 hello[規模調整集合 REST API 文件](https://docs.microsoft.com/en-us/rest/api/virtualmachinescalesets/create-or-update-a-set)。</span><span class="sxs-lookup"><span data-stu-id="6c1f8-155">For a full list of these properties, see hello [scale set REST API documentation](https://docs.microsoft.com/en-us/rest/api/virtualmachinescalesets/create-or-update-a-set).</span></span> <span data-ttu-id="6c1f8-156">針對本教學課程，我們只會設定一些常用的屬性。</span><span class="sxs-lookup"><span data-stu-id="6c1f8-156">For this tutorial, we will set only a few commonly used properties.</span></span>
### <a name="supply-vm-size-and-capacity"></a><span data-ttu-id="6c1f8-157">提供 VM 大小和容量</span><span class="sxs-lookup"><span data-stu-id="6c1f8-157">Supply VM size and capacity</span></span>
<span data-ttu-id="6c1f8-158">hello 小數位數設定需求 tooknow 何種大小的 VM toocreate （「 sku 名稱 」） 及多少這類 Vm toocreate （「 sku 容量 」）。</span><span class="sxs-lookup"><span data-stu-id="6c1f8-158">hello scale set needs tooknow what size of VM toocreate ("sku name") and how many such VMs toocreate ("sku capacity").</span></span> <span data-ttu-id="6c1f8-159">toosee 的 VM 大小可供使用，請參閱 hello [VM 大小的文件](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-windows-sizes)。</span><span class="sxs-lookup"><span data-stu-id="6c1f8-159">toosee which VM sizes are available, see hello [VM Sizes documentation](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-windows-sizes).</span></span>

```json
       "sku": {
         "name": "Standard_A1",
         "capacity": 2
       },
```

### <a name="choose-type-of-updates"></a><span data-ttu-id="6c1f8-160">選擇更新類型</span><span class="sxs-lookup"><span data-stu-id="6c1f8-160">Choose type of updates</span></span>
<span data-ttu-id="6c1f8-161">hello 規模集也必須的 tooknow toohandle hello 規模調整集合的更新方式。</span><span class="sxs-lookup"><span data-stu-id="6c1f8-161">hello scale set also needs tooknow how toohandle updates on hello scale set.</span></span> <span data-ttu-id="6c1f8-162">目前有兩個選項：`Manual` 和 `Automatic`。</span><span class="sxs-lookup"><span data-stu-id="6c1f8-162">Currently, there are two options, `Manual` and `Automatic`.</span></span> <span data-ttu-id="6c1f8-163">Hello hello 兩個差異的詳細資訊，請參閱 hello 文件，在[如何 tooupgrade 規模調整集合](./virtual-machine-scale-sets-upgrade-scale-set.md)。</span><span class="sxs-lookup"><span data-stu-id="6c1f8-163">For more information on hello differences between hello two, see hello documentation on [how tooupgrade a scale set](./virtual-machine-scale-sets-upgrade-scale-set.md).</span></span>

```json
       "properties": {
         "upgradePolicy": {
           "mode": "Manual"
         },
```

### <a name="choose-vm-operating-system"></a><span data-ttu-id="6c1f8-164">選擇 VM 作業系統</span><span class="sxs-lookup"><span data-stu-id="6c1f8-164">Choose VM operating system</span></span>
<span data-ttu-id="6c1f8-165">hello 擴展集需求 tooknow 哪些作業系統 tooput hello Vm 上。</span><span class="sxs-lookup"><span data-stu-id="6c1f8-165">hello scale set needs tooknow what operating system tooput on hello VMs.</span></span> <span data-ttu-id="6c1f8-166">在這裡，我們建立具有完整修補 Ubuntu 16.04 LTS 影像 hello Vm。</span><span class="sxs-lookup"><span data-stu-id="6c1f8-166">Here, we create hello VMs with a fully patched Ubuntu 16.04-LTS image.</span></span>

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

### <a name="specify-computernameprefix"></a><span data-ttu-id="6c1f8-167">指定 computerNamePrefix</span><span class="sxs-lookup"><span data-stu-id="6c1f8-167">Specify computerNamePrefix</span></span>
<span data-ttu-id="6c1f8-168">hello 規模調整集合部署了多個 Vm。</span><span class="sxs-lookup"><span data-stu-id="6c1f8-168">hello scale set deploys multiple VMs.</span></span> <span data-ttu-id="6c1f8-169">我們會指定 `computerNamePrefix`，而不是指定每個 VM 名稱。</span><span class="sxs-lookup"><span data-stu-id="6c1f8-169">Instead of specifying each VM name, we specify `computerNamePrefix`.</span></span> <span data-ttu-id="6c1f8-170">hello 規模集附加索引 toohello 前置詞為每個 VM，所以 VM 名稱有 hello 形式`<computerNamePrefix>_<auto-generated-index>`。</span><span class="sxs-lookup"><span data-stu-id="6c1f8-170">hello scale set appends an index toohello prefix for each VM, so VM names have hello form `<computerNamePrefix>_<auto-generated-index>`.</span></span>

<span data-ttu-id="6c1f8-171">下列程式碼片段的 hello，在中，我們會使用從前面 tooset hello 系統管理員使用者名稱和密碼的 hello 參數 hello 規模集中的所有 vm。</span><span class="sxs-lookup"><span data-stu-id="6c1f8-171">In hello following snippet, we use hello parameters from before tooset hello administrator username and password for all VMs in hello scale set.</span></span> <span data-ttu-id="6c1f8-172">執行此作業，以 hello`parameters`樣板函式。</span><span class="sxs-lookup"><span data-stu-id="6c1f8-172">We do this with hello `parameters` template function.</span></span> <span data-ttu-id="6c1f8-173">這個函數接受字串，指定哪些參數 toorefer tooand 輸出 hello 該參數的值。</span><span class="sxs-lookup"><span data-stu-id="6c1f8-173">This function takes in a string that specifies which parameter toorefer tooand outputs hello value for that parameter.</span></span>

```json
           "osProfile": {
             "computerNamePrefix": "vm",
             "adminUsername": "[parameters('adminUsername')]",
             "adminPassword": "[parameters('adminPassword')]"
           },
```

### <a name="specify-vm-network-configuration"></a><span data-ttu-id="6c1f8-174">指定 VM 網路組態</span><span class="sxs-lookup"><span data-stu-id="6c1f8-174">Specify VM network configuration</span></span>
<span data-ttu-id="6c1f8-175">最後，我們需要 hello 規模集中的 hello Vm toospecify hello 網路組態。</span><span class="sxs-lookup"><span data-stu-id="6c1f8-175">Finally, we need toospecify hello network configuration for hello VMs in hello scale set.</span></span> <span data-ttu-id="6c1f8-176">在此情況下，我們只需要 toospecify hello 識別碼 hello 稍早建立的子網路。</span><span class="sxs-lookup"><span data-stu-id="6c1f8-176">In this case, we only need toospecify hello ID of hello subnet created earlier.</span></span> <span data-ttu-id="6c1f8-177">這會告訴 hello 標尺 tooput hello 網路介面中設定此子網路。</span><span class="sxs-lookup"><span data-stu-id="6c1f8-177">This tells hello scale set tooput hello network interfaces in this subnet.</span></span>

<span data-ttu-id="6c1f8-178">您可以取得 hello 識別碼 hello 包含使用 hello hello 子網路的虛擬網路的`resourceId`樣板函式。</span><span class="sxs-lookup"><span data-stu-id="6c1f8-178">You can get hello ID of hello virtual network containing hello subnet by using hello `resourceId` template function.</span></span> <span data-ttu-id="6c1f8-179">此函式會接受 hello 型別和資源的名稱，並傳回 hello 該資源的完整的識別碼。</span><span class="sxs-lookup"><span data-stu-id="6c1f8-179">This function takes in hello type and name of a resource and returns hello fully qualified identifier of that resource.</span></span> <span data-ttu-id="6c1f8-180">此識別碼具有 hello 格式：`/subscriptions/<subscriptionId>/resourceGroups/<resourceGroupName>/<resourceProviderNamespace>/<resourceType>/<resourceName>`</span><span class="sxs-lookup"><span data-stu-id="6c1f8-180">This ID has hello form: `/subscriptions/<subscriptionId>/resourceGroups/<resourceGroupName>/<resourceProviderNamespace>/<resourceType>/<resourceName>`</span></span>

<span data-ttu-id="6c1f8-181">不過，hello 識別碼 hello 虛擬網路是不夠的。</span><span class="sxs-lookup"><span data-stu-id="6c1f8-181">However, hello identifier of hello virtual network is not enough.</span></span> <span data-ttu-id="6c1f8-182">您必須指定 hello 擴展集 Vm 應該位於 hello 特定子網路。</span><span class="sxs-lookup"><span data-stu-id="6c1f8-182">You must specify hello specific subnet that hello scale set VMs should be in.</span></span> <span data-ttu-id="6c1f8-183">toodo，串連`/subnets/mySubnet`toohello 識別碼 hello 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="6c1f8-183">toodo this, concatenate `/subnets/mySubnet` toohello ID of hello virtual network.</span></span> <span data-ttu-id="6c1f8-184">hello 結果會是完整的 hello hello 子網路識別碼。</span><span class="sxs-lookup"><span data-stu-id="6c1f8-184">hello result is hello fully qualified ID of hello subnet.</span></span> <span data-ttu-id="6c1f8-185">執行以 hello 這個串連`concat`函式，以接受一系列字串並傳回它們的串連。</span><span class="sxs-lookup"><span data-stu-id="6c1f8-185">Do this concatenation with hello `concat` function, which takes in a series of strings and returns their concatenation.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="6c1f8-186">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6c1f8-186">Next steps</span></span>

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
