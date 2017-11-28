---
title: "Azure Service Fabric 叢集中的 aaaManage 憑證 |Microsoft 文件"
description: "描述如何 tooadd 新的憑證、 變換憑證，以及移除憑證 tooor 從 Service Fabric 叢集。"
services: service-fabric
documentationcenter: .net
author: ChackDan
manager: timlt
editor: 
ms.assetid: 91adc3d3-a4ca-46cf-ac5f-368fb6458d74
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/09/2017
ms.author: chackdan
ms.openlocfilehash: 8e57bd95dbb800ecc04cf6988047e3abdc2fe56a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="add-or-remove-certificates-for-a-service-fabric-cluster-in-azure"></a><span data-ttu-id="1a52c-103">新增或移除 Azure 中 Service Fabric 叢集的憑證</span><span class="sxs-lookup"><span data-stu-id="1a52c-103">Add or remove certificates for a Service Fabric cluster in Azure</span></span>
<span data-ttu-id="1a52c-104">建議您先熟悉 Service Fabric 如何使用 X.509 憑證，並熟悉 hello[叢集安全性案例](service-fabric-cluster-security.md)。</span><span class="sxs-lookup"><span data-stu-id="1a52c-104">It is recommended that you familiarize yourself with how Service Fabric uses X.509 certificates and be familiar with hello [Cluster security scenarios](service-fabric-cluster-security.md).</span></span> <span data-ttu-id="1a52c-105">您必須瞭解什麼是叢集憑證及其用途，方可繼續進行後續作業。</span><span class="sxs-lookup"><span data-stu-id="1a52c-105">You must understand what a cluster certificate is and what is used for, before you proceed further.</span></span>

<span data-ttu-id="1a52c-106">服務網狀架構可讓您指定兩個叢集憑證中，主要和次要複本，當您設定叢集建立期間，加法 tooclient 憑證中的憑證安全性。</span><span class="sxs-lookup"><span data-stu-id="1a52c-106">Service fabric lets you specify two cluster certificates, a primary and a secondary, when you configure certificate security during cluster creation, in addition tooclient certificates.</span></span> <span data-ttu-id="1a52c-107">請參閱太[建立透過入口網站的 azure 叢集](service-fabric-cluster-creation-via-portal.md)或[建立 azure 的叢集透過 Azure Resource Manager](service-fabric-cluster-creation-via-arm.md)它們設定在詳細資料建立時間。</span><span class="sxs-lookup"><span data-stu-id="1a52c-107">Refer too[creating an azure cluster via portal](service-fabric-cluster-creation-via-portal.md) or [creating an azure cluster via Azure Resource Manager](service-fabric-cluster-creation-via-arm.md) for details on setting them up at create time.</span></span> <span data-ttu-id="1a52c-108">如果您指定只有一個叢集憑證在建立時，然後作為 hello 主要憑證。</span><span class="sxs-lookup"><span data-stu-id="1a52c-108">If you specify only one cluster certificate at create time, then that is used as hello primary certificate.</span></span> <span data-ttu-id="1a52c-109">在叢集建立完成後，您可新增憑證做為次要憑證。</span><span class="sxs-lookup"><span data-stu-id="1a52c-109">After cluster creation, you can add a new certificate as a secondary.</span></span>

> [!NOTE]
> <span data-ttu-id="1a52c-110">安全的叢集，您永遠必須至少一個有效的 （未撤銷和未到期） 叢集 （主要或次要） 部署憑證 （如果沒有，hello 叢集會停止運作）。</span><span class="sxs-lookup"><span data-stu-id="1a52c-110">For a secure cluster, you will always need at least one valid (not revoked and not expired) cluster certificate (primary or secondary) deployed (if not, hello cluster stops functioning).</span></span> <span data-ttu-id="1a52c-111">90 天的所有有效憑證到達到期日之前 hello 系統會產生警告追蹤以及 hello 節點上的警告健全狀況事件。</span><span class="sxs-lookup"><span data-stu-id="1a52c-111">90 days before all valid certificates reach expiration, hello system generates a warning trace and also a warning health event on hello node.</span></span> <span data-ttu-id="1a52c-112">目前並無 Service Fabric 針對此主題送出的電子郵件或其他任何通知。</span><span class="sxs-lookup"><span data-stu-id="1a52c-112">There is currently no email or any other notification that service fabric sends out on this topic.</span></span> 
> 
> 

## <a name="add-a-secondary-cluster-certificate-using-hello-portal"></a><span data-ttu-id="1a52c-113">新增次要叢集憑證使用 hello 入口網站</span><span class="sxs-lookup"><span data-stu-id="1a52c-113">Add a secondary cluster certificate using hello portal</span></span>

