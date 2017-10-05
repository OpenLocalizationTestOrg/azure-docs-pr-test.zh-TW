---
title: "Azure 虛擬機器擴展集常見問題集 | Microsoft Docs"
description: "取得關於虛擬機器擴展集常見問題集的解答。"
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
ms.date: 7/20/2017
ms.author: negat
ms.custom: na
ms.openlocfilehash: f320dd5d1f8c99317792f4ae9e09bc5adaf79e25
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="azure-virtual-machine-scale-sets-faqs"></a><span data-ttu-id="6f5c7-103">Azure 虛擬機器擴展集常見問題集</span><span class="sxs-lookup"><span data-stu-id="6f5c7-103">Azure virtual machine scale sets FAQs</span></span>

<span data-ttu-id="6f5c7-104">取得關於 Azure 中虛擬機器擴展集常見問題集的解答。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-104">Get answers to frequently asked questions about virtual machine scale sets in Azure.</span></span>

## <a name="autoscale"></a><span data-ttu-id="6f5c7-105">Autoscale</span><span class="sxs-lookup"><span data-stu-id="6f5c7-105">Autoscale</span></span>

### <a name="what-are-best-practices-for-azure-autoscale"></a><span data-ttu-id="6f5c7-106">什麼是 Azure 自動調整的最佳做法？</span><span class="sxs-lookup"><span data-stu-id="6f5c7-106">What are best practices for Azure Autoscale?</span></span>

<span data-ttu-id="6f5c7-107">如需自動調整的最佳做法，請參閱[自動調整虛擬機器的最佳做法](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-autoscale-best-practices)。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-107">For best practices for Autoscale, see [Best practices for autoscaling virtual machines](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-autoscale-best-practices).</span></span>

### <a name="where-do-i-find-metric-names-for-autoscaling-that-uses-host-based-metrics"></a><span data-ttu-id="6f5c7-108">哪裡可以找到使用主機型計量自動調整的計量名稱？</span><span class="sxs-lookup"><span data-stu-id="6f5c7-108">Where do I find metric names for autoscaling that uses host-based metrics?</span></span>

