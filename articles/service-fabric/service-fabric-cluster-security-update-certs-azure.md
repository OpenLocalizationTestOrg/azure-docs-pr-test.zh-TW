---
title: "管理 Azure Service Fabric 叢集中的憑證 | Microsoft Docs"
description: "說明如何在 Service Fabric 叢集新增新的憑證、變換憑證及移除憑證。"
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
ms.openlocfilehash: c433e8683755e454f9561f094269c3daccf78a62
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="add-or-remove-certificates-for-a-service-fabric-cluster-in-azure"></a><span data-ttu-id="bda0d-103">新增或移除 Azure 中 Service Fabric 叢集的憑證</span><span class="sxs-lookup"><span data-stu-id="bda0d-103">Add or remove certificates for a Service Fabric cluster in Azure</span></span>
<span data-ttu-id="bda0d-104">建議您熟悉 Service Fabric 使用 X.509 憑證的方式，以及熟悉[叢集安全性案例](service-fabric-cluster-security.md)。</span><span class="sxs-lookup"><span data-stu-id="bda0d-104">It is recommended that you familiarize yourself with how Service Fabric uses X.509 certificates and be familiar with the [Cluster security scenarios](service-fabric-cluster-security.md).</span></span> <span data-ttu-id="bda0d-105">您必須瞭解什麼是叢集憑證及其用途，方可繼續進行後續作業。</span><span class="sxs-lookup"><span data-stu-id="bda0d-105">You must understand what a cluster certificate is and what is used for, before you proceed further.</span></span>

<span data-ttu-id="bda0d-106">當您在叢集建立期間設定憑證安全性時，除了用戶端憑證之外，Service Fabric 還可讓您指定兩個叢集憑證：主要與次要。</span><span class="sxs-lookup"><span data-stu-id="bda0d-106">Service fabric lets you specify two cluster certificates, a primary and a secondary, when you configure certificate security during cluster creation, in addition to client certificates.</span></span> <span data-ttu-id="bda0d-107">請參閱[透過入口網站建立 Azure 叢集](service-fabric-cluster-creation-via-portal.md)或[透過 Azure Resource Manager 建立 Azure 叢集](service-fabric-cluster-creation-via-arm.md)，以詳細了解如何在建立這些叢集時進行叢集設定。</span><span class="sxs-lookup"><span data-stu-id="bda0d-107">Refer to [creating an azure cluster via portal](service-fabric-cluster-creation-via-portal.md) or [creating an azure cluster via Azure Resource Manager](service-fabric-cluster-creation-via-arm.md) for details on setting them up at create time.</span></span> <span data-ttu-id="bda0d-108">如果您在建立時僅指定一個叢集憑證，該憑證就會作為主要憑證。</span><span class="sxs-lookup"><span data-stu-id="bda0d-108">If you specify only one cluster certificate at create time, then that is used as the primary certificate.</span></span> <span data-ttu-id="bda0d-109">在叢集建立完成後，您可新增憑證做為次要憑證。</span><span class="sxs-lookup"><span data-stu-id="bda0d-109">After cluster creation, you can add a new certificate as a secondary.</span></span>

> [!NOTE]
> <span data-ttu-id="bda0d-110">針對安全叢集，您一律必須至少部署一個有效 (未撤銷或過期) 的叢集憑證 (主要或次要)，否則叢集將停止運作。</span><span class="sxs-lookup"><span data-stu-id="bda0d-110">For a secure cluster, you will always need at least one valid (not revoked and not expired) cluster certificate (primary or secondary) deployed (if not, the cluster stops functioning).</span></span> <span data-ttu-id="bda0d-111">在所有有效憑證到達到期日的 90 天前，系統會針對節點產生警告追蹤與警告健康狀態事件。</span><span class="sxs-lookup"><span data-stu-id="bda0d-111">90 days before all valid certificates reach expiration, the system generates a warning trace and also a warning health event on the node.</span></span> <span data-ttu-id="bda0d-112">目前並無 Service Fabric 針對此主題送出的電子郵件或其他任何通知。</span><span class="sxs-lookup"><span data-stu-id="bda0d-112">There is currently no email or any other notification that service fabric sends out on this topic.</span></span> 
> 
> 

## <a name="add-a-secondary-cluster-certificate-using-the-portal"></a><span data-ttu-id="bda0d-113">使用入口網站來新增次要叢集憑證</span><span class="sxs-lookup"><span data-stu-id="bda0d-113">Add a secondary cluster certificate using the portal</span></span>