<span data-ttu-id="1a52c-114">無法透過 hello Azure 入口網站中加入次要叢集憑證。</span><span class="sxs-lookup"><span data-stu-id="1a52c-114">Secondary cluster certificate cannot be added through hello Azure portal.</span></span> <span data-ttu-id="1a52c-115">您有 toouse Azure powershell 的。</span><span class="sxs-lookup"><span data-stu-id="1a52c-115">You have toouse Azure powershell for that.</span></span> <span data-ttu-id="1a52c-116">在本文件稍後所述 hello 程序。</span><span class="sxs-lookup"><span data-stu-id="1a52c-116">hello process is outlined later in this document.</span></span>

## <a name="swap-hello-cluster-certificates-using-hello-portal"></a><span data-ttu-id="1a52c-117">交換 hello 叢集憑證使用 hello 入口網站</span><span class="sxs-lookup"><span data-stu-id="1a52c-117">Swap hello cluster certificates using hello portal</span></span>

<span data-ttu-id="1a52c-118">您已成功部署次要叢集憑證中，如果您想 tooswap hello 主要和次要之後，瀏覽 toohello 安全性刀鋒視窗中，然後選取 hello '交換主要與' 選項從 hello 內容功能表 tooswap hello 次要憑證與hello 主要憑證。</span><span class="sxs-lookup"><span data-stu-id="1a52c-118">After you have successfully deployed a secondary cluster certificate, if you want tooswap hello primary and secondary, then navigate toohello Security blade, and select hello 'Swap with primary' option from hello context menu tooswap hello secondary cert with hello primary cert.</span></span>

![交換憑證][Delete_Swap_Cert]

## <a name="remove-a-cluster-certificate-using-hello-portal"></a><span data-ttu-id="1a52c-120">移除叢集憑證使用 hello 入口網站</span><span class="sxs-lookup"><span data-stu-id="1a52c-120">Remove a cluster certificate using hello portal</span></span>

<span data-ttu-id="1a52c-121">安全的叢集，您永遠必須至少一個有效 （未撤銷和未到期） 的憑證 （主要或次要） 部署否則 hello 叢集會停止運作。</span><span class="sxs-lookup"><span data-stu-id="1a52c-121">For a secure cluster, you will always need at least one valid (not revoked and not expired) certificate (primary or secondary) deployed if not, hello cluster stops functioning.</span></span>

<span data-ttu-id="1a52c-122">tooremove 用於叢集安全性、 瀏覽 toohello 安全性刀鋒視窗，然後選取 hello 'Delete' 選項從 hello 快顯功能表 hello 次要憑證上的次要憑證。</span><span class="sxs-lookup"><span data-stu-id="1a52c-122">tooremove a secondary certificate from being used for cluster security, Navigate toohello Security blade and select hello 'Delete' option from hello context menu on hello secondary certificate.</span></span>

<span data-ttu-id="1a52c-123">如果您的意圖是標示為主要，則需要 tooswap tooremove hello 憑證與 hello 次要在第一次，並 hello 升級完成之後，再刪除次要 hello。</span><span class="sxs-lookup"><span data-stu-id="1a52c-123">If your intent is tooremove hello certificate that is marked primary, then you will need tooswap it with hello secondary first, and then delete hello secondary after hello upgrade has completed.</span></span>

## <a name="add-a-secondary-certificate-using-resource-manager-powershell"></a><span data-ttu-id="1a52c-124">使用 Resource Manager Powershell 來新增次要憑證</span><span class="sxs-lookup"><span data-stu-id="1a52c-124">Add a secondary certificate using Resource Manager Powershell</span></span>

<span data-ttu-id="1a52c-125">這些步驟假設您熟悉資源管理員的運作方式，和已部署至少一個 Service Fabric 叢集，使用資源管理員範本，且有您用方便的 hello 叢集 tooset hello 範本。</span><span class="sxs-lookup"><span data-stu-id="1a52c-125">These steps assume that you are familiar with how Resource Manager works and have deployed atleast one Service Fabric cluster using a Resource Manager template, and have hello template that you used tooset up hello cluster handy.</span></span> <span data-ttu-id="1a52c-126">此外亦假設您可輕鬆自如地使用 JSON。</span><span class="sxs-lookup"><span data-stu-id="1a52c-126">It is also assumed that you are comfortable using JSON.</span></span>

> [!NOTE]
> <span data-ttu-id="1a52c-127">如果您要尋找範例範本和參數，您可以使用 toofollow 沿著或做為起點，然後從下載這[git 儲存機制](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample)。</span><span class="sxs-lookup"><span data-stu-id="1a52c-127">If you are looking for a sample template and parameters that you can use toofollow along or as a starting point, then download it from this [git-repo](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample).</span></span> 
> 
> 

