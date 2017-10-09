---
title: "aaaAzure 虛擬機器規模設定常見問題集 |Microsoft 文件"
description: "取得虛擬機器擴展集相關常見問題的解答 toofrequently。"
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
ms.openlocfilehash: 0deb9e2bb79f87f17bbf748397b94dc53070cfbb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-machine-scale-sets-faqs"></a><span data-ttu-id="ee0db-103">Azure 虛擬機器擴展集常見問題集</span><span class="sxs-lookup"><span data-stu-id="ee0db-103">Azure virtual machine scale sets FAQs</span></span>

<span data-ttu-id="ee0db-104">取得在 Azure 中設定 toofrequently 關於虛擬機器規模集的解答。</span><span class="sxs-lookup"><span data-stu-id="ee0db-104">Get answers toofrequently asked questions about virtual machine scale sets in Azure.</span></span>

## <a name="autoscale"></a><span data-ttu-id="ee0db-105">Autoscale</span><span class="sxs-lookup"><span data-stu-id="ee0db-105">Autoscale</span></span>

### <a name="what-are-best-practices-for-azure-autoscale"></a><span data-ttu-id="ee0db-106">什麼是 Azure 自動調整的最佳做法？</span><span class="sxs-lookup"><span data-stu-id="ee0db-106">What are best practices for Azure Autoscale?</span></span>

<span data-ttu-id="ee0db-107">如需自動調整的最佳做法，請參閱[自動調整虛擬機器的最佳做法](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-autoscale-best-practices)。</span><span class="sxs-lookup"><span data-stu-id="ee0db-107">For best practices for Autoscale, see [Best practices for autoscaling virtual machines](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-autoscale-best-practices).</span></span>

### <a name="where-do-i-find-metric-names-for-autoscaling-that-uses-host-based-metrics"></a><span data-ttu-id="ee0db-108">哪裡可以找到使用主機型計量自動調整的計量名稱？</span><span class="sxs-lookup"><span data-stu-id="ee0db-108">Where do I find metric names for autoscaling that uses host-based metrics?</span></span>

