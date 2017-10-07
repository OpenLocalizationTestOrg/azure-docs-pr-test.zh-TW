---
title: "aaaIntegrate 金鑰保存庫在 Azure （傳統） 中的 Windows Vm 上的 SQL server |Microsoft 文件"
description: "了解如何 tooautomate hello 的 Azure 金鑰保存庫搭配使用的 SQL Server 加密組態。 本主題說明如何使用 SQL Server 虛擬機器的 Azure 金鑰保存庫整合 toouse 建立 hello 傳統部署模型中。"
services: virtual-machines-windows
documentationcenter: 
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: ab8d41a7-1971-4032-ab71-eb435c455dc1
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 02/17/2017
ms.author: jroth
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 54664875b76dac7271d5a9f00b3f41fdc9c08491
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-key-vault-integration-for-sql-server-on-azure-virtual-machines-classic"></a><span data-ttu-id="b06f8-104">在 Azure 虛擬機器上設定 SQL Server 的 Azure Key Vault 整合 (傳統)</span><span class="sxs-lookup"><span data-stu-id="b06f8-104">Configure Azure Key Vault Integration for SQL Server on Azure Virtual Machines (Classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b06f8-105">資源管理員</span><span class="sxs-lookup"><span data-stu-id="b06f8-105">Resource Manager</span></span>](../sql/virtual-machines-windows-ps-sql-keyvault.md)
> * [<span data-ttu-id="b06f8-106">傳統</span><span class="sxs-lookup"><span data-stu-id="b06f8-106">Classic</span></span>](../classic/ps-sql-keyvault.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="b06f8-107">概觀</span><span class="sxs-lookup"><span data-stu-id="b06f8-107">Overview</span></span>
<span data-ttu-id="b06f8-108">有多個 SQL Server 加密功能，例如[透明資料加密 (TDE)](https://msdn.microsoft.com/library/bb934049.aspx)、[資料行層級加密 (CLE)](https://msdn.microsoft.com/library/ms173744.aspx) 和[備份加密](https://msdn.microsoft.com/library/dn449489.aspx)。</span><span class="sxs-lookup"><span data-stu-id="b06f8-108">There are multiple SQL Server encryption features, such as [transparent data encryption (TDE)](https://msdn.microsoft.com/library/bb934049.aspx), [column level encryption (CLE)](https://msdn.microsoft.com/library/ms173744.aspx), and [backup encryption](https://msdn.microsoft.com/library/dn449489.aspx).</span></span> <span data-ttu-id="b06f8-109">這些形式的加密需要您 toomanage，而儲存 hello 用來加密的密碼編譯金鑰。</span><span class="sxs-lookup"><span data-stu-id="b06f8-109">These forms of encryption require you toomanage and store hello cryptographic keys you use for encryption.</span></span> <span data-ttu-id="b06f8-110">hello Azure 金鑰保存庫 (AKV) 服務是設計的 tooimprove hello 安全性和管理高可用性的位置中的這些索引鍵。</span><span class="sxs-lookup"><span data-stu-id="b06f8-110">hello Azure Key Vault (AKV) service is designed tooimprove hello security and management of these keys in a secure and highly available location.</span></span> <span data-ttu-id="b06f8-111">hello [SQL Server Connector](http://www.microsoft.com/download/details.aspx?id=45344)可讓 SQL Server toouse Azure 金鑰保存庫中的這些索引鍵。</span><span class="sxs-lookup"><span data-stu-id="b06f8-111">hello [SQL Server Connector](http://www.microsoft.com/download/details.aspx?id=45344) enables SQL Server toouse these keys from Azure Key Vault.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="b06f8-112">Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../../azure-resource-manager/resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="b06f8-112">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="b06f8-113">本文件涵蓋使用 hello 傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="b06f8-113">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="b06f8-114">Microsoft 建議最新的部署使用 hello 資源管理員的模型。</span><span class="sxs-lookup"><span data-stu-id="b06f8-114">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="b06f8-115">如果您沒有執行 SQL Server 在內部部署機器，有[步驟，您可以從內部部署 SQL Server 電腦遵循 tooaccess Azure 金鑰保存庫](https://msdn.microsoft.com/library/dn198405.aspx)。</span><span class="sxs-lookup"><span data-stu-id="b06f8-115">If you are running SQL Server with on-premises machines, there are [steps you can follow tooaccess Azure Key Vault from your on-premises SQL Server machine](https://msdn.microsoft.com/library/dn198405.aspx).</span></span> <span data-ttu-id="b06f8-116">在 Azure Vm 中的 SQL server，您可以使用 hello 來節省時間，但是*Azure 金鑰保存庫整合*功能。</span><span class="sxs-lookup"><span data-stu-id="b06f8-116">But for SQL Server in Azure VMs, you can save time by using hello *Azure Key Vault Integration* feature.</span></span> <span data-ttu-id="b06f8-117">少數的 Azure PowerShell cmdlet tooenable 這項功能，您可以使用自動化 hello 組態所需的 SQL VM tooaccess 金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="b06f8-117">With a few Azure PowerShell cmdlets tooenable this feature, you can automate hello configuration necessary for a SQL VM tooaccess your key vault.</span></span>

<span data-ttu-id="b06f8-118">啟用這項功能時，它會自動安裝 SQL Server Connector hello、 設定 hello EKM 提供者 tooaccess Azure 金鑰保存庫，並且建立 hello 認證 tooallow 您 tooaccess 您保存庫。</span><span class="sxs-lookup"><span data-stu-id="b06f8-118">When this feature is enabled, it automatically installs hello SQL Server Connector, configures hello EKM provider tooaccess Azure Key Vault, and creates hello credential tooallow you tooaccess your vault.</span></span> <span data-ttu-id="b06f8-119">如果您在查看 hello 中的 hello 步驟先前所述內部文件，您可以看到這項功能會自動執行步驟 2 和 3。</span><span class="sxs-lookup"><span data-stu-id="b06f8-119">If you looked at hello steps in hello previously mentioned on-premises documentation, you can see that this feature automates steps 2 and 3.</span></span> <span data-ttu-id="b06f8-120">您仍然必須 toodo 手動 hello 唯一的是 toocreate hello 金鑰保存庫和金鑰。</span><span class="sxs-lookup"><span data-stu-id="b06f8-120">hello only thing you would still need toodo manually is toocreate hello key vault and keys.</span></span> <span data-ttu-id="b06f8-121">從該處，hello 整個安裝的 SQL VM 會自動執行。</span><span class="sxs-lookup"><span data-stu-id="b06f8-121">From there, hello entire setup of your SQL VM is automated.</span></span> <span data-ttu-id="b06f8-122">此安裝程式完成後這項功能，您可以執行 T-SQL 陳述式 toobegin 加密您的資料庫或備份，像平常一樣。</span><span class="sxs-lookup"><span data-stu-id="b06f8-122">Once this feature has completed this setup, you can execute T-SQL statements toobegin encrypting your databases or backups as you normally would.</span></span>

[!INCLUDE [AKV Integration Prepare](../../../../includes/virtual-machines-sql-server-akv-prepare.md)]

## <a name="configure-akv-integration"></a><span data-ttu-id="b06f8-123">設定 AKV 整合</span><span class="sxs-lookup"><span data-stu-id="b06f8-123">Configure AKV Integration</span></span>
<span data-ttu-id="b06f8-124">使用 PowerShell tooconfigure Azure 金鑰保存庫整合。</span><span class="sxs-lookup"><span data-stu-id="b06f8-124">Use PowerShell tooconfigure Azure Key Vault Integration.</span></span> <span data-ttu-id="b06f8-125">hello 下列各節提供所需的 hello 參數的概觀，然後的範例 PowerShell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="b06f8-125">hello following sections provide an overview of hello required parameters and then a sample PowerShell script.</span></span>

### <a name="install-hello-sql-server-iaas-extension"></a><span data-ttu-id="b06f8-126">安裝 SQL Server IaaS 延伸模組 hello</span><span class="sxs-lookup"><span data-stu-id="b06f8-126">Install hello SQL Server IaaS Extension</span></span>
<span data-ttu-id="b06f8-127">首先，[安裝 SQL Server IaaS 延伸模組 hello](../classic/sql-server-agent-extension.md)。</span><span class="sxs-lookup"><span data-stu-id="b06f8-127">First, [install hello SQL Server IaaS Extension](../classic/sql-server-agent-extension.md).</span></span>

### <a name="understand-hello-input-parameters"></a><span data-ttu-id="b06f8-128">了解 hello 輸入的參數</span><span class="sxs-lookup"><span data-stu-id="b06f8-128">Understand hello input parameters</span></span>
<span data-ttu-id="b06f8-129">hello 下列資料表列出 hello 參數需要 toorun hello PowerShell 指令碼 hello 下一節。</span><span class="sxs-lookup"><span data-stu-id="b06f8-129">hello following table lists hello parameters required toorun hello PowerShell script in hello next section.</span></span>

| <span data-ttu-id="b06f8-130">參數</span><span class="sxs-lookup"><span data-stu-id="b06f8-130">Parameter</span></span> | <span data-ttu-id="b06f8-131">說明</span><span class="sxs-lookup"><span data-stu-id="b06f8-131">Description</span></span> | <span data-ttu-id="b06f8-132">範例</span><span class="sxs-lookup"><span data-stu-id="b06f8-132">Example</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b06f8-133">**$akvURL**</span><span class="sxs-lookup"><span data-stu-id="b06f8-133">**$akvURL**</span></span> |<span data-ttu-id="b06f8-134">**hello 金鑰保存庫 URL**</span><span class="sxs-lookup"><span data-stu-id="b06f8-134">**hello key vault URL**</span></span> |<span data-ttu-id="b06f8-135">"https://contosokeyvault.vault.azure.net/"</span><span class="sxs-lookup"><span data-stu-id="b06f8-135">"https://contosokeyvault.vault.azure.net/"</span></span> |
| <span data-ttu-id="b06f8-136">**$spName**</span><span class="sxs-lookup"><span data-stu-id="b06f8-136">**$spName**</span></span> |<span data-ttu-id="b06f8-137">**服務主體名稱**</span><span class="sxs-lookup"><span data-stu-id="b06f8-137">**Service Principal name**</span></span> |<span data-ttu-id="b06f8-138">"fde2b411-33d5-4e11-af04eb07b669ccf2"</span><span class="sxs-lookup"><span data-stu-id="b06f8-138">"fde2b411-33d5-4e11-af04eb07b669ccf2"</span></span> |
| <span data-ttu-id="b06f8-139">**$spSecret**</span><span class="sxs-lookup"><span data-stu-id="b06f8-139">**$spSecret**</span></span> |<span data-ttu-id="b06f8-140">**服務主體密碼**</span><span class="sxs-lookup"><span data-stu-id="b06f8-140">**Service Principal secret**</span></span> |<span data-ttu-id="b06f8-141">"9VTJSQwzlFepD8XODnzy8n2V01Jd8dAjwm/azF1XDKM="</span><span class="sxs-lookup"><span data-stu-id="b06f8-141">"9VTJSQwzlFepD8XODnzy8n2V01Jd8dAjwm/azF1XDKM="</span></span> |
| <span data-ttu-id="b06f8-142">**$credName**</span><span class="sxs-lookup"><span data-stu-id="b06f8-142">**$credName**</span></span> |<span data-ttu-id="b06f8-143">**認證名稱**: AKV 整合建立 SQL Server，讓 hello VM toohave 存取 toohello 金鑰保存庫中的認證。</span><span class="sxs-lookup"><span data-stu-id="b06f8-143">**Credential name**: AKV Integration creates a credential within SQL Server, allowing hello VM toohave access toohello key vault.</span></span> <span data-ttu-id="b06f8-144">選擇此認證的名稱。</span><span class="sxs-lookup"><span data-stu-id="b06f8-144">Choose a name for this credential.</span></span> |<span data-ttu-id="b06f8-145">"mycred1"</span><span class="sxs-lookup"><span data-stu-id="b06f8-145">"mycred1"</span></span> |
| <span data-ttu-id="b06f8-146">**$vmName**</span><span class="sxs-lookup"><span data-stu-id="b06f8-146">**$vmName**</span></span> |<span data-ttu-id="b06f8-147">**虛擬機器名稱**: hello 先前建立的 SQL VM 名稱。</span><span class="sxs-lookup"><span data-stu-id="b06f8-147">**Virtual machine name**: hello name of a previously created SQL VM.</span></span> |<span data-ttu-id="b06f8-148">"myvmname"</span><span class="sxs-lookup"><span data-stu-id="b06f8-148">"myvmname"</span></span> |
| <span data-ttu-id="b06f8-149">**$serviceName**</span><span class="sxs-lookup"><span data-stu-id="b06f8-149">**$serviceName**</span></span> |<span data-ttu-id="b06f8-150">**服務名稱**: hello 與 hello SQL VM 相關聯的雲端服務名稱。</span><span class="sxs-lookup"><span data-stu-id="b06f8-150">**Service name**: hello Cloud Service name that is associated with hello SQL VM.</span></span> |<span data-ttu-id="b06f8-151">"mycloudservicename"</span><span class="sxs-lookup"><span data-stu-id="b06f8-151">"mycloudservicename"</span></span> |

### <a name="enable-akv-integration-with-powershell"></a><span data-ttu-id="b06f8-152">使用 PowerShell 啟用 AKV 整合</span><span class="sxs-lookup"><span data-stu-id="b06f8-152">Enable AKV Integration with PowerShell</span></span>
<span data-ttu-id="b06f8-153">hello**新增 AzureVMSqlServerKeyVaultCredentialConfig** cmdlet 會建立 hello Azure 金鑰保存庫整合功能的組態物件。</span><span class="sxs-lookup"><span data-stu-id="b06f8-153">hello **New-AzureVMSqlServerKeyVaultCredentialConfig** cmdlet creates a configuration object for hello Azure Key Vault Integration feature.</span></span> <span data-ttu-id="b06f8-154">hello**組 AzureVMSqlServerExtension**設定這項整合以 hello **KeyVaultCredentialSettings**參數。</span><span class="sxs-lookup"><span data-stu-id="b06f8-154">hello **Set-AzureVMSqlServerExtension** configures this integration with hello **KeyVaultCredentialSettings** parameter.</span></span> <span data-ttu-id="b06f8-155">hello 下列步驟顯示如何 toouse 這些命令。</span><span class="sxs-lookup"><span data-stu-id="b06f8-155">hello following steps show how toouse these commands.</span></span>

1. <span data-ttu-id="b06f8-156">在 Azure PowerShell 中，先設定 hello 輸入的參數的特定值 hello 本主題的前幾節中所述。</span><span class="sxs-lookup"><span data-stu-id="b06f8-156">In Azure PowerShell, first configure hello input parameters with your specific values as described in hello previous sections of this topic.</span></span> <span data-ttu-id="b06f8-157">下列指令碼的 hello 是範例。</span><span class="sxs-lookup"><span data-stu-id="b06f8-157">hello following script is an example.</span></span>
   
        $akvURL = "https://contosokeyvault.vault.azure.net/"
        $spName = "fde2b411-33d5-4e11-af04eb07b669ccf2"
        $spSecret = "9VTJSQwzlFepD8XODnzy8n2V01Jd8dAjwm/azF1XDKM="
        $credName = "mycred1"
        $vmName = "myvmname"
        $serviceName = "mycloudservicename"
2. <span data-ttu-id="b06f8-158">然後使用 hello 以下 tooconfigure 編寫指令碼，並啟用 AKV 整合。</span><span class="sxs-lookup"><span data-stu-id="b06f8-158">Then use hello following script tooconfigure and enable AKV Integration.</span></span>
   
        $secureakv =  $spSecret | ConvertTo-SecureString -AsPlainText -Force
        $akvs = New-AzureVMSqlServerKeyVaultCredentialConfig -Enable -CredentialName $credname -AzureKeyVaultUrl $akvURL -ServicePrincipalName $spName -ServicePrincipalSecret $secureakv
        Get-AzureVM -ServiceName $serviceName -Name $vmName | Set-AzureVMSqlServerExtension -KeyVaultCredentialSettings $akvs | Update-AzureVM

<span data-ttu-id="b06f8-159">hello SQL IaaS 代理程式延伸模組將會更新這個新的設定 hello SQL VM。</span><span class="sxs-lookup"><span data-stu-id="b06f8-159">hello SQL IaaS Agent Extension will update hello SQL VM with this new configuration.</span></span>

[!INCLUDE [AKV Integration Next Steps](../../../../includes/virtual-machines-sql-server-akv-next-steps.md)]