<span data-ttu-id="6f5c7-109">如需使用主機型計量之自動調整的計量名稱，請參閱[支援的 Azure 監視器度量](https://azure.microsoft.com/documentation/articles/monitoring-supported-metrics/)。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-109">For metric names for autoscaling that uses host-based metrics, see [Supported metrics with Azure Monitor](https://azure.microsoft.com/documentation/articles/monitoring-supported-metrics/).</span></span>

### <a name="are-there-any-examples-of-autoscaling-based-on-an-azure-service-bus-topic-and-queue-length"></a><span data-ttu-id="6f5c7-110">是否有任何根據 Azure 服務匯流排主題和佇列長度自動調整的範例？</span><span class="sxs-lookup"><span data-stu-id="6f5c7-110">Are there any examples of autoscaling based on an Azure Service Bus topic and queue length?</span></span>

<span data-ttu-id="6f5c7-111">是。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-111">Yes.</span></span> <span data-ttu-id="6f5c7-112">如需根據 Azure 服務匯流排主題和佇列長度自動調整的範例，請參閱 [Azure 監視器的自動調整常用計量](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/)。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-112">For examples of autoscaling based on an Azure Service Bus topic and queue length, see [Azure Monitor autoscaling common metrics](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/).</span></span>

<span data-ttu-id="6f5c7-113">如需服務匯流排佇列，請使用下列 JSON：</span><span class="sxs-lookup"><span data-stu-id="6f5c7-113">For a Service Bus queue, use the following JSON:</span></span>

```json
"metricName": "MessageCount",
"metricNamespace": "",
"metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.ServiceBus/namespaces/mySB/queues/myqueue"
```

<span data-ttu-id="6f5c7-114">如需儲存體佇列，請使用下列 JSON：</span><span class="sxs-lookup"><span data-stu-id="6f5c7-114">For a storage queue, use the following JSON:</span></span>

```json
"metricName": "ApproximateMessageCount",
"metricNamespace": "",
"metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.ClassicStorage/storageAccounts/mystorage/services/queue/queues/mystoragequeue"
```

<span data-ttu-id="6f5c7-115">以您資源的統一資源識別項 (URI) 取代範例值。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-115">Replace example values with your resource Uniform Resource Identifiers (URIs).</span></span>


### <a name="should-i-autoscale-by-using-host-based-metrics-or-a-diagnostics-extension"></a><span data-ttu-id="6f5c7-116">我應該使用主機型計量或診斷擴充功能進行自動調整？</span><span class="sxs-lookup"><span data-stu-id="6f5c7-116">Should I autoscale by using host-based metrics or a diagnostics extension?</span></span>

<span data-ttu-id="6f5c7-117">您可以在 VM 上建立自動調整設定，以使用主機層級計量或客體 OS 型計量。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-117">You can create an autoscale setting on a VM to use host-level metrics or guest OS-based metrics.</span></span>

<span data-ttu-id="6f5c7-118">如需支援的計量資訊，請參閱 [Azure 監視器的自動調整常見計量](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-autoscale-common-metrics)。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-118">For a list of supported metrics, see [Azure Monitor autoscaling common metrics](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-autoscale-common-metrics).</span></span> 

<span data-ttu-id="6f5c7-119">如需虛擬機器擴展集的完整範例，請參閱[使用虛擬機器擴展集的 Resource Manager 範本進行進階自動調整設定](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-advanced-autoscale-virtual-machine-scale-sets)。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-119">For a full sample for virtual machine scale sets, see [Advanced autoscale configuration by using Resource Manager templates for virtual machine scale sets](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-advanced-autoscale-virtual-machine-scale-sets).</span></span> 

<span data-ttu-id="6f5c7-120">此範例使用主機層級 CPU 計量及訊息計數計量。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-120">The sample uses the host-level CPU metric and a message count metric.</span></span>



### <a name="how-do-i-set-alert-rules-on-a-virtual-machine-scale-set"></a><span data-ttu-id="6f5c7-121">如何設定虛擬機器擴展集的警示規則？</span><span class="sxs-lookup"><span data-stu-id="6f5c7-121">How do I set alert rules on a virtual machine scale set?</span></span>

<span data-ttu-id="6f5c7-122">您可以透過 PowerShell 或 Azure CLI，建立虛擬機器擴展集計量的警示。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-122">You can create alerts on metrics for virtual machine scale sets via PowerShell or Azure CLI.</span></span> <span data-ttu-id="6f5c7-123">如需詳細資訊，請參閱 [Azure 監視器 PowerShell 快速入門範例](https://azure.microsoft.com/documentation/articles/insights-powershell-samples/#create-alert-rules)和 [Azure 監視器跨平台 CLI 快速入門範例](https://azure.microsoft.com/documentation/articles/insights-cli-samples/#work-with-alerts)。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-123">For more information, see [Azure Monitor PowerShell quick start samples](https://azure.microsoft.com/documentation/articles/insights-powershell-samples/#create-alert-rules) and [Azure Monitor cross-platform CLI quick start samples](https://azure.microsoft.com/documentation/articles/insights-cli-samples/#work-with-alerts).</span></span>

<span data-ttu-id="6f5c7-124">虛擬機器擴展集的 TargetResourceId 如下所示：</span><span class="sxs-lookup"><span data-stu-id="6f5c7-124">The TargetResourceId of the virtual machine scale set looks like this:</span></span> 

<span data-ttu-id="6f5c7-125">/subscriptions/yoursubscriptionid/resourceGroups/yourresourcegroup/providers/Microsoft.Compute/virtualMachineScaleSets/yourvmssname</span><span class="sxs-lookup"><span data-stu-id="6f5c7-125">/subscriptions/yoursubscriptionid/resourceGroups/yourresourcegroup/providers/Microsoft.Compute/virtualMachineScaleSets/yourvmssname</span></span>

<span data-ttu-id="6f5c7-126">您可以選擇任何 VM 效能計數器做為要設定警示的計量。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-126">You can choose any VM performance counter as the metric to set an alert for.</span></span> <span data-ttu-id="6f5c7-127">如需詳細資訊，請參閱 [Azure 監視器的自動調整常用計量](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/)一文中的 [Resource Manager 型 Windows VM 的客體 OS 計量](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/#guest-os-metrics-resource-manager-based-windows-vms)和 [Linux VM 的客體 OS 計量](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/#guest-os-metrics-linux-vms)。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-127">For more information, see [Guest OS metrics for Resource Manager-based Windows VMs](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/#guest-os-metrics-resource-manager-based-windows-vms) and [Guest OS metrics for Linux VMs](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/#guest-os-metrics-linux-vms) in the [Azure Monitor autoscaling common metrics](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/) article.</span></span>

### <a name="how-do-i-set-up-autoscale-on-a-virtual-machine-scale-set-by-using-powershell"></a><span data-ttu-id="6f5c7-128">如何使用 PowerShell 在虛擬機器擴展集上設定自動調整？</span><span class="sxs-lookup"><span data-stu-id="6f5c7-128">How do I set up autoscale on a virtual machine scale set by using PowerShell?</span></span>

<span data-ttu-id="6f5c7-129">若要使用 PowerShell 在虛擬機器擴展集上設定自動調整，請參閱部落格文章[如何將自動調整新增至 Azure 虛擬機器擴展集](https://msftstack.wordpress.com/2017/03/05/how-to-add-autoscale-to-an-azure-vm-scale-set/)。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-129">To set up autoscale on a virtual machine scale set by using PowerShell, see the blog post [How to add autoscale to an Azure virtual machine scale set](https://msftstack.wordpress.com/2017/03/05/how-to-add-autoscale-to-an-azure-vm-scale-set/).</span></span>




## <a name="certificates"></a><span data-ttu-id="6f5c7-130">憑證</span><span class="sxs-lookup"><span data-stu-id="6f5c7-130">Certificates</span></span>

### <a name="how-do-i-securely-ship-a-certificate-to-the-vm-how-do-i-provision-a-virtual-machine-scale-set-to-run-a-website-where-the-ssl-for-the-website-is-shipped-securely-from-a-certificate-configuration-the-common-certificate-rotation-operation-would-be-almost-the-same-as-a-configuration-update-operation-do-you-have-an-example-of-how-to-do-this"></a><span data-ttu-id="6f5c7-131">如何安全地將憑證送至 VM？</span><span class="sxs-lookup"><span data-stu-id="6f5c7-131">How do I securely ship a certificate to the VM?</span></span> <span data-ttu-id="6f5c7-132">如何佈建虛擬機器擴展集來執行網站 (其中網站的 SSL 會安全地從憑證組態送出)？</span><span class="sxs-lookup"><span data-stu-id="6f5c7-132">How do I provision a virtual machine scale set to run a website where the SSL for the website is shipped securely from a certificate configuration?</span></span> <span data-ttu-id="6f5c7-133">(常見的憑證旋轉作業幾乎與組態更新作業相同。)您是否有如何進行這項操作的範例？</span><span class="sxs-lookup"><span data-stu-id="6f5c7-133">(The common certificate rotation operation would be almost the same as a configuration update operation.) Do you have an example of how to do this?</span></span> 

<span data-ttu-id="6f5c7-134">若要安全地將憑證送至 VM，您可以將客戶憑證直接安裝至客戶金鑰保存庫中的 Windows 憑證存放區。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-134">To securely ship a certificate to the VM, you can install a customer certificate directly into a Windows certificate store from the customer's key vault.</span></span>

<span data-ttu-id="6f5c7-135">使用下列 JSON：</span><span class="sxs-lookup"><span data-stu-id="6f5c7-135">Use the following JSON:</span></span>

```json
"secrets": [
    {
        "sourceVault": {
            "id": "/subscriptions/{subscriptionid}/resourceGroups/myrg1/providers/Microsoft.KeyVault/vaults/mykeyvault1"
        },
        "vaultCertificates": [
            {
                "certificateUrl": "https://mykeyvault1.vault.azure.net/secrets/{secretname}/{secret-version}",
                "certificateStore": "certificateStoreName"
            }
        ]
    }
]
```

<span data-ttu-id="6f5c7-136">程式碼支援 Windows 和 Linux。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-136">The code supports Windows and Linux.</span></span>

<span data-ttu-id="6f5c7-137">如需詳細資訊，請參閱[建立或更新虛擬機器擴展集](https://msdn.microsoft.com/library/mt589035.aspx)。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-137">For more information, see [Create or update a virtual machine scale set](https://msdn.microsoft.com/library/mt589035.aspx).</span></span>


### <a name="example-of-self-signed-certificate"></a><span data-ttu-id="6f5c7-138">自我簽署憑證的範例</span><span class="sxs-lookup"><span data-stu-id="6f5c7-138">Example of Self-signed certificate</span></span>

1.  <span data-ttu-id="6f5c7-139">在金鑰保存庫中建立自我簽署憑證。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-139">Create a self-signed certificate in a key vault.</span></span>

    <span data-ttu-id="6f5c7-140">使用下列 PowerShell 命令：</span><span class="sxs-lookup"><span data-stu-id="6f5c7-140">Use the following PowerShell commands:</span></span>

    ```powershell
    Import-Module "C:\Users\mikhegn\Downloads\Service-Fabric-master\Scripts\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1"

    Login-AzureRmAccount

    Invoke-AddCertToKeyVault -SubscriptionId <Your SubID> -ResourceGroupName KeyVault -Location westus -VaultName MikhegnVault -CertificateName VMSSCert -Password VmssCert -CreateSelfSignedCertificate -DnsName vmss.mikhegn.azure.com -OutputPath c:\users\mikhegn\desktop\
    ```

    <span data-ttu-id="6f5c7-141">此命令可讓您輸入 Azure Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-141">This command gives you the input for the Azure Resource Manager template.</span></span>

    <span data-ttu-id="6f5c7-142">如需如何在金鑰保存庫中建立自我簽署憑證的範例，請參閱 [Service Fabric 叢集安全性案例](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/)一文。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-142">For an example of how to create a self-signed certificate in a key vault, see [Service Fabric cluster security scenarios](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/).</span></span>

2.  <span data-ttu-id="6f5c7-143">變更 Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-143">Change the Resource Manager template.</span></span>

    <span data-ttu-id="6f5c7-144">將這個屬性新增至 **virtualMachineProfile** 成為虛擬機器擴展集資源的一部分︰</span><span class="sxs-lookup"><span data-stu-id="6f5c7-144">Add this property to **virtualMachineProfile**, as part of the virtual machine scale set resource:</span></span>

    ```json 
    "osProfile": {
        "computerNamePrefix": "[variables('namingInfix')]",
        "adminUsername": "[parameters('adminUsername')]",
        "adminPassword": "[parameters('adminPassword')]",
        "secrets": [
            {
                "sourceVault": {
                    "id": "[resourceId('KeyVault', 'Microsoft.KeyVault/vaults', 'MikhegnVault')]"
                },
                "vaultCertificates": [
                    {
                        "certificateUrl": "https://mikhegnvault.vault.azure.net:443/secrets/VMSSCert/20709ca8faee4abb84bc6f4611b088a4",
                        "certificateStore": "My"
                    }
                ]
            }
        ]
    }
    ```
  

### <a name="can-i-specify-an-ssh-key-pair-to-use-for-ssh-authentication-with-a-linux-virtual-machine-scale-set-from-a-resource-manager-template"></a><span data-ttu-id="6f5c7-145">是否可指定 SSH 金鑰組以便透過 Resource Manager 範本中的 Linux 虛擬機器擴展集來進行 SSH 驗證？</span><span class="sxs-lookup"><span data-stu-id="6f5c7-145">Can I specify an SSH key pair to use for SSH authentication with a Linux virtual machine scale set from a Resource Manager template?</span></span>  

<span data-ttu-id="6f5c7-146">是。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-146">Yes.</span></span> <span data-ttu-id="6f5c7-147">**osProfile** 的 REST API 類似於標準 VM REST API。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-147">The REST API for **osProfile** is similar to the standard VM REST API.</span></span> 

<span data-ttu-id="6f5c7-148">在您的範本中包含 **osProfile**︰</span><span class="sxs-lookup"><span data-stu-id="6f5c7-148">Include **osProfile** in your template:</span></span>

```json 
"osProfile": {
    "computerName": "[variables('vmName')]",
    "adminUsername": "[parameters('adminUserName')]",
    "linuxConfiguration": {
        "disablePasswordAuthentication": "true",
        "ssh": {
            "publicKeys": [
                {
                    "path": "[variables('sshKeyPath')]",
                    "keyData": "[parameters('sshKeyData')]"
                }
            ]
        }
    }
}
```
 
<span data-ttu-id="6f5c7-149">此 JSON 區塊使用於 [101-vm-sshkey GitHub 快速入門範本](https://github.com/Azure/azure-quickstart-templates/blob/master/101-vm-sshkey/azuredeploy.json)。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-149">This JSON block is used in [the 101-vm-sshkey GitHub quick start template](https://github.com/Azure/azure-quickstart-templates/blob/master/101-vm-sshkey/azuredeploy.json).</span></span>
 
<span data-ttu-id="6f5c7-150">OS 設定檔也會使用於 [grelayhost.json GitHub 快速入門範本](https://github.com/ExchMaster/gadgetron/blob/master/Gadgetron/Templates/grelayhost.json)。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-150">The OS profile also is used in [the grelayhost.json GitHub quick start template](https://github.com/ExchMaster/gadgetron/blob/master/Gadgetron/Templates/grelayhost.json).</span></span>

<span data-ttu-id="6f5c7-151">如需詳細資訊，請參閱[建立或更新虛擬機器擴展集](https://msdn.microsoft.com/library/azure/mt589035.aspx#linuxconfiguration)。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-151">For more information, see [Create or update a virtual machine scale set](https://msdn.microsoft.com/library/azure/mt589035.aspx#linuxconfiguration).</span></span>
  

### <a name="how-do-i-remove-deprecated-certificates"></a><span data-ttu-id="6f5c7-152">如何移除已被取代的憑證？</span><span class="sxs-lookup"><span data-stu-id="6f5c7-152">How do I remove deprecated certificates?</span></span> 

<span data-ttu-id="6f5c7-153">若要移除已被取代的憑證，請從保存庫憑證清單中移除舊的憑證。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-153">To remove deprecated certificates, remove the old certificate from the vault certificates list.</span></span> <span data-ttu-id="6f5c7-154">將您想要的所有憑證保留在清單中的電腦上。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-154">Leave all the certificates that you want to remain on your computer in the list.</span></span> <span data-ttu-id="6f5c7-155">這樣不會從所有的 VM 移除憑證。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-155">This does not remove the certificate from all your VMs.</span></span> <span data-ttu-id="6f5c7-156">但也不會將憑證新增至虛擬機器擴展集中所建立的新 VM。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-156">It also does not add the certificate to new VMs that are created in the virtual machine scale set.</span></span> 

<span data-ttu-id="6f5c7-157">若要從現有的 VM 中移除憑證，請撰寫自訂指令碼擴充孤能，以從您的憑證存放區中手動移除憑證。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-157">To remove the certificate from existing VMs, write a custom script extension to manually remove the certificates from your certificate store.</span></span>
 
### <a name="how-do-i-inject-an-existing-ssh-public-key-into-the-virtual-machine-scale-set-ssh-layer-during-provisioning-i-want-to-store-the-ssh-public-key-values-in-azure-key-vault-and-then-use-them-in-my-resource-manager-template"></a><span data-ttu-id="6f5c7-158">如何在佈建期間將現有的 SSH 公開金鑰插入至虛擬機器擴展集 SSH 層？</span><span class="sxs-lookup"><span data-stu-id="6f5c7-158">How do I inject an existing SSH public key into the virtual machine scale set SSH layer during provisioning?</span></span> <span data-ttu-id="6f5c7-159">我想要將 SSH 公開金鑰值儲存在 Azure Key Vault 中，然後在我的 Resource Manager 範本中使用它們。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-159">I want to store the SSH public key values in Azure Key Vault, and then use them in my Resource Manager template.</span></span>

<span data-ttu-id="6f5c7-160">如果您只透過 SSH 公開金鑰提供 VM，則不需要將公開金鑰放在 Key Vault 中。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-160">If you are providing the VMs only with a public SSH key, you don't need to put the public keys in Key Vault.</span></span> <span data-ttu-id="6f5c7-161">公開金鑰不是密碼。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-161">Public keys are not secret.</span></span>
 
<span data-ttu-id="6f5c7-162">您可以在建立 Linux VM 時以純文字提供 SSH 公開金鑰：</span><span class="sxs-lookup"><span data-stu-id="6f5c7-162">You can provide SSH public keys in plain text when you create a Linux VM:</span></span>

```json
"linuxConfiguration": {
    "ssh": {
        "publicKeys": [
            {
                "path": "path",
                "keyData": "publickey"
            }
        ]
    }
```
 
<span data-ttu-id="6f5c7-163">linuxConfiguration 元素名稱</span><span class="sxs-lookup"><span data-stu-id="6f5c7-163">linuxConfiguration element name</span></span> | <span data-ttu-id="6f5c7-164">必要</span><span class="sxs-lookup"><span data-stu-id="6f5c7-164">Required</span></span> | <span data-ttu-id="6f5c7-165">類型</span><span class="sxs-lookup"><span data-stu-id="6f5c7-165">Type</span></span> | <span data-ttu-id="6f5c7-166">說明</span><span class="sxs-lookup"><span data-stu-id="6f5c7-166">Description</span></span>
--- | --- | --- | --- |  ---
<span data-ttu-id="6f5c7-167">ssh</span><span class="sxs-lookup"><span data-stu-id="6f5c7-167">ssh</span></span> | <span data-ttu-id="6f5c7-168">否</span><span class="sxs-lookup"><span data-stu-id="6f5c7-168">No</span></span> | <span data-ttu-id="6f5c7-169">集合</span><span class="sxs-lookup"><span data-stu-id="6f5c7-169">Collection</span></span> | <span data-ttu-id="6f5c7-170">指定 Linux OS 的 SSH 金鑰組態</span><span class="sxs-lookup"><span data-stu-id="6f5c7-170">Specifies the SSH key configuration for a Linux OS</span></span>
<span data-ttu-id="6f5c7-171">路徑</span><span class="sxs-lookup"><span data-stu-id="6f5c7-171">path</span></span> | <span data-ttu-id="6f5c7-172">是</span><span class="sxs-lookup"><span data-stu-id="6f5c7-172">Yes</span></span> | <span data-ttu-id="6f5c7-173">String</span><span class="sxs-lookup"><span data-stu-id="6f5c7-173">String</span></span> | <span data-ttu-id="6f5c7-174">指定 SSH 金鑰或憑證必須位於的 Linux 檔案路徑</span><span class="sxs-lookup"><span data-stu-id="6f5c7-174">Specifies the Linux file path where the SSH keys or certificate should be located</span></span>
<span data-ttu-id="6f5c7-175">keyData</span><span class="sxs-lookup"><span data-stu-id="6f5c7-175">keyData</span></span> | <span data-ttu-id="6f5c7-176">是</span><span class="sxs-lookup"><span data-stu-id="6f5c7-176">Yes</span></span> | <span data-ttu-id="6f5c7-177">String</span><span class="sxs-lookup"><span data-stu-id="6f5c7-177">String</span></span> | <span data-ttu-id="6f5c7-178">指定 base64 編碼的 SSH 公開金鑰</span><span class="sxs-lookup"><span data-stu-id="6f5c7-178">Specifies a base64-encoded SSH public key</span></span>

<span data-ttu-id="6f5c7-179">如需範例，請參閱 [101-vm-sshkey GitHub 快速入門範本](https://github.com/Azure/azure-quickstart-templates/blob/master/101-vm-sshkey/azuredeploy.json)。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-179">For an example, see [the 101-vm-sshkey GitHub quick start template](https://github.com/Azure/azure-quickstart-templates/blob/master/101-vm-sshkey/azuredeploy.json).</span></span>

 
### <a name="when-i-run-update-azurermvmss-after-adding-more-than-one-certificate-from-the-same-key-vault-i-see-the-following-message"></a><span data-ttu-id="6f5c7-180">當我在從相同金鑰保存庫新增一個以上的憑證之後執行 `Update-AzureRmVmss` 時，我會看到下列錯誤︰</span><span class="sxs-lookup"><span data-stu-id="6f5c7-180">When I run `Update-AzureRmVmss` after adding more than one certificate from the same key vault, I see the following message:</span></span>
 
><span data-ttu-id="6f5c7-181">Update-AzureRmVmss: 清單密碼包含重複的 /subscriptions/<my-subscription-id>/resourceGroups/internal-rg-dev/providers/Microsoft.KeyVault/vaults/internal-keyvault-dev 執行個體，不允許這種情況。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-181">Update-AzureRmVmss: List secret contains repeated instances of /subscriptions/<my-subscription-id>/resourceGroups/internal-rg-dev/providers/Microsoft.KeyVault/vaults/internal-keyvault-dev, which is disallowed.</span></span>
 
<span data-ttu-id="6f5c7-182">如果您嘗試重新新增相同的保存庫，而不是對現有的來源保存庫使用新的保存庫憑證，就會發生這種情形。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-182">This can happen if you try to re-add the same vault instead of using a new vault certificate for the existing source vault.</span></span> <span data-ttu-id="6f5c7-183">如果您要新增其他密碼，`Add-AzureRmVmssSecret` 命令無法正常運作。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-183">The `Add-AzureRmVmssSecret` command does not work correctly if you are adding additional secrets.</span></span>
 
<span data-ttu-id="6f5c7-184">若要從相同金鑰保存庫新增更多密碼，請更新 $vmss.properties.osProfile.secrets[0].vaultCertificates 清單。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-184">To add more secrets from the same key vault, update the $vmss.properties.osProfile.secrets[0].vaultCertificates list.</span></span>
 
<span data-ttu-id="6f5c7-185">如需預期的輸入結構，請參閱[建立或更新虛擬機器擴展集](https://msdn.microsoft.com/library/azure/mt589035.aspx)。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-185">For the expected input structure, see [Create or update a virtual machine set](https://msdn.microsoft.com/library/azure/mt589035.aspx).</span></span>
 
<span data-ttu-id="6f5c7-186">在金鑰保存庫中的虛擬機器擴展集物件中尋找密碼。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-186">Find the secret in the virtual machine scale set object that is in the key vault.</span></span> <span data-ttu-id="6f5c7-187">然後，將憑證參考 (URL 及密碼存放區名稱) 新增至與保存庫相關聯的清單。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-187">Then, add your certificate reference (the URL and the secret store name) to the list associated with the vault.</span></span>

> [!NOTE] 
> <span data-ttu-id="6f5c7-188">目前，您無法使用虛擬機器擴展集 API 從 VM 中移除憑證。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-188">Currently, you cannot remove certificates from VMs by using the virtual machine scale set API.</span></span>
>

<span data-ttu-id="6f5c7-189">新的 VM 不會有舊的憑證。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-189">New VMs will not have the old certificate.</span></span> <span data-ttu-id="6f5c7-190">不過，具有憑證且已經部署的 VM 會有舊的憑證。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-190">However, VMs that have the certificate and which are already deployed will have the old certificate.</span></span>
 
### <a name="can-i-push-certificates-to-the-virtual-machine-scale-set-without-providing-the-password-when-the-certificate-is-in-the-secret-store"></a><span data-ttu-id="6f5c7-191">當憑證位於密碼存放區時，可以將憑證推送至虛擬機器擴展集而無須提供密碼？</span><span class="sxs-lookup"><span data-stu-id="6f5c7-191">Can I push certificates to the virtual machine scale set without providing the password, when the certificate is in the secret store?</span></span>

<span data-ttu-id="6f5c7-192">您不需要使用硬式編碼在指令碼中寫入密碼。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-192">You do not need to hard-code passwords in scripts.</span></span> <span data-ttu-id="6f5c7-193">您可以使用您用來執行部署指令碼的權限動態擷取密碼。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-193">You can dynamically retrieve passwords with the permissions you use to run the deployment script.</span></span> <span data-ttu-id="6f5c7-194">如果您的指令碼會從密碼存放區金鑰保存庫移動憑證，則密碼存放區 `get certificate` 命令也會輸出 pfx 檔案的密碼。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-194">If you have a script that moves a certificate from the secret store key vault, the secret store `get certificate` command also outputs the password of the .pfx file.</span></span>
 
### <a name="how-does-the-secrets-property-of-virtualmachineprofileosprofile-for-a-virtual-machine-scale-set-work-why-do-i-need-the-sourcevault-value-when-i-have-to-specify-the-absolute-uri-for-a-certificate-by-using-the-certificateurl-property"></a><span data-ttu-id="6f5c7-195">虛擬機器擴展集的 virtualMachineProfile.osProfile 的 Secrets 屬性如何運作？</span><span class="sxs-lookup"><span data-stu-id="6f5c7-195">How does the Secrets property of virtualMachineProfile.osProfile for a virtual machine scale set work?</span></span> <span data-ttu-id="6f5c7-196">當我必須使用 certificateUrl 屬性來指定憑證的絕對 URI 時，為什麼需要 sourceVault 值？</span><span class="sxs-lookup"><span data-stu-id="6f5c7-196">Why do I need the sourceVault value when I have to specify the absolute URI for a certificate by using the certificateUrl property?</span></span> 

<span data-ttu-id="6f5c7-197">必須在 OS 設定檔的 Secrets 屬性中顯示 Windows 遠端管理 (WinRM) 憑證參考。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-197">A Windows Remote Management (WinRM) certificate reference must be present in the Secrets property of the OS profile.</span></span> 

<span data-ttu-id="6f5c7-198">指出來源保存庫的目的是要強制執行使用者的 Azure 雲端服務模型中存在的存取控制清單 (ACL) 原則。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-198">The purpose of indicating the source vault is to enforce access control list (ACL) policies that exist in a user's Azure Cloud Service model.</span></span> <span data-ttu-id="6f5c7-199">如果未指定來源保存庫，則沒有權限可存取密碼或將密碼部署至金鑰保存庫的使用者便能夠透過計算資源提供者 (CRP)。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-199">If the source vault isn't specified, users who do not have permissions to deploy or access secrets to a key vault would be able to through a Compute Resource Provider (CRP).</span></span> <span data-ttu-id="6f5c7-200">甚至不存在的資源也會有 ACL。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-200">ACLs exist even for resources that do not exist.</span></span>

<span data-ttu-id="6f5c7-201">如果您提供不正確的來源保存庫識別碼，但為有效的金鑰保存庫 URL，則系統會在您輪詢作業時報告錯誤。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-201">If you provide an incorrect source vault ID but a valid key vault URL, an error is reported when you poll the operation.</span></span>
 
### <a name="if-i-add-secrets-to-an-existing-virtual-machine-scale-set-are-the-secrets-injected-into-existing-vms-or-only-into-new-ones"></a><span data-ttu-id="6f5c7-202">如果我將密碼新增至現有虛擬機器擴展集，則新的密碼會插入現有的 VM，或只會插入新的 VM？</span><span class="sxs-lookup"><span data-stu-id="6f5c7-202">If I add secrets to an existing virtual machine scale set, are the secrets injected into existing VMs, or only into new ones?</span></span> 

<span data-ttu-id="6f5c7-203">憑證會新增至所有 VM，甚至是既有的 VM。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-203">Certificates are added to all your VMs, even preexisting ones.</span></span> <span data-ttu-id="6f5c7-204">如果虛擬機器擴展集 upgradePolicy 屬性設定為 **manual**，當您在 VM 上執行手動更新時，憑證會新增至 VM。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-204">If your virtual machine scale set upgradePolicy property is set to **manual**, the certificate is added to the VM when you perform a manual update on the VM.</span></span>
 
### <a name="where-do-i-put-certificates-for-linux-vms"></a><span data-ttu-id="6f5c7-205">將 Linux VM 的憑證放在哪裡？</span><span class="sxs-lookup"><span data-stu-id="6f5c7-205">Where do I put certificates for Linux VMs?</span></span>

<span data-ttu-id="6f5c7-206">若要了解如何部署 Linux VM 的憑證，請參閱[將憑證從客戶管理的金鑰保存庫部署到 VM](https://blogs.technet.microsoft.com/kv/2015/07/14/deploy-certificates-to-vms-from-customer-managed-key-vault/)。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-206">To learn how to deploy certificates for Linux VMs, see [Deploy certificates to VMs from a customer-managed key vault](https://blogs.technet.microsoft.com/kv/2015/07/14/deploy-certificates-to-vms-from-customer-managed-key-vault/).</span></span>
  
### <a name="how-do-i-add-a-new-vault-certificate-to-a-new-certificate-object"></a><span data-ttu-id="6f5c7-207">如何將新的保存庫憑證新增至新的憑證物件？</span><span class="sxs-lookup"><span data-stu-id="6f5c7-207">How do I add a new vault certificate to a new certificate object?</span></span>

<span data-ttu-id="6f5c7-208">若要將保存庫憑證新增至現有的密碼，請參閱下列 PowerShell 範例。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-208">To add a vault certificate to an existing secret, see the following PowerShell example.</span></span> <span data-ttu-id="6f5c7-209">只使用一個密碼物件。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-209">Use only one secret object.</span></span>
 
```powershell
$newVaultCertificate = New-AzureRmVmssVaultCertificateConfig -CertificateStore MY -CertificateUrl https://sansunallapps1.vault.azure.net:443/secrets/dg-private-enc/55fa0332edc44a84ad655298905f1809
 
$vmss.VirtualMachineProfile.OsProfile.Secrets[0].VaultCertificates.Add($newVaultCertificate)
 
Update-AzureRmVmss -VirtualMachineScaleSet $vmss -ResourceGroup $rg -Name $vmssName
```
 
### <a name="what-happens-to-certificates-if-you-reimage-a-vm"></a><span data-ttu-id="6f5c7-210">如果您重新安裝映像 VM，憑證會發生什麼事？</span><span class="sxs-lookup"><span data-stu-id="6f5c7-210">What happens to certificates if you reimage a VM?</span></span>

<span data-ttu-id="6f5c7-211">如果您重新安裝 VM 映像，則會刪除憑證。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-211">If you reimage a VM, certificates are deleted.</span></span> <span data-ttu-id="6f5c7-212">重新安裝映像會刪除整個 OS 磁碟。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-212">Reimaging deletes the entire OS disk.</span></span> 
 
### <a name="what-happens-if-you-delete-a-certificate-from-the-key-vault"></a><span data-ttu-id="6f5c7-213">如果您從 Key Vault 中刪除憑證會發生什麼事？</span><span class="sxs-lookup"><span data-stu-id="6f5c7-213">What happens if you delete a certificate from the key vault?</span></span>

<span data-ttu-id="6f5c7-214">如果從金鑰保存庫中刪除密碼，然後您對所有 VM 執行 `stop deallocate` 而後再次啟動它們，您會發生失敗。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-214">If the secret is deleted from the key vault, and then you run `stop deallocate` for all your VMs and then start them again, you will encounter a failure.</span></span> <span data-ttu-id="6f5c7-215">發生失敗的原因是 CRP 需要從金鑰保存庫擷取密碼，但無法這麼做。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-215">The failure occurs because the CRP needs to retrieve the secrets from the key vault, but it cannot.</span></span> <span data-ttu-id="6f5c7-216">在此案例中，您可以從虛擬機器擴展集模型刪除憑證。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-216">In this scenario, you can delete the certificates from the virtual machine scale set model.</span></span> 

<span data-ttu-id="6f5c7-217">CRP 元件不會保存客戶密碼。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-217">The CRP component does not persist customer secrets.</span></span> <span data-ttu-id="6f5c7-218">如果您對虛擬機器擴展集中的所有 VM 執行 `stop deallocate`，則會刪除快取。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-218">If you run `stop deallocate` for all VMs in the virtual machine scale set, the cache is deleted.</span></span> <span data-ttu-id="6f5c7-219">在此案例中會從金鑰保存庫中擷取密碼。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-219">In this scenario, secrets are retrieved from the key vault.</span></span>

<span data-ttu-id="6f5c7-220">您不會在相應放大時遇到此問題，因為 Azure Service Fabric 中有一個快取的密碼副本 (在單一網狀架構租用戶模型中)。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-220">You don't encounter this problem when scaling out because there is a cached copy of the secret in Azure Service Fabric (in the single-fabric tenant model).</span></span>
 
### <a name="why-do-i-have-to-specify-the-exact-location-for-the-certificate-url-httpsname-of-the-vaultvaultazurenet443secretsexact-location-as-indicated-in-service-fabric-cluster-security-scenarioshttpsazuremicrosoftcomdocumentationarticlesservice-fabric-cluster-security"></a><span data-ttu-id="6f5c7-221">為什麼我必須指定憑證 URL 的確切位置 (https://<name of the vault>.vault.azure.net:443/secrets/<exact location>)，如 [Service Fabric 叢集安全性案例](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/)所示？</span><span class="sxs-lookup"><span data-stu-id="6f5c7-221">Why do I have to specify the exact location for the certificate URL (https://<name of the vault>.vault.azure.net:443/secrets/<exact location>), as indicated in [Service Fabric cluster security scenarios](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/)?</span></span>
 
<span data-ttu-id="6f5c7-222">Azure Key Vault 文件表示「取得密碼 REST API」應傳回最新版的密碼 (若未指定版本的話)。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-222">The Azure Key Vault documentation states that the Get Secret REST API should return the latest version of the secret if the version is not specified.</span></span>
 
<span data-ttu-id="6f5c7-223">方法</span><span class="sxs-lookup"><span data-stu-id="6f5c7-223">Method</span></span> | <span data-ttu-id="6f5c7-224">URL</span><span class="sxs-lookup"><span data-stu-id="6f5c7-224">URL</span></span>
--- | ---
<span data-ttu-id="6f5c7-225">GET</span><span class="sxs-lookup"><span data-stu-id="6f5c7-225">GET</span></span> | <span data-ttu-id="6f5c7-226">https://mykeyvault.vault.azure.net/secrets/{密碼-名稱}/{密碼-版本}?api-version={api-版本}</span><span class="sxs-lookup"><span data-stu-id="6f5c7-226">https://mykeyvault.vault.azure.net/secrets/{secret-name}/{secret-version}?api-version={api-version}</span></span>

<span data-ttu-id="6f5c7-227">將 {密碼-名稱} 替換為名稱，以及將 {密碼-版本} 替換為您想要擷取的密碼版本。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-227">Replace {*secret-name*} with the name, and replace {*secret-version*} with the version of the secret you want to retrieve.</span></span> <span data-ttu-id="6f5c7-228">可能會排除密碼版本。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-228">The secret version might be excluded.</span></span> <span data-ttu-id="6f5c7-229">在此情況下會擷取目前的版本。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-229">In that case, the current version is retrieved.</span></span>
  
### <a name="why-do-i-have-to-specify-the-certificate-version-when-i-use-key-vault"></a><span data-ttu-id="6f5c7-230">使用 Key Vault 時，為什麼必須指定憑證版本？</span><span class="sxs-lookup"><span data-stu-id="6f5c7-230">Why do I have to specify the certificate version when I use Key Vault?</span></span>

<span data-ttu-id="6f5c7-231">指定憑證版本的 Key Vault 需求目的是要讓使用者清楚了解其 VM 上所部署的憑證。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-231">The purpose of the Key Vault requirement to specify the certificate version is to make it clear to the user what certificate is deployed on their VMs.</span></span>

<span data-ttu-id="6f5c7-232">如果您建立 VM，然後更新金鑰保存庫中的密碼，新的憑證不會下載至您的 VM。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-232">If you create a VM and then update your secret in the key vault, the new certificate is not downloaded to your VMs.</span></span> <span data-ttu-id="6f5c7-233">但您的 VM 似乎會參考它，且新的 VM 會取得新的密碼。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-233">But your VMs appear to reference it, and new VMs get the new secret.</span></span> <span data-ttu-id="6f5c7-234">若要避免這個問題，您必須參考密碼版本。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-234">To avoid this, you are required to reference a secret version.</span></span>

### <a name="my-team-works-with-several-certificates-that-are-distributed-to-us-as-cer-public-keys-what-is-the-recommended-approach-for-deploying-these-certificates-to-a-virtual-machine-scale-set"></a><span data-ttu-id="6f5c7-235">我的小組會使用發佈給我們做為 .cer 公開金鑰的多個憑證。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-235">My team works with several certificates that are distributed to us as .cer public keys.</span></span> <span data-ttu-id="6f5c7-236">將這些憑證部署至虛擬機器擴展集的建議方法為何？</span><span class="sxs-lookup"><span data-stu-id="6f5c7-236">What is the recommended approach for deploying these certificates to a virtual machine scale set?</span></span>

<span data-ttu-id="6f5c7-237">若要將 .cer 公開金鑰部署至虛擬機器擴展集，您可以產生僅包含 .cer 檔案的 .pfx 檔案。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-237">To deploy .cer public keys to a virtual machine scale set, you can generate a .pfx file that contains only .cer files.</span></span> <span data-ttu-id="6f5c7-238">若要這樣做，請使用 `X509ContentType = Pfx`。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-238">To do this, use `X509ContentType = Pfx`.</span></span> <span data-ttu-id="6f5c7-239">例如，載入 .cer 檔案做為 C# 或 PowerShell 中的 x509Certificate2 物件，然後呼叫此方法。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-239">For example, load the .cer file as an x509Certificate2 object in C# or PowerShell, and then call the method.</span></span> 

<span data-ttu-id="6f5c7-240">如需詳細資訊，請參閱 [X509Certificate.Export 方法 (X509ContentType, String)](https://msdn.microsoft.com/library/24ww6yzk(v=vs.110.aspx))。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-240">For more information, see [X509Certificate.Export Method (X509ContentType, String)](https://msdn.microsoft.com/library/24ww6yzk(v=vs.110.aspx)).</span></span>

### <a name="i-do-not-see-an-option-for-users-to-pass-in-certificates-as-base64-strings-most-other-resource-providers-have-this-option"></a><span data-ttu-id="6f5c7-241">我看不到可供使用者傳入憑證做為 base64 字串的選項。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-241">I do not see an option for users to pass in certificates as base64 strings.</span></span> <span data-ttu-id="6f5c7-242">大部分其他資源提供者都有這個選項。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-242">Most other resource providers have this option.</span></span>

<span data-ttu-id="6f5c7-243">若要模擬傳入憑證做為 base64 字串，您可以在 Resource Manager 範本中擷取最新版的 URL。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-243">To emulate passing in a certificate as a base64 string, you can extract the latest versioned URL in a Resource Manager template.</span></span> <span data-ttu-id="6f5c7-244">在 Resource Manager 範本中包含下列 JSON 屬性︰</span><span class="sxs-lookup"><span data-stu-id="6f5c7-244">Include the following JSON property in your Resource Manager template:</span></span>

```json 
"certificateUrl": "[reference(resourceId(parameters('vaultResourceGroup'), 'Microsoft.KeyVault/vaults/secrets', parameters('vaultName'), parameters('secretName')), '2015-06-01').secretUriWithVersion]"
```
 
### <a name="do-i-have-to-wrap-certificates-in-json-objects-in-key-vaults"></a><span data-ttu-id="6f5c7-245">我們必須在金鑰保存庫的 JSON 物件中包裝憑證嗎？</span><span class="sxs-lookup"><span data-stu-id="6f5c7-245">Do I have to wrap certificates in JSON objects in key vaults?</span></span>

<span data-ttu-id="6f5c7-246">在虛擬機器擴展集和 VM 中，憑證必須包裝在 JSON 物件中。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-246">In virtual machine scale sets and VMs, certificates must be wrapped in JSON objects.</span></span> 

<span data-ttu-id="6f5c7-247">我們也支援內容類型 application/x-pkcs12。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-247">We also support the content type application/x-pkcs12.</span></span> <span data-ttu-id="6f5c7-248">如需使用 application/x-pkcs12 的相關指示，請參閱 [Azure Key Vault 中的 PFX 憑證](http://www.rahulpnath.com/blog/pfx-certificate-in-azure-key-vault/)。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-248">For instructions on using application/x-pkcs12, see [PFX certificates in Azure Key Vault](http://www.rahulpnath.com/blog/pfx-certificate-in-azure-key-vault/).</span></span>
 
<span data-ttu-id="6f5c7-249">我們目前不支援 .cer 檔案。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-249">We currently do not support .cer files.</span></span> <span data-ttu-id="6f5c7-250">若要使用 .cer 檔案，請將它們匯出到 .pfx 容器。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-250">To use .cer files, export them into .pfx containers.</span></span>



## <a name="compliance"></a><span data-ttu-id="6f5c7-251">法規遵循</span><span class="sxs-lookup"><span data-stu-id="6f5c7-251">Compliance</span></span>

### <a name="are-virtual-machine-scale-sets-pci-compliant"></a><span data-ttu-id="6f5c7-252">虛擬機器擴展集符合 PCI 規範嗎？</span><span class="sxs-lookup"><span data-stu-id="6f5c7-252">Are virtual machine scale sets PCI-compliant?</span></span>

<span data-ttu-id="6f5c7-253">虛擬機器擴展集是以 CRP 為基礎的精簡 API 層。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-253">Virtual machine scale sets are a thin API layer on top of the CRP.</span></span> <span data-ttu-id="6f5c7-254">這兩個元件都在 Azure 服務樹狀目錄中計算平台的一部分。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-254">Both components are part of the compute platform in the Azure service tree.</span></span>

<span data-ttu-id="6f5c7-255">就相容性的觀點而言，虛擬機器擴展集是 Azure 計算平台的基本部分。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-255">From a compliance perspective, virtual machine scale sets are a fundamental part of the Azure compute platform.</span></span> <span data-ttu-id="6f5c7-256">它們會與 CRP 本身共用一個小組、工具、程序、部署方法、安全性控制、Just-In-Time (JIT) 編譯、監控、警示等。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-256">They share a team, tools, processes, deployment methodology, security controls, just-in-time (JIT) compilation, monitoring, alerting, and so on, with the CRP itself.</span></span> <span data-ttu-id="6f5c7-257">虛擬機器擴展集符合支付卡產業 (PCI) 規範，因為 CRP 是目前 PCI 資料安全標準 (DSS) 證明的一部分。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-257">Virtual machine scale sets are Payment Card Industry (PCI)-compliant because the CRP is part of the current PCI Data Security Standard (DSS) attestation.</span></span>

<span data-ttu-id="6f5c7-258">如需詳細資訊，請參閱 [Microsoft 信任中心](https://www.microsoft.com/TrustCenter/Compliance/PCI)。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-258">For more information, see [the Microsoft Trust Center](https://www.microsoft.com/TrustCenter/Compliance/PCI).</span></span>






## <a name="extensions"></a><span data-ttu-id="6f5c7-259">擴充功能</span><span class="sxs-lookup"><span data-stu-id="6f5c7-259">Extensions</span></span>

### <a name="how-do-i-delete-a-virtual-machine-scale-set-extension"></a><span data-ttu-id="6f5c7-260">如何刪除虛擬機器擴展集擴充功能？</span><span class="sxs-lookup"><span data-stu-id="6f5c7-260">How do I delete a virtual machine scale set extension?</span></span>

<span data-ttu-id="6f5c7-261">若要刪除虛擬機器擴展集擴充功能，請使用下列 PowerShell 範例︰</span><span class="sxs-lookup"><span data-stu-id="6f5c7-261">To delete a virtual machine scale set extension, use the following PowerShell example:</span></span>

```powershell
$vmss = Get-AzureRmVmss -ResourceGroupName "resource_group_name" -VMScaleSetName "vmssName" 

$vmss=Remove-AzureRmVmssExtension -VirtualMachineScaleSet $vmss -Name "extensionName"

Update-AzureRmVmss -ResourceGroupName "resource_group_name" -VMScaleSetName "vmssName" -VirtualMacineScaleSet $vmss
```
 
<span data-ttu-id="6f5c7-262">您可以在 `$vmss` 中找到 extensionName 值。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-262">You can find the extensionName value in `$vmss`.</span></span>
   
### <a name="is-there-a-virtual-machine-scale-set-template-example-that-integrates-with-operations-management-suite"></a><span data-ttu-id="6f5c7-263">是否有與 Operations Management Suite 整合的虛擬機器擴展集範本範例？</span><span class="sxs-lookup"><span data-stu-id="6f5c7-263">Is there a virtual machine scale set template example that integrates with Operations Management Suite?</span></span>

<span data-ttu-id="6f5c7-264">如需與 Operations Management Suite 整合的虛擬機器擴展集範本範例，請參閱[部署 Azure Service Fabric 叢集並使用 Log Analytics 來啟用監視](https://github.com/krnese/AzureDeploy/tree/master/OMS/MSOMS/ServiceFabric)中的第二個範例。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-264">For a virtual machine scale set template example that integrates with Operations Management Suite, see the second example in [Deploy an Azure Service Fabric cluster and enable monitoring by using Log Analytics](https://github.com/krnese/AzureDeploy/tree/master/OMS/MSOMS/ServiceFabric).</span></span>
   
### <a name="extensions-seem-to-run-in-parallel-on-virtual-machine-scale-sets-this-causes-my-custom-script-extension-to-fail-what-can-i-do-to-fix-this"></a><span data-ttu-id="6f5c7-265">擴充功能似乎會在虛擬機器擴展集上平行執行。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-265">Extensions seem to run in parallel on virtual machine scale sets.</span></span> <span data-ttu-id="6f5c7-266">這會導致自訂指令碼擴充功能失敗。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-266">This causes my custom script extension to fail.</span></span> <span data-ttu-id="6f5c7-267">可以做什麼來修正這個問題？</span><span class="sxs-lookup"><span data-stu-id="6f5c7-267">What can I do to fix this?</span></span>

<span data-ttu-id="6f5c7-268">若要了解虛擬機器擴展集中的擴充功能排序，請參閱 [Azure 虛擬機器擴展集中的擴充功能排序](https://msftstack.wordpress.com/2016/05/12/extension-sequencing-in-azure-vm-scale-sets/)。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-268">To learn about extension sequencing in virtual machine scale sets, see [Extension sequencing in Azure virtual machine scale sets](https://msftstack.wordpress.com/2016/05/12/extension-sequencing-in-azure-vm-scale-sets/).</span></span>
 
 
### <a name="how-do-i-reset-the-password-for-vms-in-my-virtual-machine-scale-set"></a><span data-ttu-id="6f5c7-269">如何重設虛擬機器擴展集中 VM 的密碼？</span><span class="sxs-lookup"><span data-stu-id="6f5c7-269">How do I reset the password for VMs in my virtual machine scale set?</span></span>

<span data-ttu-id="6f5c7-270">若要重設虛擬機器擴展集中 VM 的密碼，請使用 VM 存取擴充功能。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-270">To reset the password for VMs in your virtual machine scale set, use VM access extensions.</span></span> 

<span data-ttu-id="6f5c7-271">使用下列 PowerShell 範例：</span><span class="sxs-lookup"><span data-stu-id="6f5c7-271">Use the following PowerShell example:</span></span>

```powershell
$vmssName = "myvmss"
$vmssResourceGroup = "myvmssrg"
$publicConfig = @{"UserName" = "newuser"}
$privateConfig = @{"Password" = "********"}
 
$extName = "VMAccessAgent"
$publisher = "Microsoft.Compute"
$vmss = Get-AzureRmVmss -ResourceGroupName $vmssResourceGroup -VMScaleSetName $vmssName
$vmss = Add-AzureRmVmssExtension -VirtualMachineScaleSet $vmss -Name $extName -Publisher $publisher -Setting $publicConfig -ProtectedSetting $privateConfig -Type $extName -TypeHandlerVersion "2.0" -AutoUpgradeMinorVersion $true
Update-AzureRmVmss -ResourceGroupName $vmssResourceGroup -Name $vmssName -VirtualMachineScaleSet $vmss
```
 
 
### <a name="how-do-i-add-an-extension-to-all-vms-in-my-virtual-machine-scale-set"></a><span data-ttu-id="6f5c7-272">如何將擴充功能新增至虛擬機器擴展集中的所有 VM？</span><span class="sxs-lookup"><span data-stu-id="6f5c7-272">How do I add an extension to all VMs in my virtual machine scale set?</span></span>

<span data-ttu-id="6f5c7-273">將更新原則設定為**自動**時，使用新的擴充屬性重新部署範本便會更新所有 VM。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-273">If update policy is set to **automatic**, redeploying the template with the new extension properties updates all VMs.</span></span>

<span data-ttu-id="6f5c7-274">如果更新原則設定為**手動**，請先更新擴充功能，然後手動更新 VM 中的所有執行個體。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-274">If update policy is set to **manual**, first update the extension, and then manually update all instances in your VMs.</span></span>

  
### <a name="if-the-extensions-associated-with-an-existing-virtual-machine-scale-set-are-updated-are-existing-vms-affected-that-is-will-the-vms-not-match-the-virtual-machine-scale-set-model-or-are-they-ignored-when-an-existing-machine-is-service-healed-or-reimaged-are-the-scripts-that-are-currently-configured-on-the-virtual-machine-scale-set-executed-or-are-the-scripts-that-were-configured-when-the-vm-was-first-created-used"></a><span data-ttu-id="6f5c7-275">如果更新與現有虛擬機器擴展集相關聯的擴充功能，現有的 VM 是否會受影響？</span><span class="sxs-lookup"><span data-stu-id="6f5c7-275">If the extensions associated with an existing virtual machine scale set are updated, are existing VMs affected?</span></span> <span data-ttu-id="6f5c7-276">(也就是，VM「不」符合虛擬機器擴展集模型嗎？)或者會忽略它們？</span><span class="sxs-lookup"><span data-stu-id="6f5c7-276">(That is, will the VMs *not* match the virtual machine scale set model?) Or are they ignored?</span></span> <span data-ttu-id="6f5c7-277">當現有機器為服務所修復或重新安裝映像時，是否會執行目前在虛擬機器擴展集上設定的指令碼，或是否會使用第一次建立 VM 時設定的指令？</span><span class="sxs-lookup"><span data-stu-id="6f5c7-277">When an existing machine is service-healed or reimaged, are the scripts that are currently configured on the virtual machine scale set executed, or are the scripts that were configured when the VM was first created used?</span></span>

<span data-ttu-id="6f5c7-278">如果已更新虛擬機器擴展集模型中的擴充定義且 upgradePolicy 屬性設定為 **automatic**，則會更新 VM。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-278">If the extension definition in the virtual machine scale set model is updated and the upgradePolicy property is set to **automatic**, it updates the VMs.</span></span> <span data-ttu-id="6f5c7-279">如果 upgradePolicy 屬性設定為 **manual**，則會將擴充功能標示為不符合模型。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-279">If the upgradePolicy property is set to **manual**, extensions are flagged as not matching the model.</span></span> 

<span data-ttu-id="6f5c7-280">如果現有 VM 為服務所修復，它會呈現重新開機狀態，且不會重新執行擴充功能。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-280">If an existing VM is service-healed, it appears as a reboot, and the extensions are not rerun.</span></span> <span data-ttu-id="6f5c7-281">若已重新安裝映像，就像是以來源映像取代 OS 磁碟機。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-281">If it is reimaged, it's like replacing the OS drive with the source image.</span></span> <span data-ttu-id="6f5c7-282">系統會執行最新模型的任何特製化項目，例如擴充功能。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-282">Any specialization from the latest model, such as extensions, are run.</span></span>
 
### <a name="how-do-i-join-a-virtual-machine-scale-set-to-an-azure-ad-domain"></a><span data-ttu-id="6f5c7-283">如何將虛擬機器擴展集加入至 Azure AD 網域？</span><span class="sxs-lookup"><span data-stu-id="6f5c7-283">How do I join a virtual machine scale set to an Azure AD domain?</span></span>

<span data-ttu-id="6f5c7-284">若要將虛擬機器擴展集加入至 Azure Active Directory (Azure AD) 網域，您可以定義擴充功能。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-284">To join a virtual machine scale set to an Azure Active Directory (Azure AD) domain, you can define an extension.</span></span> 

<span data-ttu-id="6f5c7-285">若要定義擴充功能，請使用 JsonADDomainExtension 屬性︰</span><span class="sxs-lookup"><span data-stu-id="6f5c7-285">To define an extension, use the JsonADDomainExtension property:</span></span>

```json
"extensionProfile": {
    "extensions": [
        {
            "name": "joindomain",
            "properties": {
                "publisher": "Microsoft.Compute",
                "type": "JsonADDomainExtension",
                "typeHandlerVersion": "1.3",
                "settings": {
                    "Name": "[parameters('domainName')]",
                    "OUPath": "[variables('ouPath')]",
                    "User": "[variables('domainAndUsername')]",
                    "Restart": "true",
                    "Options": "[variables('domainJoinOptions')]"
                },
                "protectedsettings": {
                    "Password": "[parameters('domainJoinPassword')]"
                }
            }
        }
    ]
}
```
 
### <a name="my-virtual-machine-scale-set-extension-is-trying-to-install-something-that-requires-a-reboot-for-example-commandtoexecute-powershellexe--executionpolicy-unrestricted-install-windowsfeature-name-fs-resource-manager-includemanagementtools"></a><span data-ttu-id="6f5c7-286">我的虛擬機器擴展集擴充功能正嘗試安裝需要重新開機的項目。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-286">My virtual machine scale set extension is trying to install something that requires a reboot.</span></span> <span data-ttu-id="6f5c7-287">例如："commandToExecute": "powershell.exe -ExecutionPolicy Unrestricted Install-WindowsFeature –Name FS-Resource-Manager –IncludeManagementTools"</span><span class="sxs-lookup"><span data-stu-id="6f5c7-287">For example, "commandToExecute": "powershell.exe -ExecutionPolicy Unrestricted Install-WindowsFeature –Name FS-Resource-Manager –IncludeManagementTools"</span></span>

<span data-ttu-id="6f5c7-288">如果虛擬機器擴展集擴充功能正嘗試安裝需要重新開機的項目，您可以使用 Azure 自動化預期狀態設定 (自動化 DSC) 擴充功能。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-288">If your virtual machine scale set extension is trying to install something that requires a reboot, you can use the Azure Automation Desired State Configuration (Automation DSC) extension.</span></span> <span data-ttu-id="6f5c7-289">如果作業系統是 Windows Server 2012 R2，Azure 會提取 Windows Management Framework (WMF) 5.0 安裝程式，重新開機，然後繼續進行設定。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-289">If the operating system is Windows Server 2012 R2, Azure pulls in the Windows Management Framework (WMF) 5.0 setup, reboots, and then continues with the configuration.</span></span> 
 
### <a name="how-do-i-turn-on-antimalware-in-my-virtual-machine-scale-set"></a><span data-ttu-id="6f5c7-290">如何在虛擬機器擴展集中開啟反惡意程式碼？</span><span class="sxs-lookup"><span data-stu-id="6f5c7-290">How do I turn on antimalware in my virtual machine scale set?</span></span>

<span data-ttu-id="6f5c7-291">若要在虛擬機器擴展集上開啟反惡意程式碼，請使用下列 PowerShell 範例︰</span><span class="sxs-lookup"><span data-stu-id="6f5c7-291">To turn on antimalware on your virtual machine scale set, use the following PowerShell example:</span></span>

```powershell
$rgname = 'autolap'
$vmssname = 'autolapbr'
$location = 'eastus'
 
# Retrieve the most recent version number of the extension.
$allVersions= (Get-AzureRmVMExtensionImage -Location $location -PublisherName "Microsoft.Azure.Security" -Type "IaaSAntimalware").Version
$versionString = $allVersions[($allVersions.count)-1].Split(".")[0] + "." + $allVersions[($allVersions.count)-1].Split(".")[1]
 
$VMSS = Get-AzureRmVmss -ResourceGroupName $rgname -VMScaleSetName $vmssname
echo $VMSS
Add-AzureRmVmssExtension -VirtualMachineScaleSet $VMSS -Name "IaaSAntimalware" -Publisher "Microsoft.Azure.Security" -Type "IaaSAntimalware" -TypeHandlerVersion $versionString
Update-AzureRmVmss -ResourceGroupName $rgname -Name $vmssname -VirtualMachineScaleSet $VMSS 
```

### <a name="i-need-to-execute-a-custom-script-thats-hosted-in-a-private-storage-account-the-script-runs-successfully-when-the-storage-is-public-but-when-i-try-to-use-a-shared-access-signature-sas-it-fails-this-message-is-displayed-missing-mandatory-parameters-for-valid-shared-access-signature-linksas-works-fine-from-my-local-browser"></a><span data-ttu-id="6f5c7-292">我需要執行裝載於私人儲存體帳戶的自訂指令碼。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-292">I need to execute a custom script that's hosted in a private storage account.</span></span> <span data-ttu-id="6f5c7-293">當儲存體為公用儲存體時，指令碼會執行成功，但是當我嘗試使用共用存取簽章 (SAS) 時，它就會失敗。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-293">The script runs successfully when the storage is public, but when I try to use a Shared Access Signature (SAS), it fails.</span></span> <span data-ttu-id="6f5c7-294">隨即顯示此訊息：「遺漏有效的共用存取簽章的強制參數」。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-294">This message is displayed: “Missing mandatory parameters for valid Shared Access Signature”.</span></span> <span data-ttu-id="6f5c7-295">Link+SAS 可從我的本機瀏覽器正常運作。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-295">Link+SAS works fine from my local browser.</span></span>

<span data-ttu-id="6f5c7-296">若要執行裝載於私人儲存體帳戶的自訂指令碼，請使用儲存體帳戶金鑰和名稱來進行受保護的設定。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-296">To execute a custom script that's hosted in a private storage account, set up protected settings with the storage account key and name.</span></span> <span data-ttu-id="6f5c7-297">如需詳細資訊，請參閱[適用於 Windows 的自訂指令碼擴充功能](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-extensions-customscript/#template-example-for-a-windows-vm-with-protected-settings)。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-297">For more information, see [Custom Script Extension for Windows](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-extensions-customscript/#template-example-for-a-windows-vm-with-protected-settings).</span></span>







## <a name="networking"></a><span data-ttu-id="6f5c7-298">網路</span><span class="sxs-lookup"><span data-stu-id="6f5c7-298">Networking</span></span>
 
### <a name="is-it-possible-to-assign-a-network-security-group-nsg-to-a-scale-set-so-that-it-will-apply-to-all-the-vm-nics-in-the-set"></a><span data-ttu-id="6f5c7-299">是否可以將「網路安全性群組」(NSG) 指派給擴展集，以便將它套用至擴展集中的所有 VM NIC？</span><span class="sxs-lookup"><span data-stu-id="6f5c7-299">Is it possible to assign a Network Security Group (NSG) to a scale set, so that it will apply to all the VM NICs in the set?</span></span>

<span data-ttu-id="6f5c7-300">是。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-300">Yes.</span></span> <span data-ttu-id="6f5c7-301">您可以透過在網路設定檔的 networkInterfaceConfigurations 區段中參考「網路安全性群組」，將它直接套用至擴展集。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-301">A Network Security Group can be applied directly to a scale set by referencing it in the networkInterfaceConfigurations section of the network profile.</span></span> <span data-ttu-id="6f5c7-302">範例：</span><span class="sxs-lookup"><span data-stu-id="6f5c7-302">Example:</span></span>

```json
"networkProfile": {
    "networkInterfaceConfigurations": [
        {
            "name": "nic1",
            "properties": {
                "primary": "true",
                "ipConfigurations": [
                    {
                        "name": "ip1",
                        "properties": {
                            "subnet": {
                                "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/virtualNetworks/', variables('vnetName'), '/subnets/subnet1')]"
                            }
                "loadBalancerInboundNatPools": [
                                {
                                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/inboundNatPools/natPool1')]"
                                }
                            ],
                            "loadBalancerBackendAddressPools": [
                                {
                                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/backendAddressPools/addressPool1')]"
                                 }
                            ]
                        }
                    }
                ],
                "networkSecurityGroup": {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/networkSecurityGroups/', variables('nsgName'))]"
                }
            }
        }
    ]
}
```

### <a name="how-do-i-do-a-vip-swap-for-virtual-machine-scale-sets-in-the-same-subscription-and-same-region"></a><span data-ttu-id="6f5c7-303">如何在相同訂用帳戶和相同區域中進行虛擬機器擴展集的 VIP 交換？</span><span class="sxs-lookup"><span data-stu-id="6f5c7-303">How do I do a VIP swap for virtual machine scale sets in the same subscription and same region?</span></span>

<span data-ttu-id="6f5c7-304">如果您擁有兩個含 Azure Load Balancer 前端的虛擬機器擴展集，而且它們位於相同的訂用帳戶和區域，則您可以解除配置每個擴展集的公用 IP 位址，並指派給另一個。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-304">If you have two virtual machine scale sets with Azure Load Balancer front-ends, and they are in the same subscription and region, you could deallocate the public IP addresses from each one, and assign to the other.</span></span> <span data-ttu-id="6f5c7-305">例如，請參閱 [VIP 交換：Azure Resource Manager 中藍綠色版本部署](https://msftstack.wordpress.com/2017/02/24/vip-swap-blue-green-deployment-in-azure-resource-manager/) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-305">See [VIP Swap: Blue-green deployment in Azure Resource Manager](https://msftstack.wordpress.com/2017/02/24/vip-swap-blue-green-deployment-in-azure-resource-manager/) for example.</span></span> <span data-ttu-id="6f5c7-306">這確實意味著在網路層級取消配置/配置資源時會產生延遲。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-306">This does imply a delay though as the resources are deallocated/allocated at the network level.</span></span> <span data-ttu-id="6f5c7-307">更快的選項是搭配兩個後端集區和一個路由規則來使用 Azure 應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-307">A faster option is to use Azure Application Gateway with two backend pools, and a routing rule.</span></span> <span data-ttu-id="6f5c7-308">或者，您可以透過 [Azure App Service](https://azure.microsoft.com/en-us/services/app-service/) 裝載應用程式，以提供在預備與生產位置之間快速切換的支援。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-308">Alternatively, you could host your application with [Azure App service](https://azure.microsoft.com/en-us/services/app-service/) which provides support for fast switching between staging and production slots.</span></span>
 
### <a name="how-do-i-specify-a-range-of-private-ip-addresses-to-use-for-static-private-ip-address-allocation"></a><span data-ttu-id="6f5c7-309">如何指定要用於靜態私人 IP 位址配置的私人 IP 位址範圍？</span><span class="sxs-lookup"><span data-stu-id="6f5c7-309">How do I specify a range of private IP addresses to use for static private IP address allocation?</span></span>

<span data-ttu-id="6f5c7-310">系統會從您指定的子網路選取 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-310">IP addresses are selected from a subnet that you specify.</span></span> 

<span data-ttu-id="6f5c7-311">虛擬機器擴展集 IP 位址的配置方法永遠是「動態」的，但這並不表示可以變更這些 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-311">The allocation method of virtual machine scale set IP addresses is always “dynamic,” but that doesn't mean that these IP addresses can change.</span></span> <span data-ttu-id="6f5c7-312">在此情況下，「動態」只表示您不會在 PUT 要求中指定 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-312">In this case, "dynamic" only means that you do not specify the IP address in a PUT request.</span></span> <span data-ttu-id="6f5c7-313">使用子網路指定靜態設定。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-313">Specify the static set by using the subnet.</span></span> 
    
### <a name="how-do-i-deploy-a-virtual-machine-scale-set-to-an-existing-azure-virtual-network"></a><span data-ttu-id="6f5c7-314">如何將虛擬機器擴展集部署至現有的 Azure 虛擬網路？</span><span class="sxs-lookup"><span data-stu-id="6f5c7-314">How do I deploy a virtual machine scale set to an existing Azure virtual network?</span></span> 

<span data-ttu-id="6f5c7-315">若要將虛擬機器擴展集部署至現有的 Azure 虛擬網路，請參閱[將虛擬機器擴展集部署至現有的虛擬網路](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-existing-vnet)。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-315">To deploy a virtual machine scale set to an existing Azure virtual network, see [Deploy a virtual machine scale set to an existing virtual network](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-existing-vnet).</span></span> 

### <a name="how-do-i-add-the-ip-address-of-the-first-vm-in-a-virtual-machine-scale-set-to-the-output-of-a-template"></a><span data-ttu-id="6f5c7-316">如何將虛擬機器擴展集中第一個 VM 的 IP 位址新增至範本的輸出？</span><span class="sxs-lookup"><span data-stu-id="6f5c7-316">How do I add the IP address of the first VM in a virtual machine scale set to the output of a template?</span></span>

<span data-ttu-id="6f5c7-317">若要將虛擬機器擴展集中第一個 VM 的 IP 位址新增至範本的輸出，請參閱 [ARM︰取得 VMSS 的私人 IP](http://stackoverflow.com/questions/42790392/arm-get-vmsss-private-ips)。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-317">To add the IP address of the first VM in a virtual machine scale set to the output of a template, see [ARM: Get VMSS's private IPs](http://stackoverflow.com/questions/42790392/arm-get-vmsss-private-ips).</span></span>

### <a name="can-i-use-scale-sets-with-accelerated-networking"></a><span data-ttu-id="6f5c7-318">我可以搭配加速的網路使用擴展集嗎？</span><span class="sxs-lookup"><span data-stu-id="6f5c7-318">Can I use scale sets with Accelerated Networking?</span></span>

<span data-ttu-id="6f5c7-319">是。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-319">Yes.</span></span> <span data-ttu-id="6f5c7-320">若要使用加速的網路，請在擴展集的 networkInterfaceConfigurations 設定中，將enableAcceleratedNetworking 設為 true。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-320">To use accelerated networking, set enableAcceleratedNetworking to true in your scale set's networkInterfaceConfigurations settings.</span></span> <span data-ttu-id="6f5c7-321">例如</span><span class="sxs-lookup"><span data-stu-id="6f5c7-321">E.g.</span></span>
```json
"networkProfile": {
    "networkInterfaceConfigurations": [
    {
        "name": "niconfig1",
        "properties": {
        "primary": true,
        "enableAcceleratedNetworking" : true,
        "ipConfigurations": [
                ]
            }
            }
        ]
        }
    }
    ]
}
```

### <a name="how-can-i-configure-the-dns-servers-used-by-a-scale-set"></a><span data-ttu-id="6f5c7-322">如何設定擴展集所使用的 DNS 伺服器？</span><span class="sxs-lookup"><span data-stu-id="6f5c7-322">How can I configure the DNS servers used by a scale set?</span></span>

<span data-ttu-id="6f5c7-323">若要建立含自訂 DNS 設定的 VM 擴展集，請將 dnsSettings JSON 封包加入至擴展集 networkInterfaceConfigurations 區段。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-323">To create a VM scale set with a custom DNS configuration, add a dnsSettings JSON packet to the scale set networkInterfaceConfigurations section.</span></span> <span data-ttu-id="6f5c7-324">範例：</span><span class="sxs-lookup"><span data-stu-id="6f5c7-324">Example:</span></span>
```json
    "dnsSettings":{
        "dnsServers":["10.0.0.6", "10.0.0.5"]
    }
```

### <a name="how-can-i-configure-a-scale-set-to-assign-a-public-ip-address-to-each-vm"></a><span data-ttu-id="6f5c7-325">如何設定擴展集以將公用 IP 位址指派給每部 VM？</span><span class="sxs-lookup"><span data-stu-id="6f5c7-325">How can I configure a scale set to assign a public IP address to each VM?</span></span>

<span data-ttu-id="6f5c7-326">若要建立 VM 擴展集以將公用 IP 位址指派給每部 VM，請確定 Microsoft.Compute/virtualMAchineScaleSets 資源的 API 版本為 2017-03-30，並將 _publicipaddressconfiguration_ JSON 封包加入至擴展集 ipConfigurations 區段。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-326">To create a VM scale set that assigns a public IP address to each VM, make sure the API version of the Microsoft.Compute/virtualMAchineScaleSets resource is 2017-03-30, and add a _publicipaddressconfiguration_ JSON packet to the scale set ipConfigurations section.</span></span> <span data-ttu-id="6f5c7-327">範例：</span><span class="sxs-lookup"><span data-stu-id="6f5c7-327">Example:</span></span>

```json
    "publicipaddressconfiguration": {
        "name": "pub1",
        "properties": {
        "idleTimeoutInMinutes": 15
        }
    }
```

### <a name="can-i-configure-a-scale-set-to-work-with-multiple-application-gateways"></a><span data-ttu-id="6f5c7-328">我可以設定擴展集以搭配多個應用程式閘道使用嗎？</span><span class="sxs-lookup"><span data-stu-id="6f5c7-328">Can I configure a scale set to work with multiple Application Gateways?</span></span>

<span data-ttu-id="6f5c7-329">是。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-329">Yes.</span></span> <span data-ttu-id="6f5c7-330">您可以將多個應用程式閘道後端位址集區的資源識別碼新增至擴展集網路設定檔之 _ipConfigurations_ 區段中的 _applicationGatewayBackendAddressPools_ 清單。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-330">You can add the resource id's for multiple Application Gateway backend address pools to the _applicationGatewayBackendAddressPools_ list in the _ipConfigurations_ section of your scale set network profile.</span></span>

## <a name="scale"></a><span data-ttu-id="6f5c7-331">調整</span><span class="sxs-lookup"><span data-stu-id="6f5c7-331">Scale</span></span>

### <a name="in-what-case-would-i-create-a-virtual-machine-scale-set-with-fewer-than-two-vms"></a><span data-ttu-id="6f5c7-332">在何種情況下，我會建立具有兩部以下 VM 的虛擬機器擴展集？</span><span class="sxs-lookup"><span data-stu-id="6f5c7-332">In what case would I create a virtual machine scale set with fewer than two VMs?</span></span>

<span data-ttu-id="6f5c7-333">建立具有兩部以下 VM 的虛擬機器擴展集的原因之一，就是要使用虛擬機器擴展集的彈性屬性。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-333">One reason to create a virtual machine scale set with fewer than two VMs would be to use the elastic properties of a virtual machine scale set.</span></span> <span data-ttu-id="6f5c7-334">例如，您可部署沒有任何 VM 的虛擬機器擴展集來定義您的基礎結構，而不必支付 VM 執行成本。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-334">For example, you could deploy a virtual machine scale set with zero VMs to define your infrastructure without paying VM running costs.</span></span> <span data-ttu-id="6f5c7-335">然後，當您準備好要部署 VM 時，將虛擬機器擴展集的「容量」增加至生產執行個體計數。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-335">Then, when you are ready to deploy VMs, increase the “capacity” of the virtual machine scale set to the production instance count.</span></span>

<span data-ttu-id="6f5c7-336">建立具有兩部以下 VM 的虛擬機器擴展集的另一個原因，就是相較於使用具有離散 VM 的可用性設定組，您可能比較不擔心可用性。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-336">Another reason you might create a virtual machine scale set with fewer than two VMs is if you're concerned less with availability than in using an availability set with discrete VMs.</span></span> <span data-ttu-id="6f5c7-337">虛擬機器擴展集讓您能夠使用可取代的無差異計算單位。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-337">Virtual machine scale sets give you a way to work with undifferentiated compute units that are fungible.</span></span> <span data-ttu-id="6f5c7-338">此種一致性是虛擬機器擴展集與可用性設定組的關鍵區別指標。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-338">This uniformity is a key differentiator for virtual machine scale sets versus availability sets.</span></span> <span data-ttu-id="6f5c7-339">許多無狀態的工作負載都不會追蹤個別的單位。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-339">Many stateless workloads do not track individual units.</span></span> <span data-ttu-id="6f5c7-340">如果工作負載減少，您可以相應減少為一個計算單位，然後在工作負載增加時相應增加為許多計算單位。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-340">If the workload drops, you can scale down to one compute unit, and then scale up to many when the workload increases.</span></span>

### <a name="how-do-i-change-the-number-of-vms-in-a-virtual-machine-scale-set"></a><span data-ttu-id="6f5c7-341">如何變更虛擬機器擴展集中的 VM 數目？</span><span class="sxs-lookup"><span data-stu-id="6f5c7-341">How do I change the number of VMs in a virtual machine scale set?</span></span>

<span data-ttu-id="6f5c7-342">若要變更虛擬機器擴展集中的 VM 數目，請參閱[變更虛擬機器擴展集的執行個體計數](https://msftstack.wordpress.com/2016/05/13/change-the-instance-count-of-an-azure-vm-scale-set/)。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-342">To change the number of VMs in a virtual machine scale set, see [Change the instance count of a virtual machine scale set](https://msftstack.wordpress.com/2016/05/13/change-the-instance-count-of-an-azure-vm-scale-set/).</span></span>

### <a name="how-do-i-define-custom-alerts-for-when-certain-thresholds-are-reached"></a><span data-ttu-id="6f5c7-343">如何定義觸達特定臨界值時的自訂警示？</span><span class="sxs-lookup"><span data-stu-id="6f5c7-343">How do I define custom alerts for when certain thresholds are reached?</span></span>

<span data-ttu-id="6f5c7-344">您在處理指定之臨界值的警示時有一些彈性。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-344">You have some flexibility in how you handle alerts for specified thresholds.</span></span> <span data-ttu-id="6f5c7-345">例如，您可以定義自訂的 webhook。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-345">For example, you can define customized webhooks.</span></span> <span data-ttu-id="6f5c7-346">下列 webhook 範例來自 Resource Manager 範本：</span><span class="sxs-lookup"><span data-stu-id="6f5c7-346">The following webhook example is from a Resource Manager template:</span></span>

```json
{
    "type": "Microsoft.Insights/autoscaleSettings",
    "apiVersion": "[variables('insightsApi')]",
    "name": "autoscale",
    "location": "[parameters('resourceLocation')]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachineScaleSets/', parameters('vmSSName'))]"
    ],
    "properties": {
        "name": "autoscale",
        "targetResourceUri": "[concat('/subscriptions/',subscription().subscriptionId, '/resourceGroups/',  resourceGroup().name, '/providers/Microsoft.Compute/virtualMachineScaleSets/', parameters('vmSSName'))]",
        "enabled": true,
        "notifications": [
            {
                "operation": "Scale",
                "email": {
                    "sendToSubscriptionAdministrator": true,
                    "sendToSubscriptionCoAdministrators": true,
                    "customEmails": [
                        "youremail@address.com"
                    ]
                },
                "webhooks": [
                    {
                        "serviceUri": "https://events.pagerduty.com/integration/0b75b57246814149b4d87fa6e1273687/enqueue",
                        "properties": {
                            "key1": "custommetric",
                            "key2": "scalevmss"
                        }
                    }
                ]
            }
        ],
```

<span data-ttu-id="6f5c7-347">在此範例中，警示會在觸達臨界值時移至 Pagerduty.com。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-347">In this example, an alert goes to Pagerduty.com when a threshold is reached.</span></span>



## <a name="patching-and-operations"></a><span data-ttu-id="6f5c7-348">修補和作業</span><span class="sxs-lookup"><span data-stu-id="6f5c7-348">Patching and operations</span></span>

### <a name="how-do-i-create-a-scale-set-in-an-existing-resource-group"></a><span data-ttu-id="6f5c7-349">我如何在現有資源群組中建立擴展集？</span><span class="sxs-lookup"><span data-stu-id="6f5c7-349">How do I create a scale set in an existing resource group?</span></span>

<span data-ttu-id="6f5c7-350">您尚無法從 Azure 入口網站在現有資源群組中建立擴展集，但您從 Azure Resource Manager 範本部署擴展集時，可以指定現有的資源群組。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-350">Creating scale sets in an existing resource group is not yet possible from the Azure portal, but you can specify an existing resource group when deploying a scale set from an Azure Resource Manager template.</span></span> <span data-ttu-id="6f5c7-351">您也可以在使用 Azure PowerShell 或 CLI 建立擴展集時，指定現有的資源群組。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-351">You can also specify an existing resource group when creating a scale set using Azure PowerShell or CLI.</span></span>

### <a name="can-we-move-a-scale-set-to-another-resource-group"></a><span data-ttu-id="6f5c7-352">是否可以將擴展集移至另一個資源群組？</span><span class="sxs-lookup"><span data-stu-id="6f5c7-352">Can we move a scale set to another resource group?</span></span>

<span data-ttu-id="6f5c7-353">是，您可以將擴展集資源移至新的訂用帳戶或資源群組。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-353">Yes, you can move scale set resources to a new subscription or resource group.</span></span>

### <a name="how-to-i-update-my-virtual-machine-scale-set-to-a-new-image-how-do-i-manage-patching"></a><span data-ttu-id="6f5c7-354">如何將虛擬機器擴展集更新為新的映像？</span><span class="sxs-lookup"><span data-stu-id="6f5c7-354">How to I update my virtual machine scale set to a new image?</span></span> <span data-ttu-id="6f5c7-355">如何管理修補？</span><span class="sxs-lookup"><span data-stu-id="6f5c7-355">How do I manage patching?</span></span>

<span data-ttu-id="6f5c7-356">若要將虛擬機器擴展集更新為新的映像，以及管理修補，請參閱[升級虛擬機器擴展集](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-upgrade-scale-set)。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-356">To update your virtual machine scale set to a new image, and to manage patching, see [Upgrade a virtual machine scale set](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-upgrade-scale-set).</span></span>

### <a name="can-i-use-the-reimage-operation-to-reset-a-vm-without-changing-the-image-that-is-i-want-reset-a-vm-to-factory-settings-rather-than-to-a-new-image"></a><span data-ttu-id="6f5c7-357">是否可以使用重新安裝映像作業來重設 VM，而不變更映像？</span><span class="sxs-lookup"><span data-stu-id="6f5c7-357">Can I use the reimage operation to reset a VM without changing the image?</span></span> <span data-ttu-id="6f5c7-358">(也就是，我想要將 VM 重設為原廠設定，而不是新的映像。)</span><span class="sxs-lookup"><span data-stu-id="6f5c7-358">(That is, I want reset a VM to factory settings rather than to a new image.)</span></span>

<span data-ttu-id="6f5c7-359">是，您可以使用重新安裝映像作業來重設 VM，而不需變更映像。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-359">Yes, you can use the reimage operation to reset a VM without changing the image.</span></span> <span data-ttu-id="6f5c7-360">不過，如果虛擬機器擴展集參考 `version = latest` 的平台映像，當您呼叫 `reimage` 時，您的 VM 可以更新為較新版本的 OS 映像。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-360">However, if your virtual machine scale set references a platform image with `version = latest`, your VM can update to a later OS image when you call `reimage`.</span></span>

<span data-ttu-id="6f5c7-361">如需詳細資訊，請參閱[管理虛擬機器擴展集中的所有 VM](https://docs.microsoft.com/rest/api/virtualmachinescalesets/manage-all-vms-in-a-set)。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-361">For more information, see [Manage all VMs in a virtual machine scale set](https://docs.microsoft.com/rest/api/virtualmachinescalesets/manage-all-vms-in-a-set).</span></span>



## <a name="troubleshooting"></a><span data-ttu-id="6f5c7-362">疑難排解</span><span class="sxs-lookup"><span data-stu-id="6f5c7-362">Troubleshooting</span></span>

### <a name="how-do-i-turn-on-boot-diagnostics"></a><span data-ttu-id="6f5c7-363">如何開啟開機診斷？</span><span class="sxs-lookup"><span data-stu-id="6f5c7-363">How do I turn on boot diagnostics?</span></span>

<span data-ttu-id="6f5c7-364">若要開啟開機診斷，首先建立儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-364">To turn on boot diagnostics, first, create a storage account.</span></span> <span data-ttu-id="6f5c7-365">然後，將此 JSON 區塊放在虛擬機器擴展集 **virtualMachineProfile** 中，並更新此虛擬機器擴展集︰</span><span class="sxs-lookup"><span data-stu-id="6f5c7-365">Then, put this JSON block in your virtual machine scale set **virtualMachineProfile**, and update the virtual machine scale set:</span></span>

```json
"diagnosticsProfile": {
    "bootDiagnostics": {
        "enabled": true,
        "storageUri": "http://yourstorageaccount.blob.core.windows.net"
    }
}
```

<span data-ttu-id="6f5c7-366">建立新的 VM 時，VM 的 InstanceView 會顯示螢幕擷取畫面等的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-366">When a new VM is created, the InstanceView property of the VM shows the details for the screenshot, and so on.</span></span> <span data-ttu-id="6f5c7-367">以下是範例：</span><span class="sxs-lookup"><span data-stu-id="6f5c7-367">Here's an example:</span></span>
 
```json
"bootDiagnostics": {
    "consoleScreenshotBlobUri": "https://o0sz3nhtbmkg6geswarm5.blob.core.windows.net/bootdiagnostics-swarmagen-4157d838-8335-4f78-bf0e-b616a99bc8bd/swarm-agent-9574AE92vmss-0_2.4157d838-8335-4f78-bf0e-b616a99bc8bd.screenshot.bmp",
    "serialConsoleLogBlobUri": "https://o0sz3nhtbmkg6geswarm5.blob.core.windows.net/bootdiagnostics-swarmagen-4157d838-8335-4f78-bf0e-b616a99bc8bd/swarm-agent-9574AE92vmss-0_2.4157d838-8335-4f78-bf0e-b616a99bc8bd.serialconsole.log"
  }
```


## <a name="virtual-machine-properties"></a><span data-ttu-id="6f5c7-368">虛擬機器屬性</span><span class="sxs-lookup"><span data-stu-id="6f5c7-368">Virtual machine properties</span></span>

### <a name="how-do-i-get-property-information-for-each-vm-without-making-multiple-calls-for-example-how-would-i-get-the-fault-domain-for-each-of-the-100-vms-in-my-virtual-machine-scale-set"></a><span data-ttu-id="6f5c7-369">如何取得每部 VM 的屬性資訊，而不進行多次呼叫？</span><span class="sxs-lookup"><span data-stu-id="6f5c7-369">How do I get property information for each VM without making multiple calls?</span></span> <span data-ttu-id="6f5c7-370">例如，如何針對虛擬機器擴展集中的 100 部 VM 取得各自的容錯網域？</span><span class="sxs-lookup"><span data-stu-id="6f5c7-370">For example, how would I get the fault domain for each of the 100 VMs in my virtual machine scale set?</span></span>

<span data-ttu-id="6f5c7-371">若要取得每部 VM 的屬性資訊，而不進行多次呼叫，您可以對下列資源 URI 進行 REST API`GET`，藉此呼叫 `ListVMInstanceViews`：</span><span class="sxs-lookup"><span data-stu-id="6f5c7-371">To get property information for each VM without making multiple calls, you can call `ListVMInstanceViews` by doing a REST API `GET` on the following resource URI:</span></span>

<span data-ttu-id="6f5c7-372">/subscriptions/<subscription_id>/resourceGroups/<resource_group_name>/providers/Microsoft.Compute/virtualMachineScaleSets/<scaleset_name>/virtualMachines?$expand=instanceView&$select=instanceView</span><span class="sxs-lookup"><span data-stu-id="6f5c7-372">/subscriptions/<subscription_id>/resourceGroups/<resource_group_name>/providers/Microsoft.Compute/virtualMachineScaleSets/<scaleset_name>/virtualMachines?$expand=instanceView&$select=instanceView</span></span>

### <a name="can-i-pass-different-extension-arguments-to-different-vms-in-a-virtual-machine-scale-set"></a><span data-ttu-id="6f5c7-373">是否可以將不同的擴充引數傳遞至虛擬機器擴展集中的不同 VM？</span><span class="sxs-lookup"><span data-stu-id="6f5c7-373">Can I pass different extension arguments to different VMs in a virtual machine scale set?</span></span>

<span data-ttu-id="6f5c7-374">否，您無法將不同的擴充引數傳遞至虛擬機器擴展集中的不同 VM。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-374">No, you cannot pass different extension arguments to different VMs in a virtual machine scale set.</span></span> <span data-ttu-id="6f5c7-375">不過，擴充功能可以根據它們執行所在 VM 的唯一屬性來行動，例如根據電腦名稱。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-375">However, extensions can act based on the unique properties of the VM they are running on, such as on the machine name.</span></span> <span data-ttu-id="6f5c7-376">擴充功能也可以在 http://169.254.169.254 上查詢執行個體中繼資料，以取得 VM 詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-376">Extensions also can query instance metadata on http://169.254.169.254 to get more information about the VM.</span></span>

### <a name="why-are-there-gaps-between-my-virtual-machine-scale-set-vm-machine-names-and-vm-ids-for-example-0-1-3"></a><span data-ttu-id="6f5c7-377">為何我的虛擬機器擴展集 VM 電腦名稱與 VM 識別碼之間會有落差？</span><span class="sxs-lookup"><span data-stu-id="6f5c7-377">Why are there gaps between my virtual machine scale set VM machine names and VM IDs?</span></span> <span data-ttu-id="6f5c7-378">例如：0、1、3...</span><span class="sxs-lookup"><span data-stu-id="6f5c7-378">For example: 0, 1, 3...</span></span>

<span data-ttu-id="6f5c7-379">您的虛擬機器擴展集 VM 電腦名稱與 VM 識別碼之間有落差，是因為虛擬機器擴展集將 **overprovision** 屬性設定為預設值 **true**。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-379">There are gaps between your virtual machine scale set VM machine names and VM IDs because your virtual machine scale set **overprovision** property is set to the default value of **true**.</span></span> <span data-ttu-id="6f5c7-380">如果過度佈建設定為 **true**，則會建立超過要求的 VM。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-380">If overprovisioning is set to **true**, more VMs than requested are created.</span></span> <span data-ttu-id="6f5c7-381">然後會刪除額外的 VM。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-381">Extra VMs are then deleted.</span></span> <span data-ttu-id="6f5c7-382">在此情況下，您會取得更高的部署可靠性，但代價是連續的命名和連續的網路位址轉譯 (NAT) 規則。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-382">In this case, you gain increased deployment reliability, but at the expense of contiguous naming and contiguous Network Address Translation (NAT) rules.</span></span> 

<span data-ttu-id="6f5c7-383">您可以將此屬性設定為 **false**。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-383">You can set this property to **false**.</span></span> <span data-ttu-id="6f5c7-384">若為小型虛擬機器擴展集，這就不會大幅影響部署可靠性。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-384">For small virtual machine scale sets, this doesn't significantly affect deployment reliability.</span></span>

### <a name="what-is-the-difference-between-deleting-a-vm-in-a-virtual-machine-scale-set-and-deallocating-the-vm-when-should-i-choose-one-over-the-other"></a><span data-ttu-id="6f5c7-385">刪除虛擬機器擴展集中的 VM 與解除配置 VM 之間的差異為何？</span><span class="sxs-lookup"><span data-stu-id="6f5c7-385">What is the difference between deleting a VM in a virtual machine scale set and deallocating the VM?</span></span> <span data-ttu-id="6f5c7-386">我何時應該選擇優先其中一個？</span><span class="sxs-lookup"><span data-stu-id="6f5c7-386">When should I choose one over the other?</span></span>

<span data-ttu-id="6f5c7-387">刪除虛擬機器擴展集中的 VM 與解除配置 VM 之間的主要差異在於 `deallocate` 不會刪除虛擬硬碟 (VHD)。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-387">The main difference between deleting a VM in a virtual machine scale set and deallocating the VM is that `deallocate` doesn’t delete the virtual hard disks (VHDs).</span></span> <span data-ttu-id="6f5c7-388">執行 `stop deallocate` 會產生相關的儲存體成本。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-388">There are storage costs associated with running `stop deallocate`.</span></span> <span data-ttu-id="6f5c7-389">基於下列原因之一，您可能會採用其中一種做法：</span><span class="sxs-lookup"><span data-stu-id="6f5c7-389">You might use one or the other for one of the following reasons:</span></span>

- <span data-ttu-id="6f5c7-390">您想要停止支付計算成本，但又想要保留 VM 的磁碟狀態。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-390">You want to stop paying compute costs, but you want to keep the disk state of the VMs.</span></span>
- <span data-ttu-id="6f5c7-391">您想要更快速地啟動一組 VM，則可相應放大虛擬機器擴展集。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-391">You want to start a set of VMs more quickly than you could scale out a virtual machine scale set.</span></span>
  - <span data-ttu-id="6f5c7-392">關於這種情況，您可能已建立自己的自動調整引擎，並想要更快速的端對端擴展。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-392">Related to this scenario, you might have created your own autoscale engine and want a faster end-to-end scale.</span></span>
- <span data-ttu-id="6f5c7-393">您的虛擬機器擴展集並未平均分散於各容錯網域或更新網域。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-393">You have a virtual machine scale set that is unevenly distributed across fault domains or update domains.</span></span> <span data-ttu-id="6f5c7-394">這可能是因為您選擇性地刪除 VM，或是因為 VM 在過度佈建之後遭到刪除。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-394">This might be because you selectively deleted VMs, or because VMs were deleted after overprovisioning.</span></span> <span data-ttu-id="6f5c7-395">在虛擬機器擴展集上接續執行 `stop deallocate` 和 `start`，可讓 VM 平均分散於各容錯網域或更新網域。</span><span class="sxs-lookup"><span data-stu-id="6f5c7-395">Running `stop deallocate` followed by `start` on the virtual machine scale set evenly distributes the VMs across fault domains or update domains.</span></span>