### <a name="edit-your-resource-manager-template"></a><span data-ttu-id="1a52c-128">編輯您的 Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="1a52c-128">Edit your Resource Manager template</span></span>

<span data-ttu-id="1a52c-129">範例 5-VM-1-NodeTypes-Secure_Step2.JSON 沿著下列簡易，包含我們將會進行所有的 hello 編輯作業。</span><span class="sxs-lookup"><span data-stu-id="1a52c-129">For ease of following along, sample 5-VM-1-NodeTypes-Secure_Step2.JSON contains all hello edits we will be making.</span></span> <span data-ttu-id="1a52c-130">hello 範例位於[git 儲存機制](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample)。</span><span class="sxs-lookup"><span data-stu-id="1a52c-130">hello sample is available at [git-repo](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample).</span></span>

<span data-ttu-id="1a52c-131">**請確定 toofollow hello 的所有步驟**</span><span class="sxs-lookup"><span data-stu-id="1a52c-131">**Make sure toofollow all hello steps**</span></span>

<span data-ttu-id="1a52c-132">**步驟 1:** hello Resource Manager 範本使用您要叢集化的 toodeploy 開啟。</span><span class="sxs-lookup"><span data-stu-id="1a52c-132">**Step 1:** Open up hello Resource Manager template you used toodeploy you Cluster.</span></span> <span data-ttu-id="1a52c-133">（如果您已從上述儲存機制的 hello 下載 hello 範例，然後使用 5-VM-1-NodeTypes-Secure_Step1.JSON toodeploy 安全的叢集，然後開啟該範本。）</span><span class="sxs-lookup"><span data-stu-id="1a52c-133">(If you have downloaded hello sample from hello above repo, then Use 5-VM-1-NodeTypes-Secure_Step1.JSON toodeploy a secure cluster and then open up that template).</span></span>

<span data-ttu-id="1a52c-134">**步驟 2:**新增**兩個新的參數**"secCertificateThumbprint"和"secCertificateUrlValue 」 類型的"string"toohello 參數區段，您的範本。</span><span class="sxs-lookup"><span data-stu-id="1a52c-134">**Step 2:** Add **two new parameters** "secCertificateThumbprint" and "secCertificateUrlValue" of type "string" toohello parameter section of your template.</span></span> <span data-ttu-id="1a52c-135">您可以複製下列程式碼片段的 hello，並將它加入 toohello 範本。</span><span class="sxs-lookup"><span data-stu-id="1a52c-135">You can copy hello following code snippet and add it toohello template.</span></span> <span data-ttu-id="1a52c-136">根據您的範本 hello 來源，您可能已經已定義，如果是這樣移動 toohello 下一個步驟。</span><span class="sxs-lookup"><span data-stu-id="1a52c-136">Depending on hello source of your template, you may already have these defined, if so move toohello next step.</span></span> 
 
```JSON
   "secCertificateThumbprint": {
      "type": "string",
      "metadata": {
        "description": "Certificate Thumbprint"
      }
    },
    "secCertificateUrlValue": {
      "type": "string",
      "metadata": {
        "description": "Refers toohello location URL in your key vault where hello certificate was uploaded, it is should be in hello format of https://<name of hello vault>.vault.azure.net:443/secrets/<exact location>"
      }
    },

```

<span data-ttu-id="1a52c-137">**步驟 3:**變更 toohello **Microsoft.ServiceFabric/clusters**資源-您在範本中找出 hello"Microsoft.ServiceFabric/clusters 」 資源定義。</span><span class="sxs-lookup"><span data-stu-id="1a52c-137">**Step 3:** Make changes toohello **Microsoft.ServiceFabric/clusters** resource - Locate hello "Microsoft.ServiceFabric/clusters" resource definition in your template.</span></span> <span data-ttu-id="1a52c-138">在定義的屬性，您會發現 「 憑證 」 JSON 標記，這看起來應該類似下列 JSON 片段 hello:</span><span class="sxs-lookup"><span data-stu-id="1a52c-138">Under properties of that definition, you will find "Certificate" JSON tag, which should look something like hello following JSON snippet:</span></span>

   
```JSON
      "properties": {
        "certificate": {
          "thumbprint": "[parameters('certificateThumbprint')]",
          "x509StoreName": "[parameters('certificateStoreValue')]"
     }
``` 

<span data-ttu-id="1a52c-139">加入新標籤「thumbprintSecondary」，並為它提供值「[parameters('secCertificateThumbprint')]」。</span><span class="sxs-lookup"><span data-stu-id="1a52c-139">Add a new tag "thumbprintSecondary" and give it a value "[parameters('secCertificateThumbprint')]".</span></span>  