<span data-ttu-id="bda0d-114">您無法透過 Azure 入口網站新增次要叢集憑證。</span><span class="sxs-lookup"><span data-stu-id="bda0d-114">Secondary cluster certificate cannot be added through the Azure portal.</span></span> <span data-ttu-id="bda0d-115">必須使用 Azure PowerShell 來執行該操作。</span><span class="sxs-lookup"><span data-stu-id="bda0d-115">You have to use Azure powershell for that.</span></span> <span data-ttu-id="bda0d-116">本文件稍後會簡要說明此程序。</span><span class="sxs-lookup"><span data-stu-id="bda0d-116">The process is outlined later in this document.</span></span>

## <a name="swap-the-cluster-certificates-using-the-portal"></a><span data-ttu-id="bda0d-117">使用入口網站來交換叢集憑證</span><span class="sxs-lookup"><span data-stu-id="bda0d-117">Swap the cluster certificates using the portal</span></span>

<span data-ttu-id="bda0d-118">在成功部署次要叢集憑證之後，如果您想要將主要憑證與次要憑證交換，則請瀏覽至 [安全性] 刀鋒視窗，然後從操作功能表中選取 [與主要憑證交換] 選項，以將次要憑證與主要憑證交換。</span><span class="sxs-lookup"><span data-stu-id="bda0d-118">After you have successfully deployed a secondary cluster certificate, if you want to swap the primary and secondary, then navigate to the Security blade, and select the 'Swap with primary' option from the context menu to swap the secondary cert with the primary cert.</span></span>

![交換憑證][Delete_Swap_Cert]

## <a name="remove-a-cluster-certificate-using-the-portal"></a><span data-ttu-id="bda0d-120">使用入口網站來移除叢集憑證</span><span class="sxs-lookup"><span data-stu-id="bda0d-120">Remove a cluster certificate using the portal</span></span>

<span data-ttu-id="bda0d-121">針對安全叢集，您一律必須至少部署一個有效 (未撤銷或過期) 的憑證 (主要或次要)，否則叢集將停止運作。</span><span class="sxs-lookup"><span data-stu-id="bda0d-121">For a secure cluster, you will always need at least one valid (not revoked and not expired) certificate (primary or secondary) deployed if not, the cluster stops functioning.</span></span>

<span data-ttu-id="bda0d-122">若要移除次要憑證，使其不用於叢集安全性，請瀏覽至 [安全性] 刀鋒視窗，然後從次要憑證上的操作功能表中選取 [刪除] 選項。</span><span class="sxs-lookup"><span data-stu-id="bda0d-122">To remove a secondary certificate from being used for cluster security, Navigate to the Security blade and select the 'Delete' option from the context menu on the secondary certificate.</span></span>

<span data-ttu-id="bda0d-123">如果您的目的是移除標示為主要的憑證，則您需要先將它與次要憑證交換，然後再於升級完成後刪除次要憑證。</span><span class="sxs-lookup"><span data-stu-id="bda0d-123">If your intent is to remove the certificate that is marked primary, then you will need to swap it with the secondary first, and then delete the secondary after the upgrade has completed.</span></span>

## <a name="add-a-secondary-certificate-using-resource-manager-powershell"></a><span data-ttu-id="bda0d-124">使用 Resource Manager Powershell 來新增次要憑證</span><span class="sxs-lookup"><span data-stu-id="bda0d-124">Add a secondary certificate using Resource Manager Powershell</span></span>

<span data-ttu-id="bda0d-125">這些步驟是假設您已熟悉 Resource Manager 的運作方式，並已使用 Resource Manager 範本至少部署一個 Service Fabric 叢集，而且已讓您使用的範本將叢集設定妥當。</span><span class="sxs-lookup"><span data-stu-id="bda0d-125">These steps assume that you are familiar with how Resource Manager works and have deployed atleast one Service Fabric cluster using a Resource Manager template, and have the template that you used to set up the cluster handy.</span></span> <span data-ttu-id="bda0d-126">此外亦假設您可輕鬆自如地使用 JSON。</span><span class="sxs-lookup"><span data-stu-id="bda0d-126">It is also assumed that you are comfortable using JSON.</span></span>