<span data-ttu-id="ee0db-109">如需使用主機型計量之自動調整的計量名稱，請參閱[支援的 Azure 監視器度量](https://azure.microsoft.com/documentation/articles/monitoring-supported-metrics/)。</span><span class="sxs-lookup"><span data-stu-id="ee0db-109">For metric names for autoscaling that uses host-based metrics, see [Supported metrics with Azure Monitor](https://azure.microsoft.com/documentation/articles/monitoring-supported-metrics/).</span></span>

### <a name="are-there-any-examples-of-autoscaling-based-on-an-azure-service-bus-topic-and-queue-length"></a><span data-ttu-id="ee0db-110">是否有任何根據 Azure 服務匯流排主題和佇列長度自動調整的範例？</span><span class="sxs-lookup"><span data-stu-id="ee0db-110">Are there any examples of autoscaling based on an Azure Service Bus topic and queue length?</span></span>

<span data-ttu-id="ee0db-111">是。</span><span class="sxs-lookup"><span data-stu-id="ee0db-111">Yes.</span></span> <span data-ttu-id="ee0db-112">如需根據 Azure 服務匯流排主題和佇列長度自動調整的範例，請參閱 [Azure 監視器的自動調整常用計量](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/)。</span><span class="sxs-lookup"><span data-stu-id="ee0db-112">For examples of autoscaling based on an Azure Service Bus topic and queue length, see [Azure Monitor autoscaling common metrics](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/).</span></span>

<span data-ttu-id="ee0db-113">服務匯流排佇列，請使用下列 JSON hello:</span><span class="sxs-lookup"><span data-stu-id="ee0db-113">For a Service Bus queue, use hello following JSON:</span></span>

```json
"metricName": "MessageCount",
"metricNamespace": "",
"metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.ServiceBus/namespaces/mySB/queues/myqueue"
```

<span data-ttu-id="ee0db-114">儲存體佇列，請使用下列 JSON hello:</span><span class="sxs-lookup"><span data-stu-id="ee0db-114">For a storage queue, use hello following JSON:</span></span>

```json
"metricName": "ApproximateMessageCount",
"metricNamespace": "",
"metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.ClassicStorage/storageAccounts/mystorage/services/queue/queues/mystoragequeue"
```

<span data-ttu-id="ee0db-115">以您資源的統一資源識別項 (URI) 取代範例值。</span><span class="sxs-lookup"><span data-stu-id="ee0db-115">Replace example values with your resource Uniform Resource Identifiers (URIs).</span></span>


### <a name="should-i-autoscale-by-using-host-based-metrics-or-a-diagnostics-extension"></a><span data-ttu-id="ee0db-116">我應該使用主機型計量或診斷擴充功能進行自動調整？</span><span class="sxs-lookup"><span data-stu-id="ee0db-116">Should I autoscale by using host-based metrics or a diagnostics extension?</span></span>

<span data-ttu-id="ee0db-117">您可以建立自動調整設定在 VM toouse 主機層級度量或客體作業系統為基礎的度量。</span><span class="sxs-lookup"><span data-stu-id="ee0db-117">You can create an autoscale setting on a VM toouse host-level metrics or guest OS-based metrics.</span></span>

<span data-ttu-id="ee0db-118">如需支援的計量資訊，請參閱 [Azure 監視器的自動調整常見計量](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-autoscale-common-metrics)。</span><span class="sxs-lookup"><span data-stu-id="ee0db-118">For a list of supported metrics, see [Azure Monitor autoscaling common metrics](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-autoscale-common-metrics).</span></span> 

<span data-ttu-id="ee0db-119">如需虛擬機器擴展集的完整範例，請參閱[使用虛擬機器擴展集的 Resource Manager 範本進行進階自動調整設定](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-advanced-autoscale-virtual-machine-scale-sets)。</span><span class="sxs-lookup"><span data-stu-id="ee0db-119">For a full sample for virtual machine scale sets, see [Advanced autoscale configuration by using Resource Manager templates for virtual machine scale sets](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-advanced-autoscale-virtual-machine-scale-sets).</span></span> 

<span data-ttu-id="ee0db-120">hello 範例會使用 hello 主機層級 CPU 度量和訊息計數 」 指標。</span><span class="sxs-lookup"><span data-stu-id="ee0db-120">hello sample uses hello host-level CPU metric and a message count metric.</span></span>



### <a name="how-do-i-set-alert-rules-on-a-virtual-machine-scale-set"></a><span data-ttu-id="ee0db-121">如何設定虛擬機器擴展集的警示規則？</span><span class="sxs-lookup"><span data-stu-id="ee0db-121">How do I set alert rules on a virtual machine scale set?</span></span>

<span data-ttu-id="ee0db-122">您可以透過 PowerShell 或 Azure CLI，建立虛擬機器擴展集計量的警示。</span><span class="sxs-lookup"><span data-stu-id="ee0db-122">You can create alerts on metrics for virtual machine scale sets via PowerShell or Azure CLI.</span></span> <span data-ttu-id="ee0db-123">如需詳細資訊，請參閱 [Azure 監視器 PowerShell 快速入門範例](https://azure.microsoft.com/documentation/articles/insights-powershell-samples/#create-alert-rules)和 [Azure 監視器跨平台 CLI 快速入門範例](https://azure.microsoft.com/documentation/articles/insights-cli-samples/#work-with-alerts)。</span><span class="sxs-lookup"><span data-stu-id="ee0db-123">For more information, see [Azure Monitor PowerShell quick start samples](https://azure.microsoft.com/documentation/articles/insights-powershell-samples/#create-alert-rules) and [Azure Monitor cross-platform CLI quick start samples](https://azure.microsoft.com/documentation/articles/insights-cli-samples/#work-with-alerts).</span></span>

<span data-ttu-id="ee0db-124">hello TargetResourceId hello 虛擬機器擴展集看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="ee0db-124">hello TargetResourceId of hello virtual machine scale set looks like this:</span></span> 

<span data-ttu-id="ee0db-125">/subscriptions/yoursubscriptionid/resourceGroups/yourresourcegroup/providers/Microsoft.Compute/virtualMachineScaleSets/yourvmssname</span><span class="sxs-lookup"><span data-stu-id="ee0db-125">/subscriptions/yoursubscriptionid/resourceGroups/yourresourcegroup/providers/Microsoft.Compute/virtualMachineScaleSets/yourvmssname</span></span>

<span data-ttu-id="ee0db-126">您可以選擇任何 VM 效能計數器為 hello 度量 tooset 的警示。</span><span class="sxs-lookup"><span data-stu-id="ee0db-126">You can choose any VM performance counter as hello metric tooset an alert for.</span></span> <span data-ttu-id="ee0db-127">如需詳細資訊，請參閱[資源管理員為基礎的 Windows Vm 的客體 OS 度量](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/#guest-os-metrics-resource-manager-based-windows-vms)和[適用於 Linux Vm 的客體 OS 度量](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/#guest-os-metrics-linux-vms)在 hello [Azure 監視自動調整常見標準](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/)發行項。</span><span class="sxs-lookup"><span data-stu-id="ee0db-127">For more information, see [Guest OS metrics for Resource Manager-based Windows VMs](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/#guest-os-metrics-resource-manager-based-windows-vms) and [Guest OS metrics for Linux VMs](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/#guest-os-metrics-linux-vms) in hello [Azure Monitor autoscaling common metrics](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/) article.</span></span>

### <a name="how-do-i-set-up-autoscale-on-a-virtual-machine-scale-set-by-using-powershell"></a><span data-ttu-id="ee0db-128">如何使用 PowerShell 在虛擬機器擴展集上設定自動調整？</span><span class="sxs-lookup"><span data-stu-id="ee0db-128">How do I set up autoscale on a virtual machine scale set by using PowerShell?</span></span>

<span data-ttu-id="ee0db-129">tooset 設定自動調整規模上的虛擬機器擴展集使用 PowerShell，請參閱 hello 部落格文章[tooadd 自動調整規模 tooan Azure 虛擬機器規模的設定方式](https://msftstack.wordpress.com/2017/03/05/how-to-add-autoscale-to-an-azure-vm-scale-set/)。</span><span class="sxs-lookup"><span data-stu-id="ee0db-129">tooset up autoscale on a virtual machine scale set by using PowerShell, see hello blog post [How tooadd autoscale tooan Azure virtual machine scale set](https://msftstack.wordpress.com/2017/03/05/how-to-add-autoscale-to-an-azure-vm-scale-set/).</span></span>




## <a name="certificates"></a><span data-ttu-id="ee0db-130">憑證</span><span class="sxs-lookup"><span data-stu-id="ee0db-130">Certificates</span></span>

### <a name="how-do-i-securely-ship-a-certificate-toohello-vm-how-do-i-provision-a-virtual-machine-scale-set-toorun-a-website-where-hello-ssl-for-hello-website-is-shipped-securely-from-a-certificate-configuration-hello-common-certificate-rotation-operation-would-be-almost-hello-same-as-a-configuration-update-operation-do-you-have-an-example-of-how-toodo-this"></a><span data-ttu-id="ee0db-131">如何安全地發行憑證 toohello VM？</span><span class="sxs-lookup"><span data-stu-id="ee0db-131">How do I securely ship a certificate toohello VM?</span></span> <span data-ttu-id="ee0db-132">如何佈建虛擬機器規模集 toorun 其中 hello hello 網站的 SSL 於安全的憑證設定的網站？</span><span class="sxs-lookup"><span data-stu-id="ee0db-132">How do I provision a virtual machine scale set toorun a website where hello SSL for hello website is shipped securely from a certificate configuration?</span></span> <span data-ttu-id="ee0db-133">(hello 常見的憑證旋轉作業將會幾乎 hello 相同的組態更新作業。)您是否有如何的範例 toodo 這？</span><span class="sxs-lookup"><span data-stu-id="ee0db-133">(hello common certificate rotation operation would be almost hello same as a configuration update operation.) Do you have an example of how toodo this?</span></span> 

<span data-ttu-id="ee0db-134">toosecurely 出貨憑證 toohello VM，您可以直接在 hello 客戶的金鑰保存庫中的 Windows 憑證存放區安裝客戶憑證。</span><span class="sxs-lookup"><span data-stu-id="ee0db-134">toosecurely ship a certificate toohello VM, you can install a customer certificate directly into a Windows certificate store from hello customer's key vault.</span></span>

<span data-ttu-id="ee0db-135">使用下列 JSON hello:</span><span class="sxs-lookup"><span data-stu-id="ee0db-135">Use hello following JSON:</span></span>

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

<span data-ttu-id="ee0db-136">hello 的程式碼支援 Windows 和 Linux。</span><span class="sxs-lookup"><span data-stu-id="ee0db-136">hello code supports Windows and Linux.</span></span>

<span data-ttu-id="ee0db-137">如需詳細資訊，請參閱[建立或更新虛擬機器擴展集](https://msdn.microsoft.com/library/mt589035.aspx)。</span><span class="sxs-lookup"><span data-stu-id="ee0db-137">For more information, see [Create or update a virtual machine scale set](https://msdn.microsoft.com/library/mt589035.aspx).</span></span>


### <a name="example-of-self-signed-certificate"></a><span data-ttu-id="ee0db-138">自我簽署憑證的範例</span><span class="sxs-lookup"><span data-stu-id="ee0db-138">Example of Self-signed certificate</span></span>

1.  <span data-ttu-id="ee0db-139">在金鑰保存庫中建立自我簽署憑證。</span><span class="sxs-lookup"><span data-stu-id="ee0db-139">Create a self-signed certificate in a key vault.</span></span>

    <span data-ttu-id="ee0db-140">使用下列 PowerShell 命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="ee0db-140">Use hello following PowerShell commands:</span></span>

    ```powershell
    Import-Module "C:\Users\mikhegn\Downloads\Service-Fabric-master\Scripts\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1"

    Login-AzureRmAccount

    Invoke-AddCertToKeyVault -SubscriptionId <Your SubID> -ResourceGroupName KeyVault -Location westus -VaultName MikhegnVault -CertificateName VMSSCert -Password VmssCert -CreateSelfSignedCertificate -DnsName vmss.mikhegn.azure.com -OutputPath c:\users\mikhegn\desktop\
    ```

    <span data-ttu-id="ee0db-141">此命令提供下列 hello hello Azure Resource Manager 範本的輸入。</span><span class="sxs-lookup"><span data-stu-id="ee0db-141">This command gives you hello input for hello Azure Resource Manager template.</span></span>

    <span data-ttu-id="ee0db-142">如需如何 toocreate 自我簽署的憑證中金鑰保存庫，請參閱[Service Fabric 叢集安全性案例](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/)。</span><span class="sxs-lookup"><span data-stu-id="ee0db-142">For an example of how toocreate a self-signed certificate in a key vault, see [Service Fabric cluster security scenarios](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/).</span></span>

2.  <span data-ttu-id="ee0db-143">變更 hello Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="ee0db-143">Change hello Resource Manager template.</span></span>

    <span data-ttu-id="ee0db-144">新增此屬性太**virtualMachineProfile**，hello 一部分的虛擬機器規模集資源：</span><span class="sxs-lookup"><span data-stu-id="ee0db-144">Add this property too**virtualMachineProfile**, as part of hello virtual machine scale set resource:</span></span>

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
  

### <a name="can-i-specify-an-ssh-key-pair-toouse-for-ssh-authentication-with-a-linux-virtual-machine-scale-set-from-a-resource-manager-template"></a><span data-ttu-id="ee0db-145">可以指定 SSH 驗證 SSH 金鑰組的 toouse 設定資源管理員範本中的 Linux 虛擬機器比例嗎？</span><span class="sxs-lookup"><span data-stu-id="ee0db-145">Can I specify an SSH key pair toouse for SSH authentication with a Linux virtual machine scale set from a Resource Manager template?</span></span>  

<span data-ttu-id="ee0db-146">是。</span><span class="sxs-lookup"><span data-stu-id="ee0db-146">Yes.</span></span> <span data-ttu-id="ee0db-147">hello REST API 的**osProfile**是類似 toohello 標準 VM REST API。</span><span class="sxs-lookup"><span data-stu-id="ee0db-147">hello REST API for **osProfile** is similar toohello standard VM REST API.</span></span> 

<span data-ttu-id="ee0db-148">在您的範本中包含 **osProfile**︰</span><span class="sxs-lookup"><span data-stu-id="ee0db-148">Include **osProfile** in your template:</span></span>

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
 
<span data-ttu-id="ee0db-149">在中使用此 JSON 區塊[hello 101-vm-sshkey GitHub 快速入門範本](https://github.com/Azure/azure-quickstart-templates/blob/master/101-vm-sshkey/azuredeploy.json)。</span><span class="sxs-lookup"><span data-stu-id="ee0db-149">This JSON block is used in [hello 101-vm-sshkey GitHub quick start template](https://github.com/Azure/azure-quickstart-templates/blob/master/101-vm-sshkey/azuredeploy.json).</span></span>
 
<span data-ttu-id="ee0db-150">hello OS 設定檔也會用於[hello grelayhost.json GitHub 快速啟動範本](https://github.com/ExchMaster/gadgetron/blob/master/Gadgetron/Templates/grelayhost.json)。</span><span class="sxs-lookup"><span data-stu-id="ee0db-150">hello OS profile also is used in [hello grelayhost.json GitHub quick start template](https://github.com/ExchMaster/gadgetron/blob/master/Gadgetron/Templates/grelayhost.json).</span></span>

<span data-ttu-id="ee0db-151">如需詳細資訊，請參閱[建立或更新虛擬機器擴展集](https://msdn.microsoft.com/library/azure/mt589035.aspx#linuxconfiguration)。</span><span class="sxs-lookup"><span data-stu-id="ee0db-151">For more information, see [Create or update a virtual machine scale set](https://msdn.microsoft.com/library/azure/mt589035.aspx#linuxconfiguration).</span></span>
  

### <a name="how-do-i-remove-deprecated-certificates"></a><span data-ttu-id="ee0db-152">如何移除已被取代的憑證？</span><span class="sxs-lookup"><span data-stu-id="ee0db-152">How do I remove deprecated certificates?</span></span> 

<span data-ttu-id="ee0db-153">tooremove 取代 hello 保存庫憑證清單中移除 hello 舊憑證的憑證。</span><span class="sxs-lookup"><span data-stu-id="ee0db-153">tooremove deprecated certificates, remove hello old certificate from hello vault certificates list.</span></span> <span data-ttu-id="ee0db-154">將保留的 tooremain hello 清單中電腦上的所有 hello 憑證。</span><span class="sxs-lookup"><span data-stu-id="ee0db-154">Leave all hello certificates that you want tooremain on your computer in hello list.</span></span> <span data-ttu-id="ee0db-155">這不會移除 hello 憑證所有 Vm。</span><span class="sxs-lookup"><span data-stu-id="ee0db-155">This does not remove hello certificate from all your VMs.</span></span> <span data-ttu-id="ee0db-156">它也不會新增 hello 憑證 toonew hello 虛擬機器規模集中建立的 Vm。</span><span class="sxs-lookup"><span data-stu-id="ee0db-156">It also does not add hello certificate toonew VMs that are created in hello virtual machine scale set.</span></span> 

<span data-ttu-id="ee0db-157">現有的 Vm 所傳來的 tooremove hello 憑證撰寫自訂指令碼延伸 toomanually 移除 hello 憑證從憑證存放區。</span><span class="sxs-lookup"><span data-stu-id="ee0db-157">tooremove hello certificate from existing VMs, write a custom script extension toomanually remove hello certificates from your certificate store.</span></span>
 
### <a name="how-do-i-inject-an-existing-ssh-public-key-into-hello-virtual-machine-scale-set-ssh-layer-during-provisioning-i-want-toostore-hello-ssh-public-key-values-in-azure-key-vault-and-then-use-them-in-my-resource-manager-template"></a><span data-ttu-id="ee0db-158">我如何插入現有的 SSH 公開金鑰 hello 虛擬機器規模集 SSH 層佈建期間？</span><span class="sxs-lookup"><span data-stu-id="ee0db-158">How do I inject an existing SSH public key into hello virtual machine scale set SSH layer during provisioning?</span></span> <span data-ttu-id="ee0db-159">我想 toostore hello SSH 公開金鑰值在 Azure 金鑰保存庫，然後在 我的資源管理員範本中使用它們。</span><span class="sxs-lookup"><span data-stu-id="ee0db-159">I want toostore hello SSH public key values in Azure Key Vault, and then use them in my Resource Manager template.</span></span>

<span data-ttu-id="ee0db-160">如果您要提供 hello Vm 只能與 SSH 公開金鑰，您不需要 tooput hello 公用金鑰在金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="ee0db-160">If you are providing hello VMs only with a public SSH key, you don't need tooput hello public keys in Key Vault.</span></span> <span data-ttu-id="ee0db-161">公開金鑰不是密碼。</span><span class="sxs-lookup"><span data-stu-id="ee0db-161">Public keys are not secret.</span></span>
 
<span data-ttu-id="ee0db-162">您可以在建立 Linux VM 時以純文字提供 SSH 公開金鑰：</span><span class="sxs-lookup"><span data-stu-id="ee0db-162">You can provide SSH public keys in plain text when you create a Linux VM:</span></span>

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
 
<span data-ttu-id="ee0db-163">linuxConfiguration 元素名稱</span><span class="sxs-lookup"><span data-stu-id="ee0db-163">linuxConfiguration element name</span></span> | <span data-ttu-id="ee0db-164">必要</span><span class="sxs-lookup"><span data-stu-id="ee0db-164">Required</span></span> | <span data-ttu-id="ee0db-165">類型</span><span class="sxs-lookup"><span data-stu-id="ee0db-165">Type</span></span> | <span data-ttu-id="ee0db-166">說明</span><span class="sxs-lookup"><span data-stu-id="ee0db-166">Description</span></span>
--- | --- | --- | --- |  ---
<span data-ttu-id="ee0db-167">ssh</span><span class="sxs-lookup"><span data-stu-id="ee0db-167">ssh</span></span> | <span data-ttu-id="ee0db-168">否</span><span class="sxs-lookup"><span data-stu-id="ee0db-168">No</span></span> | <span data-ttu-id="ee0db-169">集合</span><span class="sxs-lookup"><span data-stu-id="ee0db-169">Collection</span></span> | <span data-ttu-id="ee0db-170">指定 Linux 作業系統的 hello SSH 金鑰設定</span><span class="sxs-lookup"><span data-stu-id="ee0db-170">Specifies hello SSH key configuration for a Linux OS</span></span>
<span data-ttu-id="ee0db-171">路徑</span><span class="sxs-lookup"><span data-stu-id="ee0db-171">path</span></span> | <span data-ttu-id="ee0db-172">是</span><span class="sxs-lookup"><span data-stu-id="ee0db-172">Yes</span></span> | <span data-ttu-id="ee0db-173">String</span><span class="sxs-lookup"><span data-stu-id="ee0db-173">String</span></span> | <span data-ttu-id="ee0db-174">指定其中 hello SSH 金鑰或憑證應該位於 hello Linux 檔案路徑</span><span class="sxs-lookup"><span data-stu-id="ee0db-174">Specifies hello Linux file path where hello SSH keys or certificate should be located</span></span>
<span data-ttu-id="ee0db-175">keyData</span><span class="sxs-lookup"><span data-stu-id="ee0db-175">keyData</span></span> | <span data-ttu-id="ee0db-176">是</span><span class="sxs-lookup"><span data-stu-id="ee0db-176">Yes</span></span> | <span data-ttu-id="ee0db-177">String</span><span class="sxs-lookup"><span data-stu-id="ee0db-177">String</span></span> | <span data-ttu-id="ee0db-178">指定 base64 編碼的 SSH 公開金鑰</span><span class="sxs-lookup"><span data-stu-id="ee0db-178">Specifies a base64-encoded SSH public key</span></span>

<span data-ttu-id="ee0db-179">如需範例，請參閱[hello 101-vm-sshkey GitHub 快速入門範本](https://github.com/Azure/azure-quickstart-templates/blob/master/101-vm-sshkey/azuredeploy.json)。</span><span class="sxs-lookup"><span data-stu-id="ee0db-179">For an example, see [hello 101-vm-sshkey GitHub quick start template](https://github.com/Azure/azure-quickstart-templates/blob/master/101-vm-sshkey/azuredeploy.json).</span></span>

 
### <a name="when-i-run-update-azurermvmss-after-adding-more-than-one-certificate-from-hello-same-key-vault-i-see-hello-following-message"></a><span data-ttu-id="ee0db-180">當我執行`Update-AzureRmVmss`之後從 hello 加入一個以上的憑證相同金鑰保存庫，我看到下列訊息 hello:</span><span class="sxs-lookup"><span data-stu-id="ee0db-180">When I run `Update-AzureRmVmss` after adding more than one certificate from hello same key vault, I see hello following message:</span></span>
 
><span data-ttu-id="ee0db-181">Update-AzureRmVmss: 清單密碼包含重複的 /subscriptions/<my-subscription-id>/resourceGroups/internal-rg-dev/providers/Microsoft.KeyVault/vaults/internal-keyvault-dev 執行個體，不允許這種情況。</span><span class="sxs-lookup"><span data-stu-id="ee0db-181">Update-AzureRmVmss: List secret contains repeated instances of /subscriptions/<my-subscription-id>/resourceGroups/internal-rg-dev/providers/Microsoft.KeyVault/vaults/internal-keyvault-dev, which is disallowed.</span></span>
 
<span data-ttu-id="ee0db-182">如果您嘗試 toore 此情形-新增的 hello 相同保存庫而不是使用新的保存庫憑證 hello 現有來源保存庫。</span><span class="sxs-lookup"><span data-stu-id="ee0db-182">This can happen if you try toore-add hello same vault instead of using a new vault certificate for hello existing source vault.</span></span> <span data-ttu-id="ee0db-183">hello`Add-AzureRmVmssSecret`命令無法正常運作如果您要新增其他機密資料。</span><span class="sxs-lookup"><span data-stu-id="ee0db-183">hello `Add-AzureRmVmssSecret` command does not work correctly if you are adding additional secrets.</span></span>
 
<span data-ttu-id="ee0db-184">tooadd hello 從多個密碼相同的金鑰保存庫中，更新 hello $vmss.properties.osProfile.secrets[0].vaultCertificates 清單。</span><span class="sxs-lookup"><span data-stu-id="ee0db-184">tooadd more secrets from hello same key vault, update hello $vmss.properties.osProfile.secrets[0].vaultCertificates list.</span></span>
 
<span data-ttu-id="ee0db-185">如 hello 預期輸入的結構，請參閱 <<c0> [ 建立或更新虛擬機器設定](https://msdn.microsoft.com/library/azure/mt589035.aspx)。</span><span class="sxs-lookup"><span data-stu-id="ee0db-185">For hello expected input structure, see [Create or update a virtual machine set](https://msdn.microsoft.com/library/azure/mt589035.aspx).</span></span>
 
<span data-ttu-id="ee0db-186">尋找在 hello 虛擬機器規模集物件的 hello 金鑰保存庫中的 hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="ee0db-186">Find hello secret in hello virtual machine scale set object that is in hello key vault.</span></span> <span data-ttu-id="ee0db-187">接著，新增您 hello 保存庫相關聯的憑證 （hello URL 和 hello 密碼存放區名稱） 的參考 toohello 清單。</span><span class="sxs-lookup"><span data-stu-id="ee0db-187">Then, add your certificate reference (hello URL and hello secret store name) toohello list associated with hello vault.</span></span>

> [!NOTE] 
> <span data-ttu-id="ee0db-188">目前，您無法使用 hello 虛擬機器規模集 API，從 Vm 移除憑證。</span><span class="sxs-lookup"><span data-stu-id="ee0db-188">Currently, you cannot remove certificates from VMs by using hello virtual machine scale set API.</span></span>
>

<span data-ttu-id="ee0db-189">新的 Vm 不會有 hello 舊的憑證。</span><span class="sxs-lookup"><span data-stu-id="ee0db-189">New VMs will not have hello old certificate.</span></span> <span data-ttu-id="ee0db-190">不過，具有 hello 憑證，且其已部署的 Vm 會具備 hello 舊憑證。</span><span class="sxs-lookup"><span data-stu-id="ee0db-190">However, VMs that have hello certificate and which are already deployed will have hello old certificate.</span></span>
 
### <a name="can-i-push-certificates-toohello-virtual-machine-scale-set-without-providing-hello-password-when-hello-certificate-is-in-hello-secret-store"></a><span data-ttu-id="ee0db-191">可以推播憑證 toohello 虛擬機器擴展集而不需 hello 密碼存放區 hello 憑證時提供 hello 密碼嗎？</span><span class="sxs-lookup"><span data-stu-id="ee0db-191">Can I push certificates toohello virtual machine scale set without providing hello password, when hello certificate is in hello secret store?</span></span>

<span data-ttu-id="ee0db-192">您不需要 toohard 程式碼在指令碼中的密碼。</span><span class="sxs-lookup"><span data-stu-id="ee0db-192">You do not need toohard-code passwords in scripts.</span></span> <span data-ttu-id="ee0db-193">您可以動態擷取密碼與 hello 權限，您使用 toorun hello 部署指令碼。</span><span class="sxs-lookup"><span data-stu-id="ee0db-193">You can dynamically retrieve passwords with hello permissions you use toorun hello deployment script.</span></span> <span data-ttu-id="ee0db-194">如果您將憑證移動 hello 密碼存放區的金鑰保存庫中的指令碼，hello 密碼存放區`get certificate`命令也會輸出 hello hello.pfx 檔案的密碼。</span><span class="sxs-lookup"><span data-stu-id="ee0db-194">If you have a script that moves a certificate from hello secret store key vault, hello secret store `get certificate` command also outputs hello password of hello .pfx file.</span></span>
 
### <a name="how-does-hello-secrets-property-of-virtualmachineprofileosprofile-for-a-virtual-machine-scale-set-work-why-do-i-need-hello-sourcevault-value-when-i-have-toospecify-hello-absolute-uri-for-a-certificate-by-using-hello-certificateurl-property"></a><span data-ttu-id="ee0db-195">虛擬機器規模的 virtualMachineProfile.osProfile hello 機密屬性如何設定工作？</span><span class="sxs-lookup"><span data-stu-id="ee0db-195">How does hello Secrets property of virtualMachineProfile.osProfile for a virtual machine scale set work?</span></span> <span data-ttu-id="ee0db-196">當使用 hello certificateUrl 屬性 hello 憑證的絕對 URI 的 toospecify 為什麼需要 hello sourceVault 值？</span><span class="sxs-lookup"><span data-stu-id="ee0db-196">Why do I need hello sourceVault value when I have toospecify hello absolute URI for a certificate by using hello certificateUrl property?</span></span> 

<span data-ttu-id="ee0db-197">Windows 遠端管理 (WinRM) 憑證參考中必須要有 hello hello OS 設定檔的密碼屬性。</span><span class="sxs-lookup"><span data-stu-id="ee0db-197">A Windows Remote Management (WinRM) certificate reference must be present in hello Secrets property of hello OS profile.</span></span> 

<span data-ttu-id="ee0db-198">指出 hello 來源保存庫的 hello 目的是 tooenforce 存取控制清單 (ACL) 原則存在於使用者的 Azure 雲端服務模型中。</span><span class="sxs-lookup"><span data-stu-id="ee0db-198">hello purpose of indicating hello source vault is tooenforce access control list (ACL) policies that exist in a user's Azure Cloud Service model.</span></span> <span data-ttu-id="ee0db-199">如果未指定 hello 來源保存庫，沒有權限 toodeploy 或存取機密資料 tooa 金鑰保存庫的使用者將能夠 toothrough 計算資源提供者 (CRP)。</span><span class="sxs-lookup"><span data-stu-id="ee0db-199">If hello source vault isn't specified, users who do not have permissions toodeploy or access secrets tooa key vault would be able toothrough a Compute Resource Provider (CRP).</span></span> <span data-ttu-id="ee0db-200">甚至不存在的資源也會有 ACL。</span><span class="sxs-lookup"><span data-stu-id="ee0db-200">ACLs exist even for resources that do not exist.</span></span>

<span data-ttu-id="ee0db-201">如果您提供有效的金鑰保存庫 URL 但不正確的來源保存庫識別碼，輪詢 hello 作業時報告錯誤。</span><span class="sxs-lookup"><span data-stu-id="ee0db-201">If you provide an incorrect source vault ID but a valid key vault URL, an error is reported when you poll hello operation.</span></span>
 
### <a name="if-i-add-secrets-tooan-existing-virtual-machine-scale-set-are-hello-secrets-injected-into-existing-vms-or-only-into-new-ones"></a><span data-ttu-id="ee0db-202">如果我要加入現有的虛擬機器規模集的密碼 tooan，hello 機密資料插入到現有的 Vm，或只有新的嗎？</span><span class="sxs-lookup"><span data-stu-id="ee0db-202">If I add secrets tooan existing virtual machine scale set, are hello secrets injected into existing VMs, or only into new ones?</span></span> 

<span data-ttu-id="ee0db-203">憑證會加入 tooall Vm，即使預先存在的。</span><span class="sxs-lookup"><span data-stu-id="ee0db-203">Certificates are added tooall your VMs, even preexisting ones.</span></span> <span data-ttu-id="ee0db-204">如果您的虛擬機器規模集 upgradePolicy 屬性設定太**手動**，hello 憑證會新增 toohello VM，當您在 hello VM 上執行的手動更新。</span><span class="sxs-lookup"><span data-stu-id="ee0db-204">If your virtual machine scale set upgradePolicy property is set too**manual**, hello certificate is added toohello VM when you perform a manual update on hello VM.</span></span>
 
### <a name="where-do-i-put-certificates-for-linux-vms"></a><span data-ttu-id="ee0db-205">將 Linux VM 的憑證放在哪裡？</span><span class="sxs-lookup"><span data-stu-id="ee0db-205">Where do I put certificates for Linux VMs?</span></span>

<span data-ttu-id="ee0db-206">如何 toodeploy 憑證適用於 Linux Vm，請參閱的 toolearn[部署從客戶管理的金鑰保存庫憑證 tooVMs](https://blogs.technet.microsoft.com/kv/2015/07/14/deploy-certificates-to-vms-from-customer-managed-key-vault/)。</span><span class="sxs-lookup"><span data-stu-id="ee0db-206">toolearn how toodeploy certificates for Linux VMs, see [Deploy certificates tooVMs from a customer-managed key vault](https://blogs.technet.microsoft.com/kv/2015/07/14/deploy-certificates-to-vms-from-customer-managed-key-vault/).</span></span>
  
### <a name="how-do-i-add-a-new-vault-certificate-tooa-new-certificate-object"></a><span data-ttu-id="ee0db-207">如何新增新保存庫憑證 tooa 新憑證的物件？</span><span class="sxs-lookup"><span data-stu-id="ee0db-207">How do I add a new vault certificate tooa new certificate object?</span></span>

<span data-ttu-id="ee0db-208">tooadd 保存庫憑證 tooan 現有密碼，請參閱下列 PowerShell 範例 hello。</span><span class="sxs-lookup"><span data-stu-id="ee0db-208">tooadd a vault certificate tooan existing secret, see hello following PowerShell example.</span></span> <span data-ttu-id="ee0db-209">只使用一個密碼物件。</span><span class="sxs-lookup"><span data-stu-id="ee0db-209">Use only one secret object.</span></span>
 
```powershell
$newVaultCertificate = New-AzureRmVmssVaultCertificateConfig -CertificateStore MY -CertificateUrl https://sansunallapps1.vault.azure.net:443/secrets/dg-private-enc/55fa0332edc44a84ad655298905f1809
 
$vmss.VirtualMachineProfile.OsProfile.Secrets[0].VaultCertificates.Add($newVaultCertificate)
 
Update-AzureRmVmss -VirtualMachineScaleSet $vmss -ResourceGroup $rg -Name $vmssName
```
 
### <a name="what-happens-toocertificates-if-you-reimage-a-vm"></a><span data-ttu-id="ee0db-210">發生什麼情況 toocertificates VM 重新製作映像？</span><span class="sxs-lookup"><span data-stu-id="ee0db-210">What happens toocertificates if you reimage a VM?</span></span>

<span data-ttu-id="ee0db-211">如果您重新安裝 VM 映像，則會刪除憑證。</span><span class="sxs-lookup"><span data-stu-id="ee0db-211">If you reimage a VM, certificates are deleted.</span></span> <span data-ttu-id="ee0db-212">刪除 hello 整個作業系統磁碟重新安裝映像。</span><span class="sxs-lookup"><span data-stu-id="ee0db-212">Reimaging deletes hello entire OS disk.</span></span> 
 
### <a name="what-happens-if-you-delete-a-certificate-from-hello-key-vault"></a><span data-ttu-id="ee0db-213">如果您從 hello 金鑰保存庫刪除憑證，怎樣？</span><span class="sxs-lookup"><span data-stu-id="ee0db-213">What happens if you delete a certificate from hello key vault?</span></span>

<span data-ttu-id="ee0db-214">如果從 hello 金鑰保存庫中刪除 hello 密碼，然後執行`stop deallocate`為您的 Vm，然後再次啟動，您將遇到失敗。</span><span class="sxs-lookup"><span data-stu-id="ee0db-214">If hello secret is deleted from hello key vault, and then you run `stop deallocate` for all your VMs and then start them again, you will encounter a failure.</span></span> <span data-ttu-id="ee0db-215">hello 失敗發生因為 hello CRP 需要 tooretrieve hello 金鑰保存庫中的 hello 機密資料，但它不能。</span><span class="sxs-lookup"><span data-stu-id="ee0db-215">hello failure occurs because hello CRP needs tooretrieve hello secrets from hello key vault, but it cannot.</span></span> <span data-ttu-id="ee0db-216">在此案例中，您可以刪除 hello 憑證從 hello 虛擬機器規模集模型。</span><span class="sxs-lookup"><span data-stu-id="ee0db-216">In this scenario, you can delete hello certificates from hello virtual machine scale set model.</span></span> 

<span data-ttu-id="ee0db-217">hello CRP 元件不會保留客戶機密資料。</span><span class="sxs-lookup"><span data-stu-id="ee0db-217">hello CRP component does not persist customer secrets.</span></span> <span data-ttu-id="ee0db-218">如果您執行`stop deallocate`hello 虛擬機器規模集中的所有 vm，已刪除的 hello 快取。</span><span class="sxs-lookup"><span data-stu-id="ee0db-218">If you run `stop deallocate` for all VMs in hello virtual machine scale set, hello cache is deleted.</span></span> <span data-ttu-id="ee0db-219">在此案例中，從 hello 金鑰保存庫擷取密碼。</span><span class="sxs-lookup"><span data-stu-id="ee0db-219">In this scenario, secrets are retrieved from hello key vault.</span></span>

<span data-ttu-id="ee0db-220">向外延展，因為沒有快取的密碼的複本 hello Azure Service Fabric 中 （在 hello 單一網狀架構租用戶模型） 時，不會遇到這個問題。</span><span class="sxs-lookup"><span data-stu-id="ee0db-220">You don't encounter this problem when scaling out because there is a cached copy of hello secret in Azure Service Fabric (in hello single-fabric tenant model).</span></span>
 
### <a name="why-do-i-have-toospecify-hello-exact-location-for-hello-certificate-url-httpsname-of-hello-vaultvaultazurenet443secretsexact-location-as-indicated-in-service-fabric-cluster-security-scenarioshttpsazuremicrosoftcomdocumentationarticlesservice-fabric-cluster-security"></a><span data-ttu-id="ee0db-221">為什麼必須 hello 憑證 URL 的 toospecify hello 確切位置 (https://<name of hello vault>.vault.azure.net:443/secrets/<exact location>)，如下所示[Service Fabric 叢集安全性案例](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/)？</span><span class="sxs-lookup"><span data-stu-id="ee0db-221">Why do I have toospecify hello exact location for hello certificate URL (https://<name of hello vault>.vault.azure.net:443/secrets/<exact location>), as indicated in [Service Fabric cluster security scenarios](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/)?</span></span>
 
<span data-ttu-id="ee0db-222">hello Azure Key Vault 文件會指出該 hello 取得密碼 REST API 應傳回 hello hello 密碼的最新的版本，如果未指定 hello 版本。</span><span class="sxs-lookup"><span data-stu-id="ee0db-222">hello Azure Key Vault documentation states that hello Get Secret REST API should return hello latest version of hello secret if hello version is not specified.</span></span>
 
<span data-ttu-id="ee0db-223">方法</span><span class="sxs-lookup"><span data-stu-id="ee0db-223">Method</span></span> | <span data-ttu-id="ee0db-224">URL</span><span class="sxs-lookup"><span data-stu-id="ee0db-224">URL</span></span>
--- | ---
<span data-ttu-id="ee0db-225">GET</span><span class="sxs-lookup"><span data-stu-id="ee0db-225">GET</span></span> | <span data-ttu-id="ee0db-226">https://mykeyvault.vault.azure.net/secrets/{密碼-名稱}/{密碼-版本}?api-version={api-版本}</span><span class="sxs-lookup"><span data-stu-id="ee0db-226">https://mykeyvault.vault.azure.net/secrets/{secret-name}/{secret-version}?api-version={api-version}</span></span>

<span data-ttu-id="ee0db-227">取代 {*密碼名稱*} 與 hello 名稱取代 {*密碼-版本*} 想 tooretrieve hello 版本 hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="ee0db-227">Replace {*secret-name*} with hello name, and replace {*secret-version*} with hello version of hello secret you want tooretrieve.</span></span> <span data-ttu-id="ee0db-228">可能會排除 hello 密碼版本。</span><span class="sxs-lookup"><span data-stu-id="ee0db-228">hello secret version might be excluded.</span></span> <span data-ttu-id="ee0db-229">在此情況下，會擷取 hello 目前版本。</span><span class="sxs-lookup"><span data-stu-id="ee0db-229">In that case, hello current version is retrieved.</span></span>
  
### <a name="why-do-i-have-toospecify-hello-certificate-version-when-i-use-key-vault"></a><span data-ttu-id="ee0db-230">為什麼當我使用金鑰保存庫有 toospecify hello 憑證版本？</span><span class="sxs-lookup"><span data-stu-id="ee0db-230">Why do I have toospecify hello certificate version when I use Key Vault?</span></span>

<span data-ttu-id="ee0db-231">hello 目的 hello 金鑰保存庫需求 toospecify hello 憑證版本是的 toomake 它清除 toohello 使用者 Vm 上部署何種憑證。</span><span class="sxs-lookup"><span data-stu-id="ee0db-231">hello purpose of hello Key Vault requirement toospecify hello certificate version is toomake it clear toohello user what certificate is deployed on their VMs.</span></span>

<span data-ttu-id="ee0db-232">如果您建立的 VM，然後更新您的密碼在 hello 金鑰保存庫 hello 新憑證不是下載的 tooyour Vm。</span><span class="sxs-lookup"><span data-stu-id="ee0db-232">If you create a VM and then update your secret in hello key vault, hello new certificate is not downloaded tooyour VMs.</span></span> <span data-ttu-id="ee0db-233">但您的 Vm 會出現 tooreference，且新的 Vm 取得 hello 新密碼。</span><span class="sxs-lookup"><span data-stu-id="ee0db-233">But your VMs appear tooreference it, and new VMs get hello new secret.</span></span> <span data-ttu-id="ee0db-234">tooavoid，您會需要的 tooreference 密碼版本。</span><span class="sxs-lookup"><span data-stu-id="ee0db-234">tooavoid this, you are required tooreference a secret version.</span></span>

### <a name="my-team-works-with-several-certificates-that-are-distributed-toous-as-cer-public-keys-what-is-hello-recommended-approach-for-deploying-these-certificates-tooa-virtual-machine-scale-set"></a><span data-ttu-id="ee0db-235">我的小組會搭配幾個散發 toous 為.cer 公開金鑰的憑證。</span><span class="sxs-lookup"><span data-stu-id="ee0db-235">My team works with several certificates that are distributed toous as .cer public keys.</span></span> <span data-ttu-id="ee0db-236">什麼是建議的方法來部署這些憑證 tooa 虛擬機器規模集的 hello？</span><span class="sxs-lookup"><span data-stu-id="ee0db-236">What is hello recommended approach for deploying these certificates tooa virtual machine scale set?</span></span>

<span data-ttu-id="ee0db-237">toodeploy.cer 公開金鑰 tooa 虛擬機器規模集，您可以產生僅包含.cer 檔案的.pfx 檔案。</span><span class="sxs-lookup"><span data-stu-id="ee0db-237">toodeploy .cer public keys tooa virtual machine scale set, you can generate a .pfx file that contains only .cer files.</span></span> <span data-ttu-id="ee0db-238">toodo 此，請使用`X509ContentType = Pfx`。</span><span class="sxs-lookup"><span data-stu-id="ee0db-238">toodo this, use `X509ContentType = Pfx`.</span></span> <span data-ttu-id="ee0db-239">例如，當做 C# 或 PowerShell 中的 x509Certificate2 物件載入 hello.cer 檔案，然後呼叫 hello 方法。</span><span class="sxs-lookup"><span data-stu-id="ee0db-239">For example, load hello .cer file as an x509Certificate2 object in C# or PowerShell, and then call hello method.</span></span> 

<span data-ttu-id="ee0db-240">如需詳細資訊，請參閱 [X509Certificate.Export 方法 (X509ContentType, String)](https://msdn.microsoft.com/library/24ww6yzk(v=vs.110.aspx))。</span><span class="sxs-lookup"><span data-stu-id="ee0db-240">For more information, see [X509Certificate.Export Method (X509ContentType, String)](https://msdn.microsoft.com/library/24ww6yzk(v=vs.110.aspx)).</span></span>

### <a name="i-do-not-see-an-option-for-users-toopass-in-certificates-as-base64-strings-most-other-resource-providers-have-this-option"></a><span data-ttu-id="ee0db-241">我看不到憑證中的使用者 toopass 選項 base64 字串。</span><span class="sxs-lookup"><span data-stu-id="ee0db-241">I do not see an option for users toopass in certificates as base64 strings.</span></span> <span data-ttu-id="ee0db-242">大部分其他資源提供者都有這個選項。</span><span class="sxs-lookup"><span data-stu-id="ee0db-242">Most other resource providers have this option.</span></span>

<span data-ttu-id="ee0db-243">tooemulate 傳入做為 base64 字串憑證，您可以擷取 hello 最新版本 URL 中的資源管理員範本。</span><span class="sxs-lookup"><span data-stu-id="ee0db-243">tooemulate passing in a certificate as a base64 string, you can extract hello latest versioned URL in a Resource Manager template.</span></span> <span data-ttu-id="ee0db-244">包括下列資源管理員範本中的 JSON 屬性的 hello:</span><span class="sxs-lookup"><span data-stu-id="ee0db-244">Include hello following JSON property in your Resource Manager template:</span></span>

```json 
"certificateUrl": "[reference(resourceId(parameters('vaultResourceGroup'), 'Microsoft.KeyVault/vaults/secrets', parameters('vaultName'), parameters('secretName')), '2015-06-01').secretUriWithVersion]"
```
 
### <a name="do-i-have-toowrap-certificates-in-json-objects-in-key-vaults"></a><span data-ttu-id="ee0db-245">有金鑰保存庫中的 JSON 物件中 toowrap 憑證嗎？</span><span class="sxs-lookup"><span data-stu-id="ee0db-245">Do I have toowrap certificates in JSON objects in key vaults?</span></span>

<span data-ttu-id="ee0db-246">在虛擬機器擴展集和 VM 中，憑證必須包裝在 JSON 物件中。</span><span class="sxs-lookup"><span data-stu-id="ee0db-246">In virtual machine scale sets and VMs, certificates must be wrapped in JSON objects.</span></span> 

<span data-ttu-id="ee0db-247">我們也支援 hello 內容類型的應用程式/x-pkcs12。</span><span class="sxs-lookup"><span data-stu-id="ee0db-247">We also support hello content type application/x-pkcs12.</span></span> <span data-ttu-id="ee0db-248">如需使用 application/x-pkcs12 的相關指示，請參閱 [Azure Key Vault 中的 PFX 憑證](http://www.rahulpnath.com/blog/pfx-certificate-in-azure-key-vault/)。</span><span class="sxs-lookup"><span data-stu-id="ee0db-248">For instructions on using application/x-pkcs12, see [PFX certificates in Azure Key Vault](http://www.rahulpnath.com/blog/pfx-certificate-in-azure-key-vault/).</span></span>
 
<span data-ttu-id="ee0db-249">我們目前不支援 .cer 檔案。</span><span class="sxs-lookup"><span data-stu-id="ee0db-249">We currently do not support .cer files.</span></span> <span data-ttu-id="ee0db-250">toouse.cer 檔案，將它們匯出到.pfx 容器。</span><span class="sxs-lookup"><span data-stu-id="ee0db-250">toouse .cer files, export them into .pfx containers.</span></span>



## <a name="compliance"></a><span data-ttu-id="ee0db-251">法規遵循</span><span class="sxs-lookup"><span data-stu-id="ee0db-251">Compliance</span></span>

### <a name="are-virtual-machine-scale-sets-pci-compliant"></a><span data-ttu-id="ee0db-252">虛擬機器擴展集符合 PCI 規範嗎？</span><span class="sxs-lookup"><span data-stu-id="ee0db-252">Are virtual machine scale sets PCI-compliant?</span></span>

<span data-ttu-id="ee0db-253">虛擬機器擴展集是之上 hello CRP 精簡型的應用程式開發介面層級。</span><span class="sxs-lookup"><span data-stu-id="ee0db-253">Virtual machine scale sets are a thin API layer on top of hello CRP.</span></span> <span data-ttu-id="ee0db-254">兩個元件均 hello Azure 服務樹狀目錄中的 hello 運算平台的一部分。</span><span class="sxs-lookup"><span data-stu-id="ee0db-254">Both components are part of hello compute platform in hello Azure service tree.</span></span>

<span data-ttu-id="ee0db-255">相容性的觀點而言，虛擬機器擴展集是 hello Azure 運算平台的基礎部分。</span><span class="sxs-lookup"><span data-stu-id="ee0db-255">From a compliance perspective, virtual machine scale sets are a fundamental part of hello Azure compute platform.</span></span> <span data-ttu-id="ee0db-256">它們 hello CRP 本身的情況下，共用小組、 工具、 處理程序、 部署方法，安全性控制，在 just-in-time (JIT) 編譯、 監視、 警示與等等。</span><span class="sxs-lookup"><span data-stu-id="ee0db-256">They share a team, tools, processes, deployment methodology, security controls, just-in-time (JIT) compilation, monitoring, alerting, and so on, with hello CRP itself.</span></span> <span data-ttu-id="ee0db-257">虛擬機器擴展集是付款卡產業 (PCI)-因為 hello CRP 屬於 hello 目前 PCI 資料安全標準 (DSS) 情況證明相容。</span><span class="sxs-lookup"><span data-stu-id="ee0db-257">Virtual machine scale sets are Payment Card Industry (PCI)-compliant because hello CRP is part of hello current PCI Data Security Standard (DSS) attestation.</span></span>

<span data-ttu-id="ee0db-258">如需詳細資訊，請參閱[hello Microsoft 信任中心](https://www.microsoft.com/TrustCenter/Compliance/PCI)。</span><span class="sxs-lookup"><span data-stu-id="ee0db-258">For more information, see [hello Microsoft Trust Center](https://www.microsoft.com/TrustCenter/Compliance/PCI).</span></span>






## <a name="extensions"></a><span data-ttu-id="ee0db-259">擴充功能</span><span class="sxs-lookup"><span data-stu-id="ee0db-259">Extensions</span></span>

### <a name="how-do-i-delete-a-virtual-machine-scale-set-extension"></a><span data-ttu-id="ee0db-260">如何刪除虛擬機器擴展集擴充功能？</span><span class="sxs-lookup"><span data-stu-id="ee0db-260">How do I delete a virtual machine scale set extension?</span></span>

<span data-ttu-id="ee0db-261">toodelete 的虛擬機器擴展集延伸模組，使用下列 PowerShell 範例的 hello:</span><span class="sxs-lookup"><span data-stu-id="ee0db-261">toodelete a virtual machine scale set extension, use hello following PowerShell example:</span></span>

```powershell
$vmss = Get-AzureRmVmss -ResourceGroupName "resource_group_name" -VMScaleSetName "vmssName" 

$vmss=Remove-AzureRmVmssExtension -VirtualMachineScaleSet $vmss -Name "extensionName"

Update-AzureRmVmss -ResourceGroupName "resource_group_name" -VMScaleSetName "vmssName" -VirtualMacineScaleSet $vmss
```
 
<span data-ttu-id="ee0db-262">您可以找到中的 hello extensionName 值`$vmss`。</span><span class="sxs-lookup"><span data-stu-id="ee0db-262">You can find hello extensionName value in `$vmss`.</span></span>
   
### <a name="is-there-a-virtual-machine-scale-set-template-example-that-integrates-with-operations-management-suite"></a><span data-ttu-id="ee0db-263">是否有與 Operations Management Suite 整合的虛擬機器擴展集範本範例？</span><span class="sxs-lookup"><span data-stu-id="ee0db-263">Is there a virtual machine scale set template example that integrates with Operations Management Suite?</span></span>

<span data-ttu-id="ee0db-264">虛擬機器擴展集整合與 Operations Management Suite 的範本範例，請參閱中的 hello 第二個範例[部署 Azure Service Fabric 叢集，並啟用監視，可使用記錄分析](https://github.com/krnese/AzureDeploy/tree/master/OMS/MSOMS/ServiceFabric)。</span><span class="sxs-lookup"><span data-stu-id="ee0db-264">For a virtual machine scale set template example that integrates with Operations Management Suite, see hello second example in [Deploy an Azure Service Fabric cluster and enable monitoring by using Log Analytics](https://github.com/krnese/AzureDeploy/tree/master/OMS/MSOMS/ServiceFabric).</span></span>
   
### <a name="extensions-seem-toorun-in-parallel-on-virtual-machine-scale-sets-this-causes-my-custom-script-extension-toofail-what-can-i-do-toofix-this"></a><span data-ttu-id="ee0db-265">延伸模組看起來 toorun 以平行方式上的虛擬機器規模集。</span><span class="sxs-lookup"><span data-stu-id="ee0db-265">Extensions seem toorun in parallel on virtual machine scale sets.</span></span> <span data-ttu-id="ee0db-266">這會導致我的自訂指令碼延伸 toofail。</span><span class="sxs-lookup"><span data-stu-id="ee0db-266">This causes my custom script extension toofail.</span></span> <span data-ttu-id="ee0db-267">怎麼 toofix 這？</span><span class="sxs-lookup"><span data-stu-id="ee0db-267">What can I do toofix this?</span></span>

<span data-ttu-id="ee0db-268">請參閱 < 關於虛擬機器擴展集，在擴充功能順序 toolearn[在 Azure 虛擬機器擴展集延伸模組排序](https://msftstack.wordpress.com/2016/05/12/extension-sequencing-in-azure-vm-scale-sets/)。</span><span class="sxs-lookup"><span data-stu-id="ee0db-268">toolearn about extension sequencing in virtual machine scale sets, see [Extension sequencing in Azure virtual machine scale sets](https://msftstack.wordpress.com/2016/05/12/extension-sequencing-in-azure-vm-scale-sets/).</span></span>
 
 
### <a name="how-do-i-reset-hello-password-for-vms-in-my-virtual-machine-scale-set"></a><span data-ttu-id="ee0db-269">如何重設 hello 密碼對於 Vm 在我的虛擬機器規模集？</span><span class="sxs-lookup"><span data-stu-id="ee0db-269">How do I reset hello password for VMs in my virtual machine scale set?</span></span>

<span data-ttu-id="ee0db-270">Vm 的虛擬機器規模的 tooreset hello 密碼設定，請使用 VM 存取擴充功能。</span><span class="sxs-lookup"><span data-stu-id="ee0db-270">tooreset hello password for VMs in your virtual machine scale set, use VM access extensions.</span></span> 

<span data-ttu-id="ee0db-271">使用下列 PowerShell 範例 hello:</span><span class="sxs-lookup"><span data-stu-id="ee0db-271">Use hello following PowerShell example:</span></span>

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
 
 
### <a name="how-do-i-add-an-extension-tooall-vms-in-my-virtual-machine-scale-set"></a><span data-ttu-id="ee0db-272">如何在我的虛擬機器規模集中新增擴充功能 tooall Vm？</span><span class="sxs-lookup"><span data-stu-id="ee0db-272">How do I add an extension tooall VMs in my virtual machine scale set?</span></span>

<span data-ttu-id="ee0db-273">如果更新原則設定太**自動**，重新部署的 hello 新延伸模組屬性的 hello 範本更新所有 Vm。</span><span class="sxs-lookup"><span data-stu-id="ee0db-273">If update policy is set too**automatic**, redeploying hello template with hello new extension properties updates all VMs.</span></span>

<span data-ttu-id="ee0db-274">如果更新原則設定太**手動**，第一次更新 hello 副檔名，並以手動方式更新您的 Vm 中的所有執行個體。</span><span class="sxs-lookup"><span data-stu-id="ee0db-274">If update policy is set too**manual**, first update hello extension, and then manually update all instances in your VMs.</span></span>

  
### <a name="if-hello-extensions-associated-with-an-existing-virtual-machine-scale-set-are-updated-are-existing-vms-affected-that-is-will-hello-vms-not-match-hello-virtual-machine-scale-set-model-or-are-they-ignored-when-an-existing-machine-is-service-healed-or-reimaged-are-hello-scripts-that-are-currently-configured-on-hello-virtual-machine-scale-set-executed-or-are-hello-scripts-that-were-configured-when-hello-vm-was-first-created-used"></a><span data-ttu-id="ee0db-275">Hello 與現有的虛擬機器規模集相關聯的延伸模組更新時，如果現有的 Vm 會受到影響？</span><span class="sxs-lookup"><span data-stu-id="ee0db-275">If hello extensions associated with an existing virtual machine scale set are updated, are existing VMs affected?</span></span> <span data-ttu-id="ee0db-276">(也就是將 hello Vm*不*相符 hello 虛擬機器擴充集模型嗎？)或者會忽略它們？</span><span class="sxs-lookup"><span data-stu-id="ee0db-276">(That is, will hello VMs *not* match hello virtual machine scale set model?) Or are they ignored?</span></span> <span data-ttu-id="ee0db-277">當現有的機器是服務修復或重新安裝映像時，會 hello hello 虛擬機器規模集執行，目前設定的指令碼或 hello 指令碼已設定使用時，會先建立 VM 的 hello？</span><span class="sxs-lookup"><span data-stu-id="ee0db-277">When an existing machine is service-healed or reimaged, are hello scripts that are currently configured on hello virtual machine scale set executed, or are hello scripts that were configured when hello VM was first created used?</span></span>

<span data-ttu-id="ee0db-278">如果 hello 延伸定義在 hello 虛擬機器擴展集模型已更新，而且 hello upgradePolicy 屬性設定太**自動**，它會更新 hello Vm。</span><span class="sxs-lookup"><span data-stu-id="ee0db-278">If hello extension definition in hello virtual machine scale set model is updated and hello upgradePolicy property is set too**automatic**, it updates hello VMs.</span></span> <span data-ttu-id="ee0db-279">如果 hello upgradePolicy 屬性設定太**手動**，延伸模組已標示為不符合 hello 模型。</span><span class="sxs-lookup"><span data-stu-id="ee0db-279">If hello upgradePolicy property is set too**manual**, extensions are flagged as not matching hello model.</span></span> 

<span data-ttu-id="ee0db-280">如果服務修復現有的 VM，它會顯示為重新開機，並 hello 擴充功能不會重新執行。</span><span class="sxs-lookup"><span data-stu-id="ee0db-280">If an existing VM is service-healed, it appears as a reboot, and hello extensions are not rerun.</span></span> <span data-ttu-id="ee0db-281">如果它的映像後，就像是 hello 作業系統磁碟機取代 hello 來源映像。</span><span class="sxs-lookup"><span data-stu-id="ee0db-281">If it is reimaged, it's like replacing hello OS drive with hello source image.</span></span> <span data-ttu-id="ee0db-282">執行從 hello 最新的模型，例如延伸模組的任何特製化。</span><span class="sxs-lookup"><span data-stu-id="ee0db-282">Any specialization from hello latest model, such as extensions, are run.</span></span>
 
### <a name="how-do-i-join-a-virtual-machine-scale-set-tooan-azure-ad-domain"></a><span data-ttu-id="ee0db-283">如何將虛擬機器規模集 tooan Azure AD 網域的聯結？</span><span class="sxs-lookup"><span data-stu-id="ee0db-283">How do I join a virtual machine scale set tooan Azure AD domain?</span></span>

<span data-ttu-id="ee0db-284">toojoin 虛擬機器規模集 tooan Azure Active Directory (Azure AD) 網域，您可以定義擴充功能。</span><span class="sxs-lookup"><span data-stu-id="ee0db-284">toojoin a virtual machine scale set tooan Azure Active Directory (Azure AD) domain, you can define an extension.</span></span> 

<span data-ttu-id="ee0db-285">toodefine 擴充功能，使用 hello JsonADDomainExtension 屬性：</span><span class="sxs-lookup"><span data-stu-id="ee0db-285">toodefine an extension, use hello JsonADDomainExtension property:</span></span>

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
 
### <a name="my-virtual-machine-scale-set-extension-is-trying-tooinstall-something-that-requires-a-reboot-for-example-commandtoexecute-powershellexe--executionpolicy-unrestricted-install-windowsfeature-name-fs-resource-manager-includemanagementtools"></a><span data-ttu-id="ee0db-286">我的虛擬機器規模集擴充功能正嘗試 tooinstall 而需要重新開機的項目。</span><span class="sxs-lookup"><span data-stu-id="ee0db-286">My virtual machine scale set extension is trying tooinstall something that requires a reboot.</span></span> <span data-ttu-id="ee0db-287">例如："commandToExecute": "powershell.exe -ExecutionPolicy Unrestricted Install-WindowsFeature –Name FS-Resource-Manager –IncludeManagementTools"</span><span class="sxs-lookup"><span data-stu-id="ee0db-287">For example, "commandToExecute": "powershell.exe -ExecutionPolicy Unrestricted Install-WindowsFeature –Name FS-Resource-Manager –IncludeManagementTools"</span></span>

<span data-ttu-id="ee0db-288">如果虛擬機器規模集擴充功能會嘗試 tooinstall 而需要重新開機的項目，您可以使用 hello Azure 自動化 Desired State Configuration (Automation DSC) 的延伸模組。</span><span class="sxs-lookup"><span data-stu-id="ee0db-288">If your virtual machine scale set extension is trying tooinstall something that requires a reboot, you can use hello Azure Automation Desired State Configuration (Automation DSC) extension.</span></span> <span data-ttu-id="ee0db-289">如果 hello 作業系統是 Windows Server 2012 R2，Azure 會提取在 hello Windows Management Framework (WMF) 5.0 安裝程式中重新開機，然後再繼續執行 hello 組態。</span><span class="sxs-lookup"><span data-stu-id="ee0db-289">If hello operating system is Windows Server 2012 R2, Azure pulls in hello Windows Management Framework (WMF) 5.0 setup, reboots, and then continues with hello configuration.</span></span> 
 
### <a name="how-do-i-turn-on-antimalware-in-my-virtual-machine-scale-set"></a><span data-ttu-id="ee0db-290">如何在虛擬機器擴展集中開啟反惡意程式碼？</span><span class="sxs-lookup"><span data-stu-id="ee0db-290">How do I turn on antimalware in my virtual machine scale set?</span></span>

<span data-ttu-id="ee0db-291">tooturn 虛擬機器的標尺上的反惡意程式碼上設定，請使用下列 PowerShell 範例 hello:</span><span class="sxs-lookup"><span data-stu-id="ee0db-291">tooturn on antimalware on your virtual machine scale set, use hello following PowerShell example:</span></span>

```powershell
$rgname = 'autolap'
$vmssname = 'autolapbr'
$location = 'eastus'
 
# Retrieve hello most recent version number of hello extension.
$allVersions= (Get-AzureRmVMExtensionImage -Location $location -PublisherName "Microsoft.Azure.Security" -Type "IaaSAntimalware").Version
$versionString = $allVersions[($allVersions.count)-1].Split(".")[0] + "." + $allVersions[($allVersions.count)-1].Split(".")[1]
 
$VMSS = Get-AzureRmVmss -ResourceGroupName $rgname -VMScaleSetName $vmssname
echo $VMSS
Add-AzureRmVmssExtension -VirtualMachineScaleSet $VMSS -Name "IaaSAntimalware" -Publisher "Microsoft.Azure.Security" -Type "IaaSAntimalware" -TypeHandlerVersion $versionString
Update-AzureRmVmss -ResourceGroupName $rgname -Name $vmssname -VirtualMachineScaleSet $VMSS 
```

### <a name="i-need-tooexecute-a-custom-script-thats-hosted-in-a-private-storage-account-hello-script-runs-successfully-when-hello-storage-is-public-but-when-i-try-toouse-a-shared-access-signature-sas-it-fails-this-message-is-displayed-missing-mandatory-parameters-for-valid-shared-access-signature-linksas-works-fine-from-my-local-browser"></a><span data-ttu-id="ee0db-292">我需要 tooexecute 裝載在私人儲存體帳戶中之自訂指令碼。</span><span class="sxs-lookup"><span data-stu-id="ee0db-292">I need tooexecute a custom script that's hosted in a private storage account.</span></span> <span data-ttu-id="ee0db-293">hello 指令碼順利執行時 hello 儲存體是公用的但是當我嘗試 toouse 共用存取簽章 (SAS)，它將會失敗。</span><span class="sxs-lookup"><span data-stu-id="ee0db-293">hello script runs successfully when hello storage is public, but when I try toouse a Shared Access Signature (SAS), it fails.</span></span> <span data-ttu-id="ee0db-294">隨即顯示此訊息：「遺漏有效的共用存取簽章的強制參數」。</span><span class="sxs-lookup"><span data-stu-id="ee0db-294">This message is displayed: “Missing mandatory parameters for valid Shared Access Signature”.</span></span> <span data-ttu-id="ee0db-295">Link+SAS 可從我的本機瀏覽器正常運作。</span><span class="sxs-lookup"><span data-stu-id="ee0db-295">Link+SAS works fine from my local browser.</span></span>

<span data-ttu-id="ee0db-296">tooexecute 裝載在私人儲存體帳戶之自訂指令碼會設定與 hello 儲存體帳戶金鑰和名稱的受保護的設定。</span><span class="sxs-lookup"><span data-stu-id="ee0db-296">tooexecute a custom script that's hosted in a private storage account, set up protected settings with hello storage account key and name.</span></span> <span data-ttu-id="ee0db-297">如需詳細資訊，請參閱[適用於 Windows 的自訂指令碼擴充功能](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-extensions-customscript/#template-example-for-a-windows-vm-with-protected-settings)。</span><span class="sxs-lookup"><span data-stu-id="ee0db-297">For more information, see [Custom Script Extension for Windows](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-extensions-customscript/#template-example-for-a-windows-vm-with-protected-settings).</span></span>







## <a name="networking"></a><span data-ttu-id="ee0db-298">網路</span><span class="sxs-lookup"><span data-stu-id="ee0db-298">Networking</span></span>
 
### <a name="is-it-possible-tooassign-a-network-security-group-nsg-tooa-scale-set-so-that-it-will-apply-tooall-hello-vm-nics-in-hello-set"></a><span data-ttu-id="ee0db-299">是否可能 tooassign 網路安全性群組 (NSG) tooa 縮放設定，讓它將會套用在 hello 集中 tooall hello VM Nic？</span><span class="sxs-lookup"><span data-stu-id="ee0db-299">Is it possible tooassign a Network Security Group (NSG) tooa scale set, so that it will apply tooall hello VM NICs in hello set?</span></span>

<span data-ttu-id="ee0db-300">是。</span><span class="sxs-lookup"><span data-stu-id="ee0db-300">Yes.</span></span> <span data-ttu-id="ee0db-301">直接 tooa 規模調整集合參考 hello networkInterfaceConfigurations hello 網路設定檔 區段中，可以套用網路安全性群組。</span><span class="sxs-lookup"><span data-stu-id="ee0db-301">A Network Security Group can be applied directly tooa scale set by referencing it in hello networkInterfaceConfigurations section of hello network profile.</span></span> <span data-ttu-id="ee0db-302">範例：</span><span class="sxs-lookup"><span data-stu-id="ee0db-302">Example:</span></span>

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

### <a name="how-do-i-do-a-vip-swap-for-virtual-machine-scale-sets-in-hello-same-subscription-and-same-region"></a><span data-ttu-id="ee0db-303">如何進行 VIP 交換的虛擬機器規模集中 hello 相同訂用帳戶和相同的區域？</span><span class="sxs-lookup"><span data-stu-id="ee0db-303">How do I do a VIP swap for virtual machine scale sets in hello same subscription and same region?</span></span>

<span data-ttu-id="ee0db-304">如果您有兩個虛擬機器規模設定具有 Azure 負載平衡器前端，而且它們處於 hello 相同訂用帳戶和地區，您無法取消配置每個從 hello 公用 IP 位址，並指派其他 toohello。</span><span class="sxs-lookup"><span data-stu-id="ee0db-304">If you have two virtual machine scale sets with Azure Load Balancer front-ends, and they are in hello same subscription and region, you could deallocate hello public IP addresses from each one, and assign toohello other.</span></span> <span data-ttu-id="ee0db-305">例如，請參閱 [VIP 交換：Azure Resource Manager 中藍綠色版本部署](https://msftstack.wordpress.com/2017/02/24/vip-swap-blue-green-deployment-in-azure-resource-manager/) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="ee0db-305">See [VIP Swap: Blue-green deployment in Azure Resource Manager](https://msftstack.wordpress.com/2017/02/24/vip-swap-blue-green-deployment-in-azure-resource-manager/) for example.</span></span> <span data-ttu-id="ee0db-306">雖然 hello 資源會取消配置/配置在 hello 網路層級意味著延遲。</span><span class="sxs-lookup"><span data-stu-id="ee0db-306">This does imply a delay though as hello resources are deallocated/allocated at hello network level.</span></span> <span data-ttu-id="ee0db-307">更快的選項是使用兩個後端集區和路由規則 toouse Azure 應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="ee0db-307">A faster option is toouse Azure Application Gateway with two backend pools, and a routing rule.</span></span> <span data-ttu-id="ee0db-308">或者，您可以透過 [Azure App Service](https://azure.microsoft.com/en-us/services/app-service/) 裝載應用程式，以提供在預備與生產位置之間快速切換的支援。</span><span class="sxs-lookup"><span data-stu-id="ee0db-308">Alternatively, you could host your application with [Azure App service](https://azure.microsoft.com/en-us/services/app-service/) which provides support for fast switching between staging and production slots.</span></span>
 
### <a name="how-do-i-specify-a-range-of-private-ip-addresses-toouse-for-static-private-ip-address-allocation"></a><span data-ttu-id="ee0db-309">如何指定的私人 IP 位址 toouse 靜態私人 IP 位址配置的範圍？</span><span class="sxs-lookup"><span data-stu-id="ee0db-309">How do I specify a range of private IP addresses toouse for static private IP address allocation?</span></span>

<span data-ttu-id="ee0db-310">系統會從您指定的子網路選取 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="ee0db-310">IP addresses are selected from a subnet that you specify.</span></span> 

<span data-ttu-id="ee0db-311">hello 配置方法的虛擬機器規模集的 IP 位址永遠是 「 動態 」，但這並不表示這些 IP 位址，可以變更。</span><span class="sxs-lookup"><span data-stu-id="ee0db-311">hello allocation method of virtual machine scale set IP addresses is always “dynamic,” but that doesn't mean that these IP addresses can change.</span></span> <span data-ttu-id="ee0db-312">在此情況下，「 動態 」 只表示您沒有在 PUT 要求中指定 hello IP 位址。</span><span class="sxs-lookup"><span data-stu-id="ee0db-312">In this case, "dynamic" only means that you do not specify hello IP address in a PUT request.</span></span> <span data-ttu-id="ee0db-313">指定 hello 靜態使用 hello 子網路設定。</span><span class="sxs-lookup"><span data-stu-id="ee0db-313">Specify hello static set by using hello subnet.</span></span> 
    
### <a name="how-do-i-deploy-a-virtual-machine-scale-set-tooan-existing-azure-virtual-network"></a><span data-ttu-id="ee0db-314">我要如何部署虛擬機器規模集 tooan 現有 Azure 虛擬網路？</span><span class="sxs-lookup"><span data-stu-id="ee0db-314">How do I deploy a virtual machine scale set tooan existing Azure virtual network?</span></span> 

<span data-ttu-id="ee0db-315">toodeploy 的虛擬機器擴展集 tooan 現有的 Azure 虛擬網路，請參閱[部署虛擬機器規模集 tooan 現有虛擬網路](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-existing-vnet)。</span><span class="sxs-lookup"><span data-stu-id="ee0db-315">toodeploy a virtual machine scale set tooan existing Azure virtual network, see [Deploy a virtual machine scale set tooan existing virtual network](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-existing-vnet).</span></span> 

### <a name="how-do-i-add-hello-ip-address-of-hello-first-vm-in-a-virtual-machine-scale-set-toohello-output-of-a-template"></a><span data-ttu-id="ee0db-316">如何新增 hello IP 位址第一個 VM 中的虛擬機器擴展集 toohello 範本輸出的 hello？</span><span class="sxs-lookup"><span data-stu-id="ee0db-316">How do I add hello IP address of hello first VM in a virtual machine scale set toohello output of a template?</span></span>

<span data-ttu-id="ee0db-317">hello tooadd hello IP 位址第一個 VM 範本時，虛擬機器規模集 toohello 輸出中的看到[ARM： 取得 VMSS 私用 Ip](http://stackoverflow.com/questions/42790392/arm-get-vmsss-private-ips)。</span><span class="sxs-lookup"><span data-stu-id="ee0db-317">tooadd hello IP address of hello first VM in a virtual machine scale set toohello output of a template, see [ARM: Get VMSS's private IPs](http://stackoverflow.com/questions/42790392/arm-get-vmsss-private-ips).</span></span>

### <a name="can-i-use-scale-sets-with-accelerated-networking"></a><span data-ttu-id="ee0db-318">我可以搭配加速的網路使用擴展集嗎？</span><span class="sxs-lookup"><span data-stu-id="ee0db-318">Can I use scale sets with Accelerated Networking?</span></span>

<span data-ttu-id="ee0db-319">是。</span><span class="sxs-lookup"><span data-stu-id="ee0db-319">Yes.</span></span> <span data-ttu-id="ee0db-320">網路功能，加速 toouse enableAcceleratedNetworking tootrue 在設定中設定您的標尺集的 networkInterfaceConfigurations。</span><span class="sxs-lookup"><span data-stu-id="ee0db-320">toouse accelerated networking, set enableAcceleratedNetworking tootrue in your scale set's networkInterfaceConfigurations settings.</span></span> <span data-ttu-id="ee0db-321">例如</span><span class="sxs-lookup"><span data-stu-id="ee0db-321">E.g.</span></span>
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

### <a name="how-can-i-configure-hello-dns-servers-used-by-a-scale-set"></a><span data-ttu-id="ee0db-322">如何設定規模集所使用的 hello DNS 伺服器？</span><span class="sxs-lookup"><span data-stu-id="ee0db-322">How can I configure hello DNS servers used by a scale set?</span></span>

<span data-ttu-id="ee0db-323">toocreate VM 規模調整設定自訂的 DNS 設定，並將 dnsSettings JSON 封包 toohello 規模調整集合 networkInterfaceConfigurations > 一節。</span><span class="sxs-lookup"><span data-stu-id="ee0db-323">toocreate a VM scale set with a custom DNS configuration, add a dnsSettings JSON packet toohello scale set networkInterfaceConfigurations section.</span></span> <span data-ttu-id="ee0db-324">範例：</span><span class="sxs-lookup"><span data-stu-id="ee0db-324">Example:</span></span>
```json
    "dnsSettings":{
        "dnsServers":["10.0.0.6", "10.0.0.5"]
    }
```

### <a name="how-can-i-configure-a-scale-set-tooassign-a-public-ip-address-tooeach-vm"></a><span data-ttu-id="ee0db-325">我要如何設定公用 IP 位址 tooeach VM 規模集 tooassign？</span><span class="sxs-lookup"><span data-stu-id="ee0db-325">How can I configure a scale set tooassign a public IP address tooeach VM?</span></span>

<span data-ttu-id="ee0db-326">toocreate VM 規模調整集合，會將指派的公用 IP 位址 tooeach VM，請確定 hello API 版的 hello Microsoft.Compute/virtualMAchineScaleSets 資源 2017年-03-30，並新增_publicipaddressconfiguration_ JSON 封包toohello 規模調整集合 ipConfigurations > 一節。</span><span class="sxs-lookup"><span data-stu-id="ee0db-326">toocreate a VM scale set that assigns a public IP address tooeach VM, make sure hello API version of hello Microsoft.Compute/virtualMAchineScaleSets resource is 2017-03-30, and add a _publicipaddressconfiguration_ JSON packet toohello scale set ipConfigurations section.</span></span> <span data-ttu-id="ee0db-327">範例：</span><span class="sxs-lookup"><span data-stu-id="ee0db-327">Example:</span></span>

```json
    "publicipaddressconfiguration": {
        "name": "pub1",
        "properties": {
        "idleTimeoutInMinutes": 15
        }
    }
```

### <a name="can-i-configure-a-scale-set-toowork-with-multiple-application-gateways"></a><span data-ttu-id="ee0db-328">可以與多個應用程式閘道設定小數位數組 toowork 嗎？</span><span class="sxs-lookup"><span data-stu-id="ee0db-328">Can I configure a scale set toowork with multiple Application Gateways?</span></span>

<span data-ttu-id="ee0db-329">是。</span><span class="sxs-lookup"><span data-stu-id="ee0db-329">Yes.</span></span> <span data-ttu-id="ee0db-330">您可以加入 hello 資源識別碼的多個應用程式閘道後端位址集區 toohello _applicationGatewayBackendAddressPools_列入 hello _ipConfigurations_規模集的區段網路設定檔。</span><span class="sxs-lookup"><span data-stu-id="ee0db-330">You can add hello resource id's for multiple Application Gateway backend address pools toohello _applicationGatewayBackendAddressPools_ list in hello _ipConfigurations_ section of your scale set network profile.</span></span>

## <a name="scale"></a><span data-ttu-id="ee0db-331">調整</span><span class="sxs-lookup"><span data-stu-id="ee0db-331">Scale</span></span>

### <a name="in-what-case-would-i-create-a-virtual-machine-scale-set-with-fewer-than-two-vms"></a><span data-ttu-id="ee0db-332">在何種情況下，我會建立具有兩部以下 VM 的虛擬機器擴展集？</span><span class="sxs-lookup"><span data-stu-id="ee0db-332">In what case would I create a virtual machine scale set with fewer than two VMs?</span></span>

<span data-ttu-id="ee0db-333">其中一個原因 toocreate 的虛擬機器擴展集少於兩個 Vm 會 toouse hello 彈性屬性的虛擬機器規模設定。</span><span class="sxs-lookup"><span data-stu-id="ee0db-333">One reason toocreate a virtual machine scale set with fewer than two VMs would be toouse hello elastic properties of a virtual machine scale set.</span></span> <span data-ttu-id="ee0db-334">比方說，您無法部署虛擬機器規模集與零 Vm toodefine 基礎結構而不必付出 VM 執行成本。</span><span class="sxs-lookup"><span data-stu-id="ee0db-334">For example, you could deploy a virtual machine scale set with zero VMs toodefine your infrastructure without paying VM running costs.</span></span> <span data-ttu-id="ee0db-335">然後，當您準備好 toodeploy Vm，增加 hello 「 容量 」 的 hello 虛擬機器擴充集 toohello 生產執行個體計數。</span><span class="sxs-lookup"><span data-stu-id="ee0db-335">Then, when you are ready toodeploy VMs, increase hello “capacity” of hello virtual machine scale set toohello production instance count.</span></span>

<span data-ttu-id="ee0db-336">建立具有兩部以下 VM 的虛擬機器擴展集的另一個原因，就是相較於使用具有離散 VM 的可用性設定組，您可能比較不擔心可用性。</span><span class="sxs-lookup"><span data-stu-id="ee0db-336">Another reason you might create a virtual machine scale set with fewer than two VMs is if you're concerned less with availability than in using an availability set with discrete VMs.</span></span> <span data-ttu-id="ee0db-337">虛擬機器擴展集可讓您使用無的計算的單位，可替代方式 toowork。</span><span class="sxs-lookup"><span data-stu-id="ee0db-337">Virtual machine scale sets give you a way toowork with undifferentiated compute units that are fungible.</span></span> <span data-ttu-id="ee0db-338">此種一致性是虛擬機器擴展集與可用性設定組的關鍵區別指標。</span><span class="sxs-lookup"><span data-stu-id="ee0db-338">This uniformity is a key differentiator for virtual machine scale sets versus availability sets.</span></span> <span data-ttu-id="ee0db-339">許多無狀態的工作負載都不會追蹤個別的單位。</span><span class="sxs-lookup"><span data-stu-id="ee0db-339">Many stateless workloads do not track individual units.</span></span> <span data-ttu-id="ee0db-340">Hello 工作負載會卸除，您可以縮小 tooone 計算單位，並再 toomany 向上延展 hello 工作負載增加時。</span><span class="sxs-lookup"><span data-stu-id="ee0db-340">If hello workload drops, you can scale down tooone compute unit, and then scale up toomany when hello workload increases.</span></span>

### <a name="how-do-i-change-hello-number-of-vms-in-a-virtual-machine-scale-set"></a><span data-ttu-id="ee0db-341">如何變更虛擬機器規模集中的 Vm hello 數目？</span><span class="sxs-lookup"><span data-stu-id="ee0db-341">How do I change hello number of VMs in a virtual machine scale set?</span></span>

<span data-ttu-id="ee0db-342">toochange hello 數目 Vm 規模集中的虛擬機器，請參閱[變更 hello 的虛擬機器規模集的執行個體計數](https://msftstack.wordpress.com/2016/05/13/change-the-instance-count-of-an-azure-vm-scale-set/)。</span><span class="sxs-lookup"><span data-stu-id="ee0db-342">toochange hello number of VMs in a virtual machine scale set, see [Change hello instance count of a virtual machine scale set](https://msftstack.wordpress.com/2016/05/13/change-the-instance-count-of-an-azure-vm-scale-set/).</span></span>

### <a name="how-do-i-define-custom-alerts-for-when-certain-thresholds-are-reached"></a><span data-ttu-id="ee0db-343">如何定義觸達特定臨界值時的自訂警示？</span><span class="sxs-lookup"><span data-stu-id="ee0db-343">How do I define custom alerts for when certain thresholds are reached?</span></span>

<span data-ttu-id="ee0db-344">您在處理指定之臨界值的警示時有一些彈性。</span><span class="sxs-lookup"><span data-stu-id="ee0db-344">You have some flexibility in how you handle alerts for specified thresholds.</span></span> <span data-ttu-id="ee0db-345">例如，您可以定義自訂的 webhook。</span><span class="sxs-lookup"><span data-stu-id="ee0db-345">For example, you can define customized webhooks.</span></span> <span data-ttu-id="ee0db-346">hello 下列 webhook 範例是從資源管理員範本：</span><span class="sxs-lookup"><span data-stu-id="ee0db-346">hello following webhook example is from a Resource Manager template:</span></span>

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

<span data-ttu-id="ee0db-347">在此範例中，警示會進入 tooPagerduty.com 達到臨界值時。</span><span class="sxs-lookup"><span data-stu-id="ee0db-347">In this example, an alert goes tooPagerduty.com when a threshold is reached.</span></span>



## <a name="patching-and-operations"></a><span data-ttu-id="ee0db-348">修補和作業</span><span class="sxs-lookup"><span data-stu-id="ee0db-348">Patching and operations</span></span>

### <a name="how-do-i-create-a-scale-set-in-an-existing-resource-group"></a><span data-ttu-id="ee0db-349">我如何在現有資源群組中建立擴展集？</span><span class="sxs-lookup"><span data-stu-id="ee0db-349">How do I create a scale set in an existing resource group?</span></span>

<span data-ttu-id="ee0db-350">建立小數位數的集合中現有的資源群組還不能從 hello Azure 入口網站，但部署小數位數設定的 Azure Resource Manager 範本時，您可以指定現有的資源群組。</span><span class="sxs-lookup"><span data-stu-id="ee0db-350">Creating scale sets in an existing resource group is not yet possible from hello Azure portal, but you can specify an existing resource group when deploying a scale set from an Azure Resource Manager template.</span></span> <span data-ttu-id="ee0db-351">您也可以在使用 Azure PowerShell 或 CLI 建立擴展集時，指定現有的資源群組。</span><span class="sxs-lookup"><span data-stu-id="ee0db-351">You can also specify an existing resource group when creating a scale set using Azure PowerShell or CLI.</span></span>

### <a name="can-we-move-a-scale-set-tooanother-resource-group"></a><span data-ttu-id="ee0db-352">我們可以將規模調整集合 tooanother 資源群組嗎？</span><span class="sxs-lookup"><span data-stu-id="ee0db-352">Can we move a scale set tooanother resource group?</span></span>

<span data-ttu-id="ee0db-353">是，您可以移動標尺組資源 tooa 新訂用帳戶或資源群組。</span><span class="sxs-lookup"><span data-stu-id="ee0db-353">Yes, you can move scale set resources tooa new subscription or resource group.</span></span>

### <a name="how-tooi-update-my-virtual-machine-scale-set-tooa-new-image-how-do-i-manage-patching"></a><span data-ttu-id="ee0db-354">如何更新 tooI 我虛擬機器規模集 tooa 新映像嗎？</span><span class="sxs-lookup"><span data-stu-id="ee0db-354">How tooI update my virtual machine scale set tooa new image?</span></span> <span data-ttu-id="ee0db-355">如何管理修補？</span><span class="sxs-lookup"><span data-stu-id="ee0db-355">How do I manage patching?</span></span>

<span data-ttu-id="ee0db-356">請參閱您的虛擬機器規模集 tooa 新的映像，以及 toomanage 修補的 tooupdate[升級虛擬機器規模集](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-upgrade-scale-set)。</span><span class="sxs-lookup"><span data-stu-id="ee0db-356">tooupdate your virtual machine scale set tooa new image, and toomanage patching, see [Upgrade a virtual machine scale set](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-upgrade-scale-set).</span></span>

### <a name="can-i-use-hello-reimage-operation-tooreset-a-vm-without-changing-hello-image-that-is-i-want-reset-a-vm-toofactory-settings-rather-than-tooa-new-image"></a><span data-ttu-id="ee0db-357">可以使用 hello 重新安裝映像作業 tooreset VM 而不需要變更 hello 映像嗎？</span><span class="sxs-lookup"><span data-stu-id="ee0db-357">Can I use hello reimage operation tooreset a VM without changing hello image?</span></span> <span data-ttu-id="ee0db-358">(也就是，我想重設 VM toofactory 設定而不是 tooa 新映像。)</span><span class="sxs-lookup"><span data-stu-id="ee0db-358">(That is, I want reset a VM toofactory settings rather than tooa new image.)</span></span>

<span data-ttu-id="ee0db-359">是，您可以使用 hello 重新安裝映像作業 tooreset VM 而不需要變更 hello 映像。</span><span class="sxs-lookup"><span data-stu-id="ee0db-359">Yes, you can use hello reimage operation tooreset a VM without changing hello image.</span></span> <span data-ttu-id="ee0db-360">不過，如果虛擬機器規模集參考與平台映像`version = latest`，您的 VM 可以更新 tooa 更新的 OS 映像，當您呼叫`reimage`。</span><span class="sxs-lookup"><span data-stu-id="ee0db-360">However, if your virtual machine scale set references a platform image with `version = latest`, your VM can update tooa later OS image when you call `reimage`.</span></span>

<span data-ttu-id="ee0db-361">如需詳細資訊，請參閱[管理虛擬機器擴展集中的所有 VM](https://docs.microsoft.com/rest/api/virtualmachinescalesets/manage-all-vms-in-a-set)。</span><span class="sxs-lookup"><span data-stu-id="ee0db-361">For more information, see [Manage all VMs in a virtual machine scale set](https://docs.microsoft.com/rest/api/virtualmachinescalesets/manage-all-vms-in-a-set).</span></span>



## <a name="troubleshooting"></a><span data-ttu-id="ee0db-362">疑難排解</span><span class="sxs-lookup"><span data-stu-id="ee0db-362">Troubleshooting</span></span>

### <a name="how-do-i-turn-on-boot-diagnostics"></a><span data-ttu-id="ee0db-363">如何開啟開機診斷？</span><span class="sxs-lookup"><span data-stu-id="ee0db-363">How do I turn on boot diagnostics?</span></span>

<span data-ttu-id="ee0db-364">開機診斷 tooturn 首先，建立儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="ee0db-364">tooturn on boot diagnostics, first, create a storage account.</span></span> <span data-ttu-id="ee0db-365">然後，將此 JSON 區塊放在您的虛擬機器規模集**virtualMachineProfile**，並更新 hello 虛擬機器規模集：</span><span class="sxs-lookup"><span data-stu-id="ee0db-365">Then, put this JSON block in your virtual machine scale set **virtualMachineProfile**, and update hello virtual machine scale set:</span></span>

```json
"diagnosticsProfile": {
    "bootDiagnostics": {
        "enabled": true,
        "storageUri": "http://yourstorageaccount.blob.core.windows.net"
    }
}
```

<span data-ttu-id="ee0db-366">建立新的 VM 時，hello hello VM InstanceView 屬性會顯示 hello 螢幕擷取畫面和等等的 hello 詳細資料。</span><span class="sxs-lookup"><span data-stu-id="ee0db-366">When a new VM is created, hello InstanceView property of hello VM shows hello details for hello screenshot, and so on.</span></span> <span data-ttu-id="ee0db-367">以下是範例：</span><span class="sxs-lookup"><span data-stu-id="ee0db-367">Here's an example:</span></span>
 
```json
"bootDiagnostics": {
    "consoleScreenshotBlobUri": "https://o0sz3nhtbmkg6geswarm5.blob.core.windows.net/bootdiagnostics-swarmagen-4157d838-8335-4f78-bf0e-b616a99bc8bd/swarm-agent-9574AE92vmss-0_2.4157d838-8335-4f78-bf0e-b616a99bc8bd.screenshot.bmp",
    "serialConsoleLogBlobUri": "https://o0sz3nhtbmkg6geswarm5.blob.core.windows.net/bootdiagnostics-swarmagen-4157d838-8335-4f78-bf0e-b616a99bc8bd/swarm-agent-9574AE92vmss-0_2.4157d838-8335-4f78-bf0e-b616a99bc8bd.serialconsole.log"
  }
```


## <a name="virtual-machine-properties"></a><span data-ttu-id="ee0db-368">虛擬機器屬性</span><span class="sxs-lookup"><span data-stu-id="ee0db-368">Virtual machine properties</span></span>

### <a name="how-do-i-get-property-information-for-each-vm-without-making-multiple-calls-for-example-how-would-i-get-hello-fault-domain-for-each-of-hello-100-vms-in-my-virtual-machine-scale-set"></a><span data-ttu-id="ee0db-369">如何取得每部 VM 的屬性資訊，而不進行多次呼叫？</span><span class="sxs-lookup"><span data-stu-id="ee0db-369">How do I get property information for each VM without making multiple calls?</span></span> <span data-ttu-id="ee0db-370">例如，如何會取得 hello 容錯網域 hello 的每個 100 Vm 在我的虛擬機器規模集？</span><span class="sxs-lookup"><span data-stu-id="ee0db-370">For example, how would I get hello fault domain for each of hello 100 VMs in my virtual machine scale set?</span></span>

<span data-ttu-id="ee0db-371">為每個 VM，而不需要進行多次呼叫 tooget 屬性資訊，您可以呼叫`ListVMInstanceViews`藉由 REST API `GET` hello 下列資源 URI 上：</span><span class="sxs-lookup"><span data-stu-id="ee0db-371">tooget property information for each VM without making multiple calls, you can call `ListVMInstanceViews` by doing a REST API `GET` on hello following resource URI:</span></span>

<span data-ttu-id="ee0db-372">/subscriptions/<subscription_id>/resourceGroups/<resource_group_name>/providers/Microsoft.Compute/virtualMachineScaleSets/<scaleset_name>/virtualMachines?$expand=instanceView&$select=instanceView</span><span class="sxs-lookup"><span data-stu-id="ee0db-372">/subscriptions/<subscription_id>/resourceGroups/<resource_group_name>/providers/Microsoft.Compute/virtualMachineScaleSets/<scaleset_name>/virtualMachines?$expand=instanceView&$select=instanceView</span></span>

### <a name="can-i-pass-different-extension-arguments-toodifferent-vms-in-a-virtual-machine-scale-set"></a><span data-ttu-id="ee0db-373">可以傳入不同延伸引數 toodifferent Vm 虛擬機器規模集嗎？</span><span class="sxs-lookup"><span data-stu-id="ee0db-373">Can I pass different extension arguments toodifferent VMs in a virtual machine scale set?</span></span>

<span data-ttu-id="ee0db-374">否，您無法傳遞不同的延伸引數 toodifferent Vm 中虛擬機器規模集。</span><span class="sxs-lookup"><span data-stu-id="ee0db-374">No, you cannot pass different extension arguments toodifferent VMs in a virtual machine scale set.</span></span> <span data-ttu-id="ee0db-375">不過，擴充功能可做根據 hello 的 hello VM，執行在 hello 電腦名稱的唯一屬性。</span><span class="sxs-lookup"><span data-stu-id="ee0db-375">However, extensions can act based on hello unique properties of hello VM they are running on, such as on hello machine name.</span></span> <span data-ttu-id="ee0db-376">延伸模組也可以查詢執行個體中繼資料上 http://169.254.169.254 tooget hello VM 的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="ee0db-376">Extensions also can query instance metadata on http://169.254.169.254 tooget more information about hello VM.</span></span>

### <a name="why-are-there-gaps-between-my-virtual-machine-scale-set-vm-machine-names-and-vm-ids-for-example-0-1-3"></a><span data-ttu-id="ee0db-377">為何我的虛擬機器擴展集 VM 電腦名稱與 VM 識別碼之間會有落差？</span><span class="sxs-lookup"><span data-stu-id="ee0db-377">Why are there gaps between my virtual machine scale set VM machine names and VM IDs?</span></span> <span data-ttu-id="ee0db-378">例如：0、1、3...</span><span class="sxs-lookup"><span data-stu-id="ee0db-378">For example: 0, 1, 3...</span></span>

<span data-ttu-id="ee0db-379">會虛擬機器規模集 VM 電腦名稱與 VM 識別碼之間的間距，因為虛擬機器規模集**overprovision**屬性設定為 toohello 預設值的**true**。</span><span class="sxs-lookup"><span data-stu-id="ee0db-379">There are gaps between your virtual machine scale set VM machine names and VM IDs because your virtual machine scale set **overprovision** property is set toohello default value of **true**.</span></span> <span data-ttu-id="ee0db-380">如果過度佈建太設定**true**，要求會建立多個 Vm。</span><span class="sxs-lookup"><span data-stu-id="ee0db-380">If overprovisioning is set too**true**, more VMs than requested are created.</span></span> <span data-ttu-id="ee0db-381">然後會刪除額外的 VM。</span><span class="sxs-lookup"><span data-stu-id="ee0db-381">Extra VMs are then deleted.</span></span> <span data-ttu-id="ee0db-382">在此情況下，您會取得部署增加的可靠性，但在 hello 費用連續命名連續網路位址轉譯 (NAT) 規則。</span><span class="sxs-lookup"><span data-stu-id="ee0db-382">In this case, you gain increased deployment reliability, but at hello expense of contiguous naming and contiguous Network Address Translation (NAT) rules.</span></span> 

<span data-ttu-id="ee0db-383">您可以設定此屬性太**false**。</span><span class="sxs-lookup"><span data-stu-id="ee0db-383">You can set this property too**false**.</span></span> <span data-ttu-id="ee0db-384">若為小型虛擬機器擴展集，這就不會大幅影響部署可靠性。</span><span class="sxs-lookup"><span data-stu-id="ee0db-384">For small virtual machine scale sets, this doesn't significantly affect deployment reliability.</span></span>

### <a name="what-is-hello-difference-between-deleting-a-vm-in-a-virtual-machine-scale-set-and-deallocating-hello-vm-when-should-i-choose-one-over-hello-other"></a><span data-ttu-id="ee0db-385">Hello 刪除虛擬機器規模集中的 VM 和解除配置 hello VM 之間的差異為何？</span><span class="sxs-lookup"><span data-stu-id="ee0db-385">What is hello difference between deleting a VM in a virtual machine scale set and deallocating hello VM?</span></span> <span data-ttu-id="ee0db-386">我何時應該選擇一種其他 hello？</span><span class="sxs-lookup"><span data-stu-id="ee0db-386">When should I choose one over hello other?</span></span>

<span data-ttu-id="ee0db-387">hello 刪除虛擬機器規模集中的 VM 和解除配置 hello VM 之間的主要差異在於`deallocate`並不會刪除 hello 虛擬硬碟 (Vhd)。</span><span class="sxs-lookup"><span data-stu-id="ee0db-387">hello main difference between deleting a VM in a virtual machine scale set and deallocating hello VM is that `deallocate` doesn’t delete hello virtual hard disks (VHDs).</span></span> <span data-ttu-id="ee0db-388">執行 `stop deallocate` 會產生相關的儲存體成本。</span><span class="sxs-lookup"><span data-stu-id="ee0db-388">There are storage costs associated with running `stop deallocate`.</span></span> <span data-ttu-id="ee0db-389">您可能會使用其中一個或另一個用於 hello 下列原因之一 hello:</span><span class="sxs-lookup"><span data-stu-id="ee0db-389">You might use one or hello other for one of hello following reasons:</span></span>

- <span data-ttu-id="ee0db-390">您想 toostop 支付計算費用，但是您想要的 hello Vm tookeep hello 磁碟狀態。</span><span class="sxs-lookup"><span data-stu-id="ee0db-390">You want toostop paying compute costs, but you want tookeep hello disk state of hello VMs.</span></span>
- <span data-ttu-id="ee0db-391">您無法擴充虛擬機器規模集比快速 toostart 一組的 Vm。</span><span class="sxs-lookup"><span data-stu-id="ee0db-391">You want toostart a set of VMs more quickly than you could scale out a virtual machine scale set.</span></span>
  - <span data-ttu-id="ee0db-392">相關的 toothis 案例中，您可能已建立您自己的自動調整引擎和想更快的端對端小數位數。</span><span class="sxs-lookup"><span data-stu-id="ee0db-392">Related toothis scenario, you might have created your own autoscale engine and want a faster end-to-end scale.</span></span>
- <span data-ttu-id="ee0db-393">您的虛擬機器擴展集並未平均分散於各容錯網域或更新網域。</span><span class="sxs-lookup"><span data-stu-id="ee0db-393">You have a virtual machine scale set that is unevenly distributed across fault domains or update domains.</span></span> <span data-ttu-id="ee0db-394">這可能是因為您選擇性地刪除 VM，或是因為 VM 在過度佈建之後遭到刪除。</span><span class="sxs-lookup"><span data-stu-id="ee0db-394">This might be because you selectively deleted VMs, or because VMs were deleted after overprovisioning.</span></span> <span data-ttu-id="ee0db-395">執行`stop deallocate`後面`start`hello 虛擬機器擴展集平均分散 hello Vm 容錯網域或更新網域。</span><span class="sxs-lookup"><span data-stu-id="ee0db-395">Running `stop deallocate` followed by `start` on hello virtual machine scale set evenly distributes hello VMs across fault domains or update domains.</span></span>