<span data-ttu-id="1a52c-140">因此現在 hello 資源定義應該看起來像下列 hello （根據您的 hello 範本的來源，可能無法完全一樣 hello 以下程式碼片段）。</span><span class="sxs-lookup"><span data-stu-id="1a52c-140">So now hello resource definition should look like hello following (depending on your source of hello template, it may not be exactly like hello snippet below).</span></span> 

```JSON
      "properties": {
        "certificate": {
          "thumbprint": "[parameters('certificateThumbprint')]",
          "thumbprintSecondary": "[parameters('secCertificateThumbprint')]",
          "x509StoreName": "[parameters('certificateStoreValue')]"
     }
``` 

<span data-ttu-id="1a52c-141">如果您想太**變換 hello cert**，然後將 hello 新憑證指定為主要及移動 hello 目前主要複本為次要資料庫。</span><span class="sxs-lookup"><span data-stu-id="1a52c-141">If you want too**rollover hello cert**, then specify hello new cert as primary and moving hello current primary as secondary.</span></span> <span data-ttu-id="1a52c-142">這會導致您的目前主要憑證 toohello 新憑證在一個部署步驟中的 hello 換用。</span><span class="sxs-lookup"><span data-stu-id="1a52c-142">This results in hello rollover of your current primary certificate toohello new certificate in one deployment step.</span></span>

```JSON
      "properties": {
        "certificate": {
          "thumbprint": "[parameters('secCertificateThumbprint')]",
          "thumbprintSecondary": "[parameters('certificateThumbprint')]",
          "x509StoreName": "[parameters('certificateStoreValue')]"
     }
``` 


<span data-ttu-id="1a52c-143">**步驟 4:**進行過變更**所有**hello **Microsoft.Compute/virtualMachineScaleSets**資源定義的尋找 hello Microsoft.Compute/virtualMachineScaleSets 資源定義。</span><span class="sxs-lookup"><span data-stu-id="1a52c-143">**Step 4:** Make changes too**all** hello **Microsoft.Compute/virtualMachineScaleSets** resource definitions - Locate hello Microsoft.Compute/virtualMachineScaleSets resource definition.</span></span> <span data-ttu-id="1a52c-144">捲動 toohello 「 發行者 」: 「 Microsoft.Azure.ServiceFabric"，"virtualMachineProfile"下的。</span><span class="sxs-lookup"><span data-stu-id="1a52c-144">Scroll toohello "publisher": "Microsoft.Azure.ServiceFabric", under "virtualMachineProfile".</span></span>

<span data-ttu-id="1a52c-145">在 hello 服務網狀架構 「 發行者 」 設定，您應該看到類似下面的。</span><span class="sxs-lookup"><span data-stu-id="1a52c-145">In hello service fabric publisher settings, you should see something like this.</span></span>

![Json_Pub_Setting1][Json_Pub_Setting1]

<span data-ttu-id="1a52c-147">加入新的憑證項目 tooit hello</span><span class="sxs-lookup"><span data-stu-id="1a52c-147">Add hello new cert entries tooit</span></span>

```JSON
               "certificateSecondary": {
                    "thumbprint": "[parameters('secCertificateThumbprint')]",
                    "x509StoreName": "[parameters('certificateStoreValue')]"
                    }
                  },

```

<span data-ttu-id="1a52c-148">hello 屬性現在看起來應該像這樣</span><span class="sxs-lookup"><span data-stu-id="1a52c-148">hello properties should now look like this</span></span>

![Json_Pub_Setting2][Json_Pub_Setting2]

<span data-ttu-id="1a52c-150">如果您想太**變換 hello cert**，然後將 hello 新憑證指定為主要及移動 hello 目前主要複本為次要資料庫。</span><span class="sxs-lookup"><span data-stu-id="1a52c-150">If you want too**rollover hello cert**, then specify hello new cert as primary and moving hello current primary as secondary.</span></span> <span data-ttu-id="1a52c-151">這會導致您的目前憑證 toohello 新憑證在一個部署步驟中的 hello 換用。</span><span class="sxs-lookup"><span data-stu-id="1a52c-151">This results in hello rollover of your current certificate toohello new certificate in one deployment step.</span></span> 


```JSON
               "certificate": {
                   "thumbprint": "[parameters('secCertificateThumbprint')]",
                   "x509StoreName": "[parameters('certificateStoreValue')]"
                     },
               "certificateSecondary": {
                    "thumbprint": "[parameters('certificateThumbprint')]",
                    "x509StoreName": "[parameters('certificateStoreValue')]"
                    }
                  },

```
<span data-ttu-id="1a52c-152">hello 屬性現在看起來應該像這樣</span><span class="sxs-lookup"><span data-stu-id="1a52c-152">hello properties should now look like this</span></span>