> [!NOTE]
> <span data-ttu-id="bda0d-127">如果您正在尋找可用來依循或作為起點的範例範本和參數，可從這個 [git 存放庫](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample)下載。</span><span class="sxs-lookup"><span data-stu-id="bda0d-127">If you are looking for a sample template and parameters that you can use to follow along or as a starting point, then download it from this [git-repo](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample).</span></span> 
> 
> 

### <a name="edit-your-resource-manager-template"></a><span data-ttu-id="bda0d-128">編輯您的 Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="bda0d-128">Edit your Resource Manager template</span></span>

<span data-ttu-id="bda0d-129">為了便於跟著操作，範例 5-VM-1-NodeTypes-Secure_Step2.JSON 包含我們將進行的所有編輯。</span><span class="sxs-lookup"><span data-stu-id="bda0d-129">For ease of following along, sample 5-VM-1-NodeTypes-Secure_Step2.JSON contains all the edits we will be making.</span></span> <span data-ttu-id="bda0d-130">您可以從 [git 存放庫](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample)取得該範例。</span><span class="sxs-lookup"><span data-stu-id="bda0d-130">the sample is available at [git-repo](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample).</span></span>

<span data-ttu-id="bda0d-131">**務必依照所有步驟操作**</span><span class="sxs-lookup"><span data-stu-id="bda0d-131">**Make sure to follow all the steps**</span></span>

<span data-ttu-id="bda0d-132">**步驟 1：**開啟您用來部署叢集的 Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="bda0d-132">**Step 1:** Open up the Resource Manager template you used to deploy you Cluster.</span></span> <span data-ttu-id="bda0d-133">(如果您已從上述儲存機制下載該範例，則請使用 5-VM-1-NodeTypes-Secure_Step1.JSON 來部署一個安全的叢集，然後開啟該範本)。</span><span class="sxs-lookup"><span data-stu-id="bda0d-133">(If you have downloaded the sample from the above repo, then Use 5-VM-1-NodeTypes-Secure_Step1.JSON to deploy a secure cluster and then open up that template).</span></span>

<span data-ttu-id="bda0d-134">**步驟 2：**將類型為 "string" 的**兩個新參數** "secCertificateThumbprint" 和 "secCertificateUrlValue" 新增到您範本的參數區段。</span><span class="sxs-lookup"><span data-stu-id="bda0d-134">**Step 2:** Add **two new parameters** "secCertificateThumbprint" and "secCertificateUrlValue" of type "string" to the parameter section of your template.</span></span> <span data-ttu-id="bda0d-135">您可以複製下列程式碼片段並新增到範本中。</span><span class="sxs-lookup"><span data-stu-id="bda0d-135">You can copy the following code snippet and add it to the template.</span></span> <span data-ttu-id="bda0d-136">視您的範本來源而定，這些有可能已經定義好，如果是這樣，請移至下一個步驟。</span><span class="sxs-lookup"><span data-stu-id="bda0d-136">Depending on the source of your template, you may already have these defined, if so move to the next step.</span></span> 
 
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
        "description": "Refers to the location URL in your key vault where the certificate was uploaded, it is should be in the format of https://<name of the vault>.vault.azure.net:443/secrets/<exact location>"
      }
    },