![Json_Pub_Setting3][Json_Pub_Setting3]


<span data-ttu-id="1a52c-154">**步驟 5:**變更太**所有**hello **Microsoft.Compute/virtualMachineScaleSets**資源定義的尋找 hello Microsoft.Compute/virtualMachineScaleSets 資源定義。</span><span class="sxs-lookup"><span data-stu-id="1a52c-154">**Step 5:** Make Changes too**all** hello **Microsoft.Compute/virtualMachineScaleSets** resource definitions - Locate hello Microsoft.Compute/virtualMachineScaleSets resource definition.</span></span> <span data-ttu-id="1a52c-155">捲動 toohello"vaultCertificates":，"OSProfile"下。</span><span class="sxs-lookup"><span data-stu-id="1a52c-155">Scroll toohello "vaultCertificates": , under "OSProfile".</span></span> <span data-ttu-id="1a52c-156">您應該會看到類似下面的畫面。</span><span class="sxs-lookup"><span data-stu-id="1a52c-156">it should look something like this.</span></span>


![Json_Pub_Setting4][Json_Pub_Setting4]

<span data-ttu-id="1a52c-158">新增 hello secCertificateUrlValue tooit。</span><span class="sxs-lookup"><span data-stu-id="1a52c-158">Add hello secCertificateUrlValue tooit.</span></span> <span data-ttu-id="1a52c-159">使用下列程式碼片段的 hello:</span><span class="sxs-lookup"><span data-stu-id="1a52c-159">use hello following snippet:</span></span>

```Json
                  {
                    "certificateStore": "[parameters('certificateStoreValue')]",
                    "certificateUrl": "[parameters('secCertificateUrlValue')]"
                  }

```
<span data-ttu-id="1a52c-160">立即產生 Json hello 看起來應該像這樣。</span><span class="sxs-lookup"><span data-stu-id="1a52c-160">Now hello resulting Json should look something like this.</span></span>
<span data-ttu-id="1a52c-161">![Json_Pub_Setting5][Json_Pub_Setting5]</span><span class="sxs-lookup"><span data-stu-id="1a52c-161">![Json_Pub_Setting5][Json_Pub_Setting5]</span></span>


> [!NOTE]
> <span data-ttu-id="1a52c-162">請確定您有重複的步驟 4 和 5 所有 hello Nodetypes/Microsoft.Compute/virtualMachineScaleSets 資源定義中您的範本。</span><span class="sxs-lookup"><span data-stu-id="1a52c-162">Make sure that you have repeated steps 4 and 5 for all hello Nodetypes/Microsoft.Compute/virtualMachineScaleSets resource definitions in your template.</span></span> <span data-ttu-id="1a52c-163">如果您錯過其中一個方法，該 VMSS 上不會安裝 hello 憑證，而且您必須在叢集中，包括 hello 叢集停機 （如果您不得到該 hello 叢集可以使用安全性的任何有效憑證無法預期結果。</span><span class="sxs-lookup"><span data-stu-id="1a52c-163">If you miss one of them, hello certificate will not get installed on that VMSS and you will have unpredictable results in your cluster, including hello cluster going down (if you end up with no valid certificates that hello cluster can use for security.</span></span> <span data-ttu-id="1a52c-164">因此，在進一步進行之前，請先仔細檢查。</span><span class="sxs-lookup"><span data-stu-id="1a52c-164">So please double check, before proceeding further.</span></span>
> 
> 


### <a name="edit-your-template-file-tooreflect-hello-new-parameters-you-added-above"></a><span data-ttu-id="1a52c-165">編輯您範本檔案 tooreflect hello 新參數加入之上</span><span class="sxs-lookup"><span data-stu-id="1a52c-165">Edit your template file tooreflect hello new parameters you added above</span></span>
<span data-ttu-id="1a52c-166">如果您使用從 hello hello 範例[git 儲存機制](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample)toofollow 以及，您可以在 hello 範例 5-VM-1-NodeTypes-Secure.paramters_Step2.JSON 啟動 toomake 變更</span><span class="sxs-lookup"><span data-stu-id="1a52c-166">If you are using hello sample from hello [git-repo](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample) toofollow along, you can start toomake changes in hello sample 5-VM-1-NodeTypes-Secure.paramters_Step2.JSON</span></span> 

<span data-ttu-id="1a52c-167">編輯您的資源管理員範本參數檔案，加入 hello 兩個新的參數 secCertificateThumbprint 和 secCertificateUrlValue。</span><span class="sxs-lookup"><span data-stu-id="1a52c-167">Edit your Resource Manager Template parameter File, add hello two new parameters for secCertificateThumbprint and secCertificateUrlValue.</span></span> 

```JSON
    "secCertificateThumbprint": {
      "value": "thumbprint value"
    },
    "secCertificateUrlValue": {
      "value": "Refers toohello location URL in your key vault where hello certificate was uploaded, it is should be in hello format of https://<name of hello vault>.vault.azure.net:443/secrets/<exact location>"
     },

```

### <a name="deploy-hello-template-tooazure"></a><span data-ttu-id="1a52c-168">部署 hello 範本 tooAzure</span><span class="sxs-lookup"><span data-stu-id="1a52c-168">Deploy hello template tooAzure</span></span>

- <span data-ttu-id="1a52c-169">您會立即準備 toodeploy 範本 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="1a52c-169">You are now ready toodeploy your template tooAzure.</span></span> <span data-ttu-id="1a52c-170">開啟 Azure PS 版本 1+ 命令提示字元。</span><span class="sxs-lookup"><span data-stu-id="1a52c-170">Open an Azure PS version 1+ command prompt.</span></span>
- <span data-ttu-id="1a52c-171">登入 tooyour Azure 帳戶，並選取 hello 特定的 azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="1a52c-171">Log in tooyour Azure Account and select hello specific azure subscription.</span></span> <span data-ttu-id="1a52c-172">這是擁有超過一個 azure 訂用帳戶的存取 toomore 同仁的一個重要步驟。</span><span class="sxs-lookup"><span data-stu-id="1a52c-172">This is an important step for folks who have access toomore than one azure subscription.</span></span>

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionId <Subcription ID> 

```

<span data-ttu-id="1a52c-173">測試 hello 範本先前 toodeploying 它。</span><span class="sxs-lookup"><span data-stu-id="1a52c-173">Test hello template prior toodeploying it.</span></span> <span data-ttu-id="1a52c-174">使用 hello 叢集目前已部署至同一個資源群組。</span><span class="sxs-lookup"><span data-stu-id="1a52c-174">Use hello same Resource Group that your cluster is currently deployed to.</span></span>

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName <Resource Group that your cluster is currently deployed to> -TemplateFile <PathToTemplate>

```

<span data-ttu-id="1a52c-175">部署 hello 範本 tooyour 資源群組。</span><span class="sxs-lookup"><span data-stu-id="1a52c-175">Deploy hello template tooyour resource group.</span></span> <span data-ttu-id="1a52c-176">使用 hello 叢集目前已部署至同一個資源群組。</span><span class="sxs-lookup"><span data-stu-id="1a52c-176">Use hello same Resource Group that your cluster is currently deployed to.</span></span> <span data-ttu-id="1a52c-177">執行 hello 新增 AzureRmResourceGroupDeployment 命令。</span><span class="sxs-lookup"><span data-stu-id="1a52c-177">Run hello New-AzureRmResourceGroupDeployment command.</span></span> <span data-ttu-id="1a52c-178">您不需要 toospecify hello 模式中，由於 hello 預設值為**累加**。</span><span class="sxs-lookup"><span data-stu-id="1a52c-178">You do not need toospecify hello mode, since hello default value is **incremental**.</span></span>

> [!NOTE]
> <span data-ttu-id="1a52c-179">如果您將設定模式 tooComplete，您可以不小心刪除不在範本中的資源。</span><span class="sxs-lookup"><span data-stu-id="1a52c-179">If you set Mode tooComplete, you can inadvertently delete resources that are not in your template.</span></span> <span data-ttu-id="1a52c-180">因此請勿在此案例中使用該模式。</span><span class="sxs-lookup"><span data-stu-id="1a52c-180">So do not use it in this scenario.</span></span>
> 
> 

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName <Resource Group that your cluster is currently deployed to> -TemplateFile <PathToTemplate>
```

<span data-ttu-id="1a52c-181">以下是已填入出 hello 的範例相同的 powershell。</span><span class="sxs-lookup"><span data-stu-id="1a52c-181">Here is a filled out example of hello same powershell.</span></span>

```powershell
$ResouceGroup2 = "chackosecure5"
$TemplateFile = "C:\GitHub\Service-Fabric\ARM Templates\Cert Rollover Sample\5-VM-1-NodeTypes-Secure_Step2.json"
$TemplateParmFile = "C:\GitHub\Service-Fabric\ARM Templates\Cert Rollover Sample\5-VM-1-NodeTypes-Secure.parameters_Step2.json"

New-AzureRmResourceGroupDeployment -ResourceGroupName $ResouceGroup2 -TemplateParameterFile $TemplateParmFile -TemplateUri $TemplateFile -clusterName $ResouceGroup2

```

<span data-ttu-id="1a52c-182">Tooyour 叢集使用 hello 部署完成之後，連接 hello 新的憑證，以及執行某些查詢。</span><span class="sxs-lookup"><span data-stu-id="1a52c-182">Once hello deployment is complete, connect tooyour cluster using hello new Certificate and perform some queries.</span></span> <span data-ttu-id="1a52c-183">如果您無法 toodo。</span><span class="sxs-lookup"><span data-stu-id="1a52c-183">If you are able toodo.</span></span> <span data-ttu-id="1a52c-184">然後您可以刪除 hello 舊的憑證。</span><span class="sxs-lookup"><span data-stu-id="1a52c-184">Then you can delete hello old certificate.</span></span> 

<span data-ttu-id="1a52c-185">如果您使用自我簽署的憑證，別忘了 tooimport 為本機的 TrustedPeople 憑證存放區。</span><span class="sxs-lookup"><span data-stu-id="1a52c-185">If you are using a self-signed certificate, do not forget tooimport them into your local TrustedPeople cert store.</span></span>

```powershell
######## Set up hello certs on your local box
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\TrustedPeople -FilePath c:\Mycertificates\chackdanTestCertificate9.pfx -Password (ConvertTo-SecureString -String abcd123 -AsPlainText -Force)
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\My -FilePath c:\Mycertificates\chackdanTestCertificate9.pfx -Password (ConvertTo-SecureString -String abcd123 -AsPlainText -Force)

```
<span data-ttu-id="1a52c-186">快速參考如下 hello 命令 tooconnect tooa 安全叢集</span><span class="sxs-lookup"><span data-stu-id="1a52c-186">For quick reference here is hello command tooconnect tooa secure cluster</span></span> 

```powershell
$ClusterName= "chackosecure5.westus.cloudapp.azure.com:19000"
$CertThumbprint= "70EF5E22ADB649799DA3C8B6A6BF7SD1D630F8F3" 

Connect-serviceFabricCluster -ConnectionEndpoint $ClusterName -KeepAliveIntervalInSec 10 `
    -X509Credential `
    -ServerCertThumbprint $CertThumbprint  `
    -FindType FindByThumbprint `
    -FindValue $CertThumbprint `
    -StoreLocation CurrentUser `
    -StoreName My
```
<span data-ttu-id="1a52c-187">快速參考如下 hello 命令 tooget 叢集健全狀況</span><span class="sxs-lookup"><span data-stu-id="1a52c-187">For quick reference here is hello command tooget cluster health</span></span>

```powershell
Get-ServiceFabricClusterHealth 
```

## <a name="deploying-application-certificates-toohello-cluster"></a><span data-ttu-id="1a52c-188">部署應用程式憑證 toohello 叢集。</span><span class="sxs-lookup"><span data-stu-id="1a52c-188">Deploying Application certificates toohello cluster.</span></span>

<span data-ttu-id="1a52c-189">您可以使用相同的步驟中所述的步驟 5 上方 toohave hello 憑證從 keyvault toohello 節點部署的 hello。</span><span class="sxs-lookup"><span data-stu-id="1a52c-189">You can use hello same steps as outlined in Steps 5 above toohave hello certificates deployed from a keyvault toohello Nodes.</span></span> <span data-ttu-id="1a52c-190">您只需定義和使用不同的參數即可。</span><span class="sxs-lookup"><span data-stu-id="1a52c-190">you just need define and use different parameters.</span></span>


## <a name="adding-or-removing-client-certificates"></a><span data-ttu-id="1a52c-191">新增或移除用戶端憑證</span><span class="sxs-lookup"><span data-stu-id="1a52c-191">Adding or removing Client certificates</span></span>

<span data-ttu-id="1a52c-192">在加法 toohello 叢集憑證，您可以加入用戶端憑證 tooperform service fabric 叢集上的管理作業。</span><span class="sxs-lookup"><span data-stu-id="1a52c-192">In addition toohello cluster certificates, you can add client certificates tooperform management operations on a service fabric cluster.</span></span>

<span data-ttu-id="1a52c-193">您可以新增兩種用戶端憑證 - 系統管理員或唯讀。</span><span class="sxs-lookup"><span data-stu-id="1a52c-193">You can add two kinds of client certificates - Admin or Read-only.</span></span> <span data-ttu-id="1a52c-194">這些然後可使用的 toocontrol 存取 toohello 管理作業和 hello 叢集上的查詢作業。</span><span class="sxs-lookup"><span data-stu-id="1a52c-194">These then can be used toocontrol access toohello admin operations and Query operations on hello cluster.</span></span> <span data-ttu-id="1a52c-195">根據預設，hello 叢集憑證會加入 toohello 允許系統管理員的憑證清單。</span><span class="sxs-lookup"><span data-stu-id="1a52c-195">By default, hello cluster certificates are added toohello allowed Admin certificates list.</span></span>

<span data-ttu-id="1a52c-196">您可以指定任何數目的用戶端憑證。</span><span class="sxs-lookup"><span data-stu-id="1a52c-196">you can specify any number of client certificates.</span></span> <span data-ttu-id="1a52c-197">每個新增/刪除導致組態更新 toohello service fabric 叢集</span><span class="sxs-lookup"><span data-stu-id="1a52c-197">Each addition/deletion results in a configuration update toohello service fabric cluster</span></span>


### <a name="adding-client-certificates---admin-or-read-only-via-portal"></a><span data-ttu-id="1a52c-198">透過入口網站新增用戶端憑證 - 系統管理員或唯讀</span><span class="sxs-lookup"><span data-stu-id="1a52c-198">Adding client certificates - Admin or Read-Only via portal</span></span>

1. <span data-ttu-id="1a52c-199">瀏覽 toohello 安全性刀鋒視窗中，並選取 hello '+ 驗證' hello 安全性刀鋒視窗頂端的按鈕。</span><span class="sxs-lookup"><span data-stu-id="1a52c-199">Navigate toohello Security blade, and select hello '+ Authentication' button on top of hello security blade.</span></span>
2. <span data-ttu-id="1a52c-200">在 hello 新增驗證刀鋒視窗中，選擇 hello '驗證類型'-'唯讀用戶端' 或 '管理用戶端'</span><span class="sxs-lookup"><span data-stu-id="1a52c-200">On hello 'Add Authentication' blade, choose hello 'Authentication Type' - 'Read-only client' or 'Admin client'</span></span>
3. <span data-ttu-id="1a52c-201">現在選擇 hello 授權方法。</span><span class="sxs-lookup"><span data-stu-id="1a52c-201">Now choose hello Authorization method.</span></span> <span data-ttu-id="1a52c-202">是否它應使用 hello 主體名稱或 hello 指紋查閱此憑證，這表示 tooService 網狀架構。</span><span class="sxs-lookup"><span data-stu-id="1a52c-202">This indicates tooService Fabric whether it should look up this certificate by using hello subject name or hello thumbprint.</span></span> <span data-ttu-id="1a52c-203">一般情況下，它不是很好的安全性作法 toouse hello 授權方法的主體名稱。</span><span class="sxs-lookup"><span data-stu-id="1a52c-203">In general, it is not a good security practice toouse hello authorization method of subject name.</span></span> 

![新增用戶端憑證][Add_Client_Cert]

### <a name="deletion-of-client-certificates---admin-or-read-only-using-hello-portal"></a><span data-ttu-id="1a52c-205">刪除的用戶端憑證-系統管理員或唯讀使用 hello 入口網站</span><span class="sxs-lookup"><span data-stu-id="1a52c-205">Deletion of Client Certificates - Admin or Read-Only using hello portal</span></span>

<span data-ttu-id="1a52c-206">tooremove 叢集安全性、 瀏覽 toohello 安全性刀鋒視窗，然後選取 hello 'Delete' 選項從 hello 內容功能表上 hello 特定憑證的正在使用的次要憑證。</span><span class="sxs-lookup"><span data-stu-id="1a52c-206">tooremove a secondary certificate from being used for cluster security, Navigate toohello Security blade and select hello 'Delete' option from hello context menu on hello specific certificate.</span></span>



## <a name="next-steps"></a><span data-ttu-id="1a52c-207">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1a52c-207">Next steps</span></span>
<span data-ttu-id="1a52c-208">如需有關叢集管理的詳細資訊，請參閱下列文件︰</span><span class="sxs-lookup"><span data-stu-id="1a52c-208">Read these articles for more information on cluster management:</span></span>

* [<span data-ttu-id="1a52c-209">Service Fabric 叢集升級程序與您的期望</span><span class="sxs-lookup"><span data-stu-id="1a52c-209">Service Fabric Cluster upgrade process and expectations from you</span></span>](service-fabric-cluster-upgrade.md)
* [<span data-ttu-id="1a52c-210">設定用戶端的角色型存取</span><span class="sxs-lookup"><span data-stu-id="1a52c-210">Setup role-based access for clients</span></span>](service-fabric-cluster-security-roles.md)

<!--Image references-->
[Delete_Swap_Cert]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_09.PNG
[Add_Client_Cert]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_13.PNG
[Json_Pub_Setting1]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_14.PNG
[Json_Pub_Setting2]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_15.PNG
[Json_Pub_Setting3]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_16.PNG
[Json_Pub_Setting4]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_17.PNG
[Json_Pub_Setting5]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_18.PNG