```

<span data-ttu-id="bda0d-137">**步驟 3：**對 **Microsoft.ServiceFabric/clusters** 資源進行變更 - 找出您範本中的 "Microsoft.ServiceFabric/clusters" 資源定義。</span><span class="sxs-lookup"><span data-stu-id="bda0d-137">**Step 3:** Make changes to the **Microsoft.ServiceFabric/clusters** resource - Locate the "Microsoft.ServiceFabric/clusters" resource definition in your template.</span></span> <span data-ttu-id="bda0d-138">在該定義的屬性底下，您會發現「憑證」JSON 標籤，看起來應該會像以下 JSON 程式碼片段：</span><span class="sxs-lookup"><span data-stu-id="bda0d-138">Under properties of that definition, you will find "Certificate" JSON tag, which should look something like the following JSON snippet:</span></span>

   
```JSON
      "properties": {
        "certificate": {
          "thumbprint": "[parameters('certificateThumbprint')]",
          "x509StoreName": "[parameters('certificateStoreValue')]"
     }
``` 

<span data-ttu-id="bda0d-139">加入新標籤「thumbprintSecondary」，並為它提供值「[parameters('secCertificateThumbprint')]」。</span><span class="sxs-lookup"><span data-stu-id="bda0d-139">Add a new tag "thumbprintSecondary" and give it a value "[parameters('secCertificateThumbprint')]".</span></span>  

<span data-ttu-id="bda0d-140">資源定義現在看起來應該像下面這樣 (視您的範本來源而定，可能不會與下面的程式碼片段完全相同)。</span><span class="sxs-lookup"><span data-stu-id="bda0d-140">So now the resource definition should look like the following (depending on your source of the template, it may not be exactly like the snippet below).</span></span> 

```JSON
      "properties": {
        "certificate": {
          "thumbprint": "[parameters('certificateThumbprint')]",
          "thumbprintSecondary": "[parameters('secCertificateThumbprint')]",
          "x509StoreName": "[parameters('certificateStoreValue')]"
     }
``` 

<span data-ttu-id="bda0d-141">如果您想要「變換憑證」，請將新憑證指定為主要憑證，並將目前的主要憑證移轉為次要憑證。</span><span class="sxs-lookup"><span data-stu-id="bda0d-141">If you want to **rollover the cert**, then specify the new cert as primary and moving the current primary as secondary.</span></span> <span data-ttu-id="bda0d-142">這可讓您透過單一部署步驟，就將目前的主要憑證變換成新憑證。</span><span class="sxs-lookup"><span data-stu-id="bda0d-142">This results in the rollover of your current primary certificate to the new certificate in one deployment step.</span></span>

```JSON
      "properties": {
        "certificate": {
          "thumbprint": "[parameters('secCertificateThumbprint')]",
          "thumbprintSecondary": "[parameters('certificateThumbprint')]",
          "x509StoreName": "[parameters('certificateStoreValue')]"
     }
``` 


<span data-ttu-id="bda0d-143">**步驟 4：**對**所有** **Microsoft.Compute/virtualMachineScaleSets** 資源定義進行變更 - 找出 Microsoft.Compute/virtualMachineScaleSets 資源定義。</span><span class="sxs-lookup"><span data-stu-id="bda0d-143">**Step 4:** Make changes to **all** the **Microsoft.Compute/virtualMachineScaleSets** resource definitions - Locate the Microsoft.Compute/virtualMachineScaleSets resource definition.</span></span> <span data-ttu-id="bda0d-144">捲動到 "virtualMachineProfile" 底下的 "publisher": "Microsoft.Azure.ServiceFabric"。</span><span class="sxs-lookup"><span data-stu-id="bda0d-144">Scroll to the "publisher": "Microsoft.Azure.ServiceFabric", under "virtualMachineProfile".</span></span>

<span data-ttu-id="bda0d-145">在 Service Fabric 發行者設定中，您應該會看到像這樣的畫面。</span><span class="sxs-lookup"><span data-stu-id="bda0d-145">In the service fabric publisher settings, you should see something like this.</span></span>

![Json_Pub_Setting1][Json_Pub_Setting1]

<span data-ttu-id="bda0d-147">請將新憑證項目新增到其中</span><span class="sxs-lookup"><span data-stu-id="bda0d-147">Add the new cert entries to it</span></span>

```JSON
               "certificateSecondary": {
                    "thumbprint": "[parameters('secCertificateThumbprint')]",
                    "x509StoreName": "[parameters('certificateStoreValue')]"
                    }
                  },

```

<span data-ttu-id="bda0d-148">屬性現在應該看起來像這樣</span><span class="sxs-lookup"><span data-stu-id="bda0d-148">The properties should now look like this</span></span>

![Json_Pub_Setting2][Json_Pub_Setting2]

<span data-ttu-id="bda0d-150">如果您想要「變換憑證」，請將新憑證指定為主要憑證，並將目前的主要憑證移轉為次要憑證。</span><span class="sxs-lookup"><span data-stu-id="bda0d-150">If you want to **rollover the cert**, then specify the new cert as primary and moving the current primary as secondary.</span></span> <span data-ttu-id="bda0d-151">這可讓您在單一部署步驟中，將目前的憑證變換為新憑證。</span><span class="sxs-lookup"><span data-stu-id="bda0d-151">This results in the rollover of your current certificate to the new certificate in one deployment step.</span></span> 


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
<span data-ttu-id="bda0d-152">屬性現在應該看起來像這樣</span><span class="sxs-lookup"><span data-stu-id="bda0d-152">The properties should now look like this</span></span>

![Json_Pub_Setting3][Json_Pub_Setting3]


<span data-ttu-id="bda0d-154">**步驟 5：**對「所有」**Microsoft.Compute/virtualMachineScaleSets** 資源定義進行變更 - 找出 Microsoft.Compute/virtualMachineScaleSets 資源定義。</span><span class="sxs-lookup"><span data-stu-id="bda0d-154">**Step 5:** Make Changes to **all** the **Microsoft.Compute/virtualMachineScaleSets** resource definitions - Locate the Microsoft.Compute/virtualMachineScaleSets resource definition.</span></span> <span data-ttu-id="bda0d-155">捲動到 "OSProfile" 底下的 "vaultCertificates":。</span><span class="sxs-lookup"><span data-stu-id="bda0d-155">Scroll to the "vaultCertificates": , under "OSProfile".</span></span> <span data-ttu-id="bda0d-156">您應該會看到類似下面的畫面。</span><span class="sxs-lookup"><span data-stu-id="bda0d-156">it should look something like this.</span></span>


![Json_Pub_Setting4][Json_Pub_Setting4]

<span data-ttu-id="bda0d-158">請將 secCertificateUrlValue 新增到其中。</span><span class="sxs-lookup"><span data-stu-id="bda0d-158">Add the secCertificateUrlValue to it.</span></span> <span data-ttu-id="bda0d-159">請使用下列程式碼片段：</span><span class="sxs-lookup"><span data-stu-id="bda0d-159">use the following snippet:</span></span>

```Json
                  {
                    "certificateStore": "[parameters('certificateStoreValue')]",
                    "certificateUrl": "[parameters('secCertificateUrlValue')]"
                  }

```
<span data-ttu-id="bda0d-160">產生的 Json 現在應該看起來像這樣。</span><span class="sxs-lookup"><span data-stu-id="bda0d-160">Now the resulting Json should look something like this.</span></span>
<span data-ttu-id="bda0d-161">![Json_Pub_Setting5][Json_Pub_Setting5]</span><span class="sxs-lookup"><span data-stu-id="bda0d-161">![Json_Pub_Setting5][Json_Pub_Setting5]</span></span>


> [!NOTE]
> <span data-ttu-id="bda0d-162">請確定您已針對範本中的所有 Nodetypes/Microsoft.Compute/virtualMachineScaleSets 資源定義重複步驟 4 和 5。</span><span class="sxs-lookup"><span data-stu-id="bda0d-162">Make sure that you have repeated steps 4 and 5 for all the Nodetypes/Microsoft.Compute/virtualMachineScaleSets resource definitions in your template.</span></span> <span data-ttu-id="bda0d-163">如果您遺漏其中一個，憑證就不會安裝在該 VMSS 上，而您的叢集中將會有無法預測的結果，包括叢集停止運作 (如果您最終沒有任何可供叢集用於安全性的有效憑證)。</span><span class="sxs-lookup"><span data-stu-id="bda0d-163">If you miss one of them, the certificate will not get installed on that VMSS and you will have unpredictable results in your cluster, including the cluster going down (if you end up with no valid certificates that the cluster can use for security.</span></span> <span data-ttu-id="bda0d-164">因此，在進一步進行之前，請先仔細檢查。</span><span class="sxs-lookup"><span data-stu-id="bda0d-164">So please double check, before proceeding further.</span></span>
> 
> 


### <a name="edit-your-template-file-to-reflect-the-new-parameters-you-added-above"></a><span data-ttu-id="bda0d-165">編輯您的範本檔案，以反映先前加入的新參數</span><span class="sxs-lookup"><span data-stu-id="bda0d-165">Edit your template file to reflect the new parameters you added above</span></span>
<span data-ttu-id="bda0d-166">如果您是依循來自 [git 儲存機制](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample)的範例進行操作，則可以開始在範例 5-VM-1-NodeTypes-Secure.paramters_Step2.JSON 中進行變更</span><span class="sxs-lookup"><span data-stu-id="bda0d-166">If you are using the sample from the [git-repo](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample) to follow along, you can start to make changes in The sample 5-VM-1-NodeTypes-Secure.paramters_Step2.JSON</span></span> 

<span data-ttu-id="bda0d-167">請編輯您的 Resource Manager 範本參數檔，新增 secCertificateThumbprint 和 secCertificateUrlValue 的兩個新參數。</span><span class="sxs-lookup"><span data-stu-id="bda0d-167">Edit your Resource Manager Template parameter File, add the two new parameters for secCertificateThumbprint and secCertificateUrlValue.</span></span> 

```JSON
    "secCertificateThumbprint": {
      "value": "thumbprint value"
    },
    "secCertificateUrlValue": {
      "value": "Refers to the location URL in your key vault where the certificate was uploaded, it is should be in the format of https://<name of the vault>.vault.azure.net:443/secrets/<exact location>"
     },

```

### <a name="deploy-the-template-to-azure"></a><span data-ttu-id="bda0d-168">將範本部署到 Azure</span><span class="sxs-lookup"><span data-stu-id="bda0d-168">Deploy the template to Azure</span></span>

- <span data-ttu-id="bda0d-169">您現在已可將範本部署至 Azure。</span><span class="sxs-lookup"><span data-stu-id="bda0d-169">You are now ready to deploy your template to Azure.</span></span> <span data-ttu-id="bda0d-170">開啟 Azure PS 版本 1+ 命令提示字元。</span><span class="sxs-lookup"><span data-stu-id="bda0d-170">Open an Azure PS version 1+ command prompt.</span></span>
- <span data-ttu-id="bda0d-171">登入您的 Azure 帳戶，並選取特定的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="bda0d-171">Log in to your Azure Account and select the specific azure subscription.</span></span> <span data-ttu-id="bda0d-172">對於擁有多個 Azure 訂用帳戶存取權的使用者而言，這是一個重要步驟。</span><span class="sxs-lookup"><span data-stu-id="bda0d-172">This is an important step for folks who have access to more than one azure subscription.</span></span>

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionId <Subcription ID> 

```

<span data-ttu-id="bda0d-173">部署範本前先進行測試。</span><span class="sxs-lookup"><span data-stu-id="bda0d-173">Test the template prior to deploying it.</span></span> <span data-ttu-id="bda0d-174">使用您目前在其中部署叢集的同一個資源群組。</span><span class="sxs-lookup"><span data-stu-id="bda0d-174">Use the same Resource Group that your cluster is currently deployed to.</span></span>

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName <Resource Group that your cluster is currently deployed to> -TemplateFile <PathToTemplate>

```

<span data-ttu-id="bda0d-175">將範本部署至您的資源群組。</span><span class="sxs-lookup"><span data-stu-id="bda0d-175">Deploy the template to your resource group.</span></span> <span data-ttu-id="bda0d-176">使用您目前在其中部署叢集的同一個資源群組。</span><span class="sxs-lookup"><span data-stu-id="bda0d-176">Use the same Resource Group that your cluster is currently deployed to.</span></span> <span data-ttu-id="bda0d-177">執行 New-AzureRmResourceGroupDeployment 命令。</span><span class="sxs-lookup"><span data-stu-id="bda0d-177">Run the New-AzureRmResourceGroupDeployment command.</span></span> <span data-ttu-id="bda0d-178">您無須指定模式，因為預設值為 **增量**。</span><span class="sxs-lookup"><span data-stu-id="bda0d-178">You do not need to specify the mode, since the default value is **incremental**.</span></span>

> [!NOTE]
> <span data-ttu-id="bda0d-179">若您將 [模式] 設為 [完整]，您可能會無意間刪除不在您範本中的資源。</span><span class="sxs-lookup"><span data-stu-id="bda0d-179">If you set Mode to Complete, you can inadvertently delete resources that are not in your template.</span></span> <span data-ttu-id="bda0d-180">因此請勿在此案例中使用該模式。</span><span class="sxs-lookup"><span data-stu-id="bda0d-180">So do not use it in this scenario.</span></span>
> 
> 

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName <Resource Group that your cluster is currently deployed to> -TemplateFile <PathToTemplate>
```

<span data-ttu-id="bda0d-181">以下是已填入資料的相同 Powershell 範例。</span><span class="sxs-lookup"><span data-stu-id="bda0d-181">Here is a filled out example of the same powershell.</span></span>

```powershell
$ResouceGroup2 = "chackosecure5"
$TemplateFile = "C:\GitHub\Service-Fabric\ARM Templates\Cert Rollover Sample\5-VM-1-NodeTypes-Secure_Step2.json"
$TemplateParmFile = "C:\GitHub\Service-Fabric\ARM Templates\Cert Rollover Sample\5-VM-1-NodeTypes-Secure.parameters_Step2.json"

New-AzureRmResourceGroupDeployment -ResourceGroupName $ResouceGroup2 -TemplateParameterFile $TemplateParmFile -TemplateUri $TemplateFile -clusterName $ResouceGroup2

```

<span data-ttu-id="bda0d-182">部署完成之後，使用新的憑證連線至叢集，並執行一些查詢。</span><span class="sxs-lookup"><span data-stu-id="bda0d-182">Once the deployment is complete, connect to your cluster using the new Certificate and perform some queries.</span></span> <span data-ttu-id="bda0d-183">若您可執行動作。</span><span class="sxs-lookup"><span data-stu-id="bda0d-183">If you are able to do.</span></span> <span data-ttu-id="bda0d-184">接著，您可以刪除舊憑證。</span><span class="sxs-lookup"><span data-stu-id="bda0d-184">Then you can delete the old certificate.</span></span> 

<span data-ttu-id="bda0d-185">若您是使用自我簽署憑證，請務必將它們匯入至本機 TrustedPeople 憑證存放區。</span><span class="sxs-lookup"><span data-stu-id="bda0d-185">If you are using a self-signed certificate, do not forget to import them into your local TrustedPeople cert store.</span></span>

```powershell
######## Set up the certs on your local box
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\TrustedPeople -FilePath c:\Mycertificates\chackdanTestCertificate9.pfx -Password (ConvertTo-SecureString -String abcd123 -AsPlainText -Force)
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\My -FilePath c:\Mycertificates\chackdanTestCertificate9.pfx -Password (ConvertTo-SecureString -String abcd123 -AsPlainText -Force)

```
<span data-ttu-id="bda0d-186">以下提供連線至安全叢集的命令的快速參考</span><span class="sxs-lookup"><span data-stu-id="bda0d-186">For quick reference here is the command to connect to a secure cluster</span></span> 

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
<span data-ttu-id="bda0d-187">以下提供取得叢集健康情況的命令的快速參考</span><span class="sxs-lookup"><span data-stu-id="bda0d-187">For quick reference here is the command to get cluster health</span></span>

```powershell
Get-ServiceFabricClusterHealth 
```

## <a name="deploying-application-certificates-to-the-cluster"></a><span data-ttu-id="bda0d-188">將應用程式憑證部署到叢集。</span><span class="sxs-lookup"><span data-stu-id="bda0d-188">Deploying Application certificates to the cluster.</span></span>

<span data-ttu-id="bda0d-189">您可以使用與上述步驟 5 中所述的相同步驟，將憑證從 Key Vault 部署到節點。</span><span class="sxs-lookup"><span data-stu-id="bda0d-189">You can use the same steps as outlined in Steps 5 above to have the certificates deployed from a keyvault to the Nodes.</span></span> <span data-ttu-id="bda0d-190">您只需定義和使用不同的參數即可。</span><span class="sxs-lookup"><span data-stu-id="bda0d-190">you just need define and use different parameters.</span></span>


## <a name="adding-or-removing-client-certificates"></a><span data-ttu-id="bda0d-191">新增或移除用戶端憑證</span><span class="sxs-lookup"><span data-stu-id="bda0d-191">Adding or removing Client certificates</span></span>

<span data-ttu-id="bda0d-192">除了叢集憑證之外，您還可以新增用戶端憑證以在 Service Fabric 叢集上執行管理作業。</span><span class="sxs-lookup"><span data-stu-id="bda0d-192">In addition to the cluster certificates, you can add client certificates to perform management operations on a service fabric cluster.</span></span>

<span data-ttu-id="bda0d-193">您可以新增兩種用戶端憑證 - 系統管理員或唯讀。</span><span class="sxs-lookup"><span data-stu-id="bda0d-193">You can add two kinds of client certificates - Admin or Read-only.</span></span> <span data-ttu-id="bda0d-194">接著這些憑證便可用來控制對叢集上系統管理員作業和查詢作業的存取。</span><span class="sxs-lookup"><span data-stu-id="bda0d-194">These then can be used to control access to the admin operations and Query operations on the cluster.</span></span> <span data-ttu-id="bda0d-195">叢集憑證預設會新增到允許的系統管理員憑證清單中。</span><span class="sxs-lookup"><span data-stu-id="bda0d-195">By default, the cluster certificates are added to the allowed Admin certificates list.</span></span>

<span data-ttu-id="bda0d-196">您可以指定任何數目的用戶端憑證。</span><span class="sxs-lookup"><span data-stu-id="bda0d-196">you can specify any number of client certificates.</span></span> <span data-ttu-id="bda0d-197">每次進行新增/刪除時，都會導致更新 Service Fabric 叢集的組態</span><span class="sxs-lookup"><span data-stu-id="bda0d-197">Each addition/deletion results in a configuration update to the service fabric cluster</span></span>


### <a name="adding-client-certificates---admin-or-read-only-via-portal"></a><span data-ttu-id="bda0d-198">透過入口網站新增用戶端憑證 - 系統管理員或唯讀</span><span class="sxs-lookup"><span data-stu-id="bda0d-198">Adding client certificates - Admin or Read-Only via portal</span></span>

1. <span data-ttu-id="bda0d-199">瀏覽至 [安全性] 刀鋒視窗，然後選取 [安全性] 刀鋒視窗頂端的 [+ 驗證] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="bda0d-199">Navigate to the Security blade, and select the '+ Authentication' button on top of the security blade.</span></span>
2. <span data-ttu-id="bda0d-200">在 [新增驗證] 刀鋒視窗上，選擇 [驗證類型] - [唯讀用戶端] 或 [系統管理員用戶端]</span><span class="sxs-lookup"><span data-stu-id="bda0d-200">On the 'Add Authentication' blade, choose the 'Authentication Type' - 'Read-only client' or 'Admin client'</span></span>
3. <span data-ttu-id="bda0d-201">現在選擇 [驗證方法]。</span><span class="sxs-lookup"><span data-stu-id="bda0d-201">Now choose the Authorization method.</span></span> <span data-ttu-id="bda0d-202">這會對 Service Fabric 指出其是否應該使用主體名稱或指紋來查詢此憑證。</span><span class="sxs-lookup"><span data-stu-id="bda0d-202">This indicates to Service Fabric whether it should look up this certificate by using the subject name or the thumbprint.</span></span> <span data-ttu-id="bda0d-203">一般而言，使用主體名稱授權方法不是很好的安全性做法。</span><span class="sxs-lookup"><span data-stu-id="bda0d-203">In general, it is not a good security practice to use the authorization method of subject name.</span></span> 

![新增用戶端憑證][Add_Client_Cert]

### <a name="deletion-of-client-certificates---admin-or-read-only-using-the-portal"></a><span data-ttu-id="bda0d-205">使用入口網站來刪除用戶端憑證 - 系統管理員或唯讀</span><span class="sxs-lookup"><span data-stu-id="bda0d-205">Deletion of Client Certificates - Admin or Read-Only using the portal</span></span>

<span data-ttu-id="bda0d-206">若要移除次要憑證，使其不用於叢集安全性，請瀏覽至 [安全性] 刀鋒視窗，然後從特定憑證上的操作功能表中選取 [刪除] 選項。</span><span class="sxs-lookup"><span data-stu-id="bda0d-206">To remove a secondary certificate from being used for cluster security, Navigate to the Security blade and select the 'Delete' option from the context menu on the specific certificate.</span></span>



## <a name="next-steps"></a><span data-ttu-id="bda0d-207">後續步驟</span><span class="sxs-lookup"><span data-stu-id="bda0d-207">Next steps</span></span>
<span data-ttu-id="bda0d-208">如需有關叢集管理的詳細資訊，請參閱下列文件︰</span><span class="sxs-lookup"><span data-stu-id="bda0d-208">Read these articles for more information on cluster management:</span></span>

* [<span data-ttu-id="bda0d-209">Service Fabric 叢集升級程序與您的期望</span><span class="sxs-lookup"><span data-stu-id="bda0d-209">Service Fabric Cluster upgrade process and expectations from you</span></span>](service-fabric-cluster-upgrade.md)
* [<span data-ttu-id="bda0d-210">設定用戶端的角色型存取</span><span class="sxs-lookup"><span data-stu-id="bda0d-210">Setup role-based access for clients</span></span>](service-fabric-cluster-security-roles.md)

<!--Image references-->
[Delete_Swap_Cert]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_09.PNG
[Add_Client_Cert]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_13.PNG
[Json_Pub_Setting1]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_14.PNG
[Json_Pub_Setting2]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_15.PNG
[Json_Pub_Setting3]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_16.PNG
[Json_Pub_Setting4]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_17.PNG
[Json_Pub_Setting5]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_18.PNG


