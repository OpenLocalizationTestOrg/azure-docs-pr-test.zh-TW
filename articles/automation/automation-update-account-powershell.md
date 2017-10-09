---
title: "使用 PowerShell 的 Azure 自動化執行身分帳戶 aaaCreate |Microsoft 文件"
description: "本文說明如何 tooupgrade 您的自動化帳戶以 PowerShell toocreate hello 執行身分帳戶如果您並未從 hello 入口網站的初始建立期間執行此步驟。"
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
ms.assetid: 
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/14/2017
ms.author: magoedte
ms.openlocfilehash: 1049601321d2bc1e5f9d982f622788f8e4e4d797
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="update-automation-run-as-account-using-powershell"></a><span data-ttu-id="16352-103">使用 PowerShell 更新自動化執行身分帳戶</span><span class="sxs-lookup"><span data-stu-id="16352-103">Update Automation Run As account using PowerShell</span></span>
<span data-ttu-id="16352-104">如果您可以使用指定 PowerShell tooupdate 您現有的自動化帳戶：</span><span class="sxs-lookup"><span data-stu-id="16352-104">You can use PowerShell tooupdate your existing Automation account if:</span></span>

* <span data-ttu-id="16352-105">建立自動化帳戶，但拒絕 toocreate hello 執行身分帳戶。</span><span class="sxs-lookup"><span data-stu-id="16352-105">You create an Automation account but decline toocreate hello Run As account.</span></span>
* <span data-ttu-id="16352-106">您已經使用自動化帳戶 toomanage 資源管理員資源，並想 runbook 驗證 tooupdate hello tooinclude hello 執行身分帳戶。</span><span class="sxs-lookup"><span data-stu-id="16352-106">You already use an Automation account toomanage Resource Manager resources and you want tooupdate hello account tooinclude hello Run As account for runbook authentication.</span></span>
* <span data-ttu-id="16352-107">您已經使用自動化帳戶 toomanage 傳統資源，而且您想 tooupdate 它 toouse hello 傳統執行身分帳戶，而不要建立新的帳戶和移轉您的 runbook 與資產 tooit。</span><span class="sxs-lookup"><span data-stu-id="16352-107">You already use an Automation account toomanage classic resources and you want tooupdate it toouse hello Classic Run As account instead of creating a new account and migrating your runbooks and assets tooit.</span></span>   
* <span data-ttu-id="16352-108">您想要 toocreate 執行身分和傳統執行身分帳戶使用企業憑證授權單位 (CA) 所核發的憑證。</span><span class="sxs-lookup"><span data-stu-id="16352-108">You want toocreate a Run As and a Classic Run As account by using a certificate issued by your enterprise certification authority (CA).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="16352-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="16352-109">Prerequisites</span></span>

* <span data-ttu-id="16352-110">hello 指令碼可以與 2.01 和更新版本的 Azure 資源管理員模組只能在 Windows 10 和 Windows Server 2016 上執行。</span><span class="sxs-lookup"><span data-stu-id="16352-110">hello script can be run only on Windows 10 and Windows Server 2016 with Azure Resource Manager modules 2.01 and later.</span></span> <span data-ttu-id="16352-111">不支援在舊版 Windows 上執行。</span><span class="sxs-lookup"><span data-stu-id="16352-111">It is not supported on earlier versions of Windows.</span></span>
* <span data-ttu-id="16352-112">Azure PowerShell 1.0 和更新版本。</span><span class="sxs-lookup"><span data-stu-id="16352-112">Azure PowerShell 1.0 and later.</span></span> <span data-ttu-id="16352-113">如需 hello PowerShell 1.0 版的資訊，請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="16352-113">For information about hello PowerShell 1.0 release, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="16352-114">自動化帳戶被稱為 hello hello 值*– AutomationAccountName*和*-ApplicationDisplayName* hello 下列 PowerShell 指令碼中的參數。</span><span class="sxs-lookup"><span data-stu-id="16352-114">An Automation account, which is referenced as hello value for hello *–AutomationAccountName* and *-ApplicationDisplayName* parameters in hello following PowerShell script.</span></span>

<span data-ttu-id="16352-115">tooget hello 值*SubscriptionID*， *ResourceGroup*，和*AutomationAccountName*、 哪些是 hello 指令碼的必要的參數、 執行 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="16352-115">tooget hello values for *SubscriptionID*, *ResourceGroup*, and *AutomationAccountName*, which are required parameters for hello scripts, do hello following:</span></span>
1. <span data-ttu-id="16352-116">在 hello Azure 入口網站中選取您的自動化帳戶上 hello**自動化帳戶**刀鋒視窗中，然後再選取**所有設定**。</span><span class="sxs-lookup"><span data-stu-id="16352-116">In hello Azure portal, select your Automation account on hello **Automation account** blade, and then select **All settings**.</span></span> 
2. <span data-ttu-id="16352-117">在 hello**所有設定**刀鋒視窗底下**帳戶設定**，選取**屬性**。</span><span class="sxs-lookup"><span data-stu-id="16352-117">On hello **All settings** blade, under **Account Settings**, select **Properties**.</span></span> 
3. <span data-ttu-id="16352-118">請注意在 hello hello 值**屬性**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="16352-118">Note hello values on hello **Properties** blade.</span></span>

![hello 自動化帳戶 [屬性] 刀鋒視窗](media/automation-sec-configure-azure-runas-account/automation-account-properties.png)  

## <a name="create-run-as-account-powershell-script"></a><span data-ttu-id="16352-120">建立執行身分帳戶 PowerShell 指令碼</span><span class="sxs-lookup"><span data-stu-id="16352-120">Create Run As Account PowerShell script</span></span>
<span data-ttu-id="16352-121">這個 PowerShell 指令碼包含支援的設定 hello:</span><span class="sxs-lookup"><span data-stu-id="16352-121">This PowerShell script includes support for hello following configurations:</span></span>

* <span data-ttu-id="16352-122">使用自我簽署憑證建立執行身分帳戶。</span><span class="sxs-lookup"><span data-stu-id="16352-122">Create a Run As account by using a self-signed certificate.</span></span>
* <span data-ttu-id="16352-123">使用自我簽署憑證建立執行身分帳戶和傳統執行身分帳戶。</span><span class="sxs-lookup"><span data-stu-id="16352-123">Create a Run As account and a Classic Run As account by using a self-signed certificate.</span></span>
* <span data-ttu-id="16352-124">使用企業憑證建立執行身分帳戶和傳統執行身分帳戶。</span><span class="sxs-lookup"><span data-stu-id="16352-124">Create a Run As account and a Classic Run As account by using an enterprise certificate.</span></span>
* <span data-ttu-id="16352-125">建立執行身分帳戶和傳統執行身分帳戶 hello Azure 政府雲端中使用自我簽署的憑證。</span><span class="sxs-lookup"><span data-stu-id="16352-125">Create a Run As account and a Classic Run As account by using a self-signed certificate in hello Azure Government cloud.</span></span>

<span data-ttu-id="16352-126">視您選取的 hello 組態選項，hello 指令碼會建立 hello 下列項目。</span><span class="sxs-lookup"><span data-stu-id="16352-126">Depending on hello configuration option you select, hello script creates hello following items.</span></span>

<span data-ttu-id="16352-127">**若為執行身分帳戶︰**</span><span class="sxs-lookup"><span data-stu-id="16352-127">**For Run As accounts:**</span></span>

* <span data-ttu-id="16352-128">建立 Azure AD 應用程式 toobe 匯出以自我簽署的任一個 hello 或企業憑證的公開金鑰，在 Azure AD 中建立 hello 應用程式的服務主體帳戶，並指派 hello hello 帳戶在您目前的參與者角色訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="16352-128">Creates an Azure AD application toobe exported with either hello self-signed or enterprise certificate public key, creates a service principal account for hello application in Azure AD, and assigns hello Contributor role for hello account in your current subscription.</span></span> <span data-ttu-id="16352-129">您可以變更此設定 tooOwner 或任何其他角色。</span><span class="sxs-lookup"><span data-stu-id="16352-129">You can change this setting tooOwner or any other role.</span></span> <span data-ttu-id="16352-130">如需詳細資訊，請參閱 [Azure 自動化中的角色型存取控制](automation-role-based-access-control.md)。</span><span class="sxs-lookup"><span data-stu-id="16352-130">For more information, see [Role-based access control in Azure Automation](automation-role-based-access-control.md).</span></span>
* <span data-ttu-id="16352-131">建立名為自動化憑證資產*AzureRunAsCertificate* hello 中指定的自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="16352-131">Creates an Automation certificate asset named *AzureRunAsCertificate* in hello specified Automation account.</span></span> <span data-ttu-id="16352-132">hello 憑證資產會保存 hello 憑證私密金鑰，可由 hello Azure AD 應用程式。</span><span class="sxs-lookup"><span data-stu-id="16352-132">hello certificate asset holds hello certificate private key that's used by hello Azure AD application.</span></span>
* <span data-ttu-id="16352-133">建立名為自動化連線資產*AzureRunAsConnection* hello 中指定的自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="16352-133">Creates an Automation connection asset named *AzureRunAsConnection* in hello specified Automation account.</span></span> <span data-ttu-id="16352-134">hello 連線資產會保存 hello applicationId、 tenantId、 subscriptionId、 和憑證指紋。</span><span class="sxs-lookup"><span data-stu-id="16352-134">hello connection asset holds hello applicationId, tenantId, subscriptionId, and certificate thumbprint.</span></span>

<span data-ttu-id="16352-135">**若為傳統執行身分帳戶：**</span><span class="sxs-lookup"><span data-stu-id="16352-135">**For Classic Run As accounts:**</span></span>

* <span data-ttu-id="16352-136">建立名為自動化憑證資產*AzureClassicRunAsCertificate* hello 中指定的自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="16352-136">Creates an Automation certificate asset named *AzureClassicRunAsCertificate* in hello specified Automation account.</span></span> <span data-ttu-id="16352-137">hello 憑證資產會保存 hello 憑證私密金鑰由 hello 管理憑證。</span><span class="sxs-lookup"><span data-stu-id="16352-137">hello certificate asset holds hello certificate private key used by hello management certificate.</span></span>
* <span data-ttu-id="16352-138">建立名為自動化連線資產*AzureClassicRunAsConnection* hello 中指定的自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="16352-138">Creates an Automation connection asset named *AzureClassicRunAsConnection* in hello specified Automation account.</span></span> <span data-ttu-id="16352-139">hello 連線資產包含 hello 訂用帳戶名稱、 訂用帳戶 Id，與憑證資產名稱。</span><span class="sxs-lookup"><span data-stu-id="16352-139">hello connection asset holds hello subscription name, subscriptionId, and certificate asset name.</span></span>

>[!NOTE]
> <span data-ttu-id="16352-140">如果您選取其中一個選項，建立傳統執行身分帳戶，hello 指令碼執行之後上, 傳 hello 公用憑證 （.cer 檔案名稱副檔名） toohello 管理的存放區 hello 訂用帳戶的 hello 自動化帳戶中建立。</span><span class="sxs-lookup"><span data-stu-id="16352-140">If you select either option for creating a Classic Run As account, after hello script is executed, upload hello public certificate (.cer file name extension) toohello management store for hello subscription that hello Automation account was created in.</span></span>
> 

1. <span data-ttu-id="16352-141">儲存您的電腦上下列指令碼的 hello。</span><span class="sxs-lookup"><span data-stu-id="16352-141">Save hello following script on your computer.</span></span> <span data-ttu-id="16352-142">在此範例中，以儲存 hello filename*新增 RunAsAccount.ps1*。</span><span class="sxs-lookup"><span data-stu-id="16352-142">In this example, save it with hello filename *New-RunAsAccount.ps1*.</span></span>

        #Requires -RunAsAdministrator
         Param (
        [Parameter(Mandatory=$true)]
        [String] $ResourceGroup,

        [Parameter(Mandatory=$true)]
        [String] $AutomationAccountName,

        [Parameter(Mandatory=$true)]
        [String] $ApplicationDisplayName,

        [Parameter(Mandatory=$true)]
        [String] $SubscriptionId,

        [Parameter(Mandatory=$true)]
        [Boolean] $CreateClassicRunAsAccount,

        [Parameter(Mandatory=$true)]
        [String] $SelfSignedCertPlainPassword,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPathForRunAsAccount,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPlainPasswordForRunAsAccount,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPathForClassicRunAsAccount,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPlainPasswordForClassicRunAsAccount,

        [Parameter(Mandatory=$false)]
        [ValidateSet("AzureCloud","AzureUSGovernment")]
        [string]$EnvironmentName="AzureCloud",

        [Parameter(Mandatory=$false)]
        [int] $SelfSignedCertNoOfMonthsUntilExpired = 12
        )

        function CreateSelfSignedCertificate([string] $keyVaultName, [string] $certificateName, [string] $selfSignedCertPlainPassword,
                                      [string] $certPath, [string] $certPathCer, [string] $selfSignedCertNoOfMonthsUntilExpired ) {
        $Cert = New-SelfSignedCertificate -DnsName $certificateName -CertStoreLocation cert:\LocalMachine\My `
           -KeyExportPolicy Exportable -Provider "Microsoft Enhanced RSA and AES Cryptographic Provider" `
           -NotAfter (Get-Date).AddMonths($selfSignedCertNoOfMonthsUntilExpired)

        $CertPassword = ConvertTo-SecureString $selfSignedCertPlainPassword -AsPlainText -Force
        Export-PfxCertificate -Cert ("Cert:\localmachine\my\" + $Cert.Thumbprint) -FilePath $certPath -Password $CertPassword -Force | Write-Verbose
        Export-Certificate -Cert ("Cert:\localmachine\my\" + $Cert.Thumbprint) -FilePath $certPathCer -Type CERT | Write-Verbose
        }

        function CreateServicePrincipal([System.Security.Cryptography.X509Certificates.X509Certificate2] $PfxCert, [string] $applicationDisplayName) {  
        $CurrentDate = Get-Date
        $keyValue = [System.Convert]::ToBase64String($PfxCert.GetRawCertData())
        $KeyId = (New-Guid).Guid

        $KeyCredential = New-Object  Microsoft.Azure.Commands.Resources.Models.ActiveDirectory.PSADKeyCredential
        $KeyCredential.StartDate = $CurrentDate
        $KeyCredential.EndDate= [DateTime]$PfxCert.GetExpirationDateString()
        $KeyCredential.EndDate = $KeyCredential.EndDate.AddDays(-1)
        $KeyCredential.KeyId = $KeyId
        $KeyCredential.CertValue  = $keyValue

        # Use key credentials and create an Azure AD application
        $Application = New-AzureRmADApplication -DisplayName $ApplicationDisplayName -HomePage ("http://" + $applicationDisplayName) -IdentifierUris ("http://" + $KeyId) -KeyCredentials $KeyCredential
        $ServicePrincipal = New-AzureRMADServicePrincipal -ApplicationId $Application.ApplicationId
        $GetServicePrincipal = Get-AzureRmADServicePrincipal -ObjectId $ServicePrincipal.Id

        # Sleep here for a few seconds tooallow hello service principal application toobecome active (ordinarily takes a few seconds)
        Sleep -s 15
        $NewRole = New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $Application.ApplicationId -ErrorAction SilentlyContinue
        $Retries = 0;
        While ($NewRole -eq $null -and $Retries -le 6)
        {
           Sleep -s 10
           New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $Application.ApplicationId | Write-Verbose -ErrorAction SilentlyContinue
           $NewRole = Get-AzureRMRoleAssignment -ServicePrincipalName $Application.ApplicationId -ErrorAction SilentlyContinue
           $Retries++;
        }
           return $Application.ApplicationId.ToString();
        }

        function CreateAutomationCertificateAsset ([string] $resourceGroup, [string] $automationAccountName, [string] $certifcateAssetName,[string] $certPath, [string] $certPlainPassword, [Boolean] $Exportable) {
        $CertPassword = ConvertTo-SecureString $certPlainPassword -AsPlainText -Force   
        Remove-AzureRmAutomationCertificate -ResourceGroupName $resourceGroup -AutomationAccountName $automationAccountName -Name $certifcateAssetName -ErrorAction SilentlyContinue
        New-AzureRmAutomationCertificate -ResourceGroupName $resourceGroup -AutomationAccountName $automationAccountName -Path $certPath -Name $certifcateAssetName -Password $CertPassword -Exportable:$Exportable  | write-verbose
        }

        function CreateAutomationConnectionAsset ([string] $resourceGroup, [string] $automationAccountName, [string] $connectionAssetName, [string] $connectionTypeName, [System.Collections.Hashtable] $connectionFieldValues ) {
        Remove-AzureRmAutomationConnection -ResourceGroupName $resourceGroup -AutomationAccountName $automationAccountName -Name $connectionAssetName -Force -ErrorAction SilentlyContinue
        New-AzureRmAutomationConnection -ResourceGroupName $ResourceGroup -AutomationAccountName $automationAccountName -Name $connectionAssetName -ConnectionTypeName $connectionTypeName -ConnectionFieldValues $connectionFieldValues
        }

        Import-Module AzureRM.Profile
        Import-Module AzureRM.Resources

        $AzureRMProfileVersion= (Get-Module AzureRM.Profile).Version
        if (!(($AzureRMProfileVersion.Major -ge 2 -and $AzureRMProfileVersion.Minor -ge 1) -or ($AzureRMProfileVersion.Major -gt 2)))
        {
           Write-Error -Message "Please install hello latest Azure PowerShell and retry. Relevant doc url : https://docs.microsoft.com/powershell/azureps-cmdlets-docs/ "
           return
        }

        Login-AzureRmAccount -EnvironmentName $EnvironmentName
        $Subscription = Select-AzureRmSubscription -SubscriptionId $SubscriptionId

        # Create a Run As account by using a service principal
        $CertifcateAssetName = "AzureRunAsCertificate"
        $ConnectionAssetName = "AzureRunAsConnection"
        $ConnectionTypeName = "AzureServicePrincipal"

        if ($EnterpriseCertPathForRunAsAccount -and $EnterpriseCertPlainPasswordForRunAsAccount) {
        $PfxCertPathForRunAsAccount = $EnterpriseCertPathForRunAsAccount
        $PfxCertPlainPasswordForRunAsAccount = $EnterpriseCertPlainPasswordForRunAsAccount
        } else {
          $CertificateName = $AutomationAccountName+$CertifcateAssetName
          $PfxCertPathForRunAsAccount = Join-Path $env:TEMP ($CertificateName + ".pfx")
          $PfxCertPlainPasswordForRunAsAccount = $SelfSignedCertPlainPassword
          $CerCertPathForRunAsAccount = Join-Path $env:TEMP ($CertificateName + ".cer")
          CreateSelfSignedCertificate $KeyVaultName $CertificateName $PfxCertPlainPasswordForRunAsAccount $PfxCertPathForRunAsAccount $CerCertPathForRunAsAccount $SelfSignedCertNoOfMonthsUntilExpired
        }

        # Create a service principal
        $PfxCert = New-Object -TypeName System.Security.Cryptography.X509Certificates.X509Certificate2 -ArgumentList @($PfxCertPathForRunAsAccount, $PfxCertPlainPasswordForRunAsAccount)
        $ApplicationId=CreateServicePrincipal $PfxCert $ApplicationDisplayName

        # Create hello Automation certificate asset
        CreateAutomationCertificateAsset $ResourceGroup $AutomationAccountName $CertifcateAssetName $PfxCertPathForRunAsAccount $PfxCertPlainPasswordForRunAsAccount $true

        # Populate hello ConnectionFieldValues
        $SubscriptionInfo = Get-AzureRmSubscription -SubscriptionId $SubscriptionId
        $TenantID = $SubscriptionInfo | Select TenantId -First 1
        $Thumbprint = $PfxCert.Thumbprint
        $ConnectionFieldValues = @{"ApplicationId" = $ApplicationId; "TenantId" = $TenantID.TenantId; "CertificateThumbprint" = $Thumbprint; "SubscriptionId" = $SubscriptionId}

        # Create an Automation connection asset named AzureRunAsConnection in hello Automation account. This connection uses hello service principal.
        CreateAutomationConnectionAsset $ResourceGroup $AutomationAccountName $ConnectionAssetName $ConnectionTypeName $ConnectionFieldValues

        if ($CreateClassicRunAsAccount) {
            # Create a Run As account by using a service principal
            $ClassicRunAsAccountCertifcateAssetName = "AzureClassicRunAsCertificate"
            $ClassicRunAsAccountConnectionAssetName = "AzureClassicRunAsConnection"
            $ClassicRunAsAccountConnectionTypeName = "AzureClassicCertificate "
            $UploadMessage = "Please upload hello .cer format of #CERT# toohello Management store by following hello steps below." + [Environment]::NewLine +
                    "Log in toohello Microsoft Azure Management portal (https://manage.windowsazure.com) and select Settings -> Management Certificates." + [Environment]::NewLine +
                    "Then click Upload and upload hello .cer format of #CERT#"

             if ($EnterpriseCertPathForClassicRunAsAccount -and $EnterpriseCertPlainPasswordForClassicRunAsAccount ) {
             $PfxCertPathForClassicRunAsAccount = $EnterpriseCertPathForClassicRunAsAccount
             $PfxCertPlainPasswordForClassicRunAsAccount = $EnterpriseCertPlainPasswordForClassicRunAsAccount
             $UploadMessage = $UploadMessage.Replace("#CERT#", $PfxCertPathForClassicRunAsAccount)
        } else {
             $ClassicRunAsAccountCertificateName = $AutomationAccountName+$ClassicRunAsAccountCertifcateAssetName
             $PfxCertPathForClassicRunAsAccount = Join-Path $env:TEMP ($ClassicRunAsAccountCertificateName + ".pfx")
             $PfxCertPlainPasswordForClassicRunAsAccount = $SelfSignedCertPlainPassword
             $CerCertPathForClassicRunAsAccount = Join-Path $env:TEMP ($ClassicRunAsAccountCertificateName + ".cer")
             $UploadMessage = $UploadMessage.Replace("#CERT#", $CerCertPathForClassicRunAsAccount)
             CreateSelfSignedCertificate $KeyVaultName $ClassicRunAsAccountCertificateName $PfxCertPlainPasswordForClassicRunAsAccount $PfxCertPathForClassicRunAsAccount $CerCertPathForClassicRunAsAccount $SelfSignedCertNoOfMonthsUntilExpired
        }

        # Create hello Automation certificate asset
        CreateAutomationCertificateAsset $ResourceGroup $AutomationAccountName $ClassicRunAsAccountCertifcateAssetName $PfxCertPathForClassicRunAsAccount $PfxCertPlainPasswordForClassicRunAsAccount $false

        # Populate hello ConnectionFieldValues
        $SubscriptionName = $subscription.Subscription.SubscriptionName
        $ClassicRunAsAccountConnectionFieldValues = @{"SubscriptionName" = $SubscriptionName; "SubscriptionId" = $SubscriptionId; "CertificateAssetName" = $ClassicRunAsAccountCertifcateAssetName}

        # Create an Automation connection asset named AzureRunAsConnection in hello Automation account. This connection uses hello service principal.
        CreateAutomationConnectionAsset $ResourceGroup $AutomationAccountName $ClassicRunAsAccountConnectionAssetName $ClassicRunAsAccountConnectionTypeName $ClassicRunAsAccountConnectionFieldValues

        Write-Host -ForegroundColor red $UploadMessage
        }

2. <span data-ttu-id="16352-143">在您的電腦上啟動**Windows PowerShell**從 hello**啟動**螢幕，以提高的使用者權限。</span><span class="sxs-lookup"><span data-stu-id="16352-143">On your computer, start **Windows PowerShell** from hello **Start** screen with elevated user rights.</span></span>
3. <span data-ttu-id="16352-144">Hello 從提高權限的命令列殼層，移 toohello 資料夾包含您在步驟 1 中建立的 hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="16352-144">From hello elevated command-line shell, go toohello folder that contains hello script you created in step 1.</span></span>  
4. <span data-ttu-id="16352-145">您需要的 hello 組態使用 hello 參數值執行 hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="16352-145">Execute hello script by using hello parameter values for hello configuration you require.</span></span>

    <span data-ttu-id="16352-146">**使用自我簽署憑證建立執行身分帳戶**</span><span class="sxs-lookup"><span data-stu-id="16352-146">**Create a Run As account by using a self-signed certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $false`

    <span data-ttu-id="16352-147">**使用自我簽署憑證建立執行身分帳戶和傳統執行身分帳戶**</span><span class="sxs-lookup"><span data-stu-id="16352-147">**Create a Run As account and a Classic Run As account by using a self-signed certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true`

    <span data-ttu-id="16352-148">**使用企業憑證建立執行身分帳戶和傳統執行身分帳戶**</span><span class="sxs-lookup"><span data-stu-id="16352-148">**Create a Run As account and a Classic Run As account by using an enterprise certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication>  -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true -EnterpriseCertPathForRunAsAccount <EnterpriseCertPfxPathForRunAsAccount> -EnterpriseCertPlainPasswordForRunAsAccount <StrongPassword> -EnterpriseCertPathForClassicRunAsAccount <EnterpriseCertPfxPathForClassicRunAsAccount> -EnterpriseCertPlainPasswordForClassicRunAsAccount <StrongPassword>`

    <span data-ttu-id="16352-149">**使用自我簽署的憑證 hello Azure 政府雲端中建立執行身分帳戶和傳統執行身分帳戶**</span><span class="sxs-lookup"><span data-stu-id="16352-149">**Create a Run As account and a Classic Run As account by using a self-signed certificate in hello Azure Government cloud**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true  -EnvironmentName AzureUSGovernment`

    > [!NOTE]
    > <span data-ttu-id="16352-150">Hello 指令碼執行之後，您將會提示的 tooauthenticate 與 Azure。</span><span class="sxs-lookup"><span data-stu-id="16352-150">After hello script has executed, you will be prompted tooauthenticate with Azure.</span></span> <span data-ttu-id="16352-151">使用屬於 hello 訂用帳戶系統管理員角色的成員和 hello 訂用帳戶的共同管理員帳戶登入。</span><span class="sxs-lookup"><span data-stu-id="16352-151">Sign in with an account that is a member of hello subscription administrators role and co-administrator of hello subscription.</span></span>
    >
    >

<span data-ttu-id="16352-152">Hello 指令碼順利執行之後，請注意 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="16352-152">After hello script has executed successfully, note hello following:</span></span>
* <span data-ttu-id="16352-153">如果您使用自我簽署的公開憑證 （.cer 檔案） 建立傳統執行身分帳戶，hello 指令碼建立，並將它 hello 使用者設定檔在電腦上儲存 toohello 暫存檔案資料夾*%USERPROFILE%\AppData\Local\Temp*，使用 tooexecute hello PowerShell 工作階段。</span><span class="sxs-lookup"><span data-stu-id="16352-153">If you created a Classic Run As account with a self-signed public certificate (.cer file), hello script creates and saves it toohello temporary files folder on your computer under hello user profile *%USERPROFILE%\AppData\Local\Temp*, which you used tooexecute hello PowerShell session.</span></span>
* <span data-ttu-id="16352-154">如果您使用企業公開憑證 (.cer 檔案) 建立了傳統執行身分帳戶，請使用此憑證。</span><span class="sxs-lookup"><span data-stu-id="16352-154">If you created a Classic Run As account with an enterprise public certificate (.cer file), use this certificate.</span></span> <span data-ttu-id="16352-155">請依照指示 hello[上傳 Azure 傳統入口網站管理 API 憑證 toohello](../azure-api-management-certs.md)，並使用 hello 驗證使用傳統部署資源的 hello 認證組態[範例程式碼使用 Azure 傳統部署資源 tooauthenticate](automation-verify-runas-authentication.md#classic-run-as-authentication)。</span><span class="sxs-lookup"><span data-stu-id="16352-155">Follow hello instructions for [uploading a management API certificate toohello Azure classic portal](../azure-api-management-certs.md), and then validate hello credential configuration with classic deployment resources by using hello [sample code tooauthenticate with Azure Classic Deployment Resources](automation-verify-runas-authentication.md#classic-run-as-authentication).</span></span> 
* <span data-ttu-id="16352-156">如果您未*不*建立傳統執行身分帳戶、 向資源管理員資源及驗證 hello 認證組態使用 hello[範例程式碼來驗證服務管理資源](automation-verify-runas-authentication.md#automation-run-as-authentication)。</span><span class="sxs-lookup"><span data-stu-id="16352-156">If you did *not* create a Classic Run As account, authenticate with Resource Manager resources and validate hello credential configuration by using hello [sample code for authenticating with Service Management resources](automation-verify-runas-authentication.md#automation-run-as-authentication).</span></span>

## <a name="next-steps"></a><span data-ttu-id="16352-157">後續步驟</span><span class="sxs-lookup"><span data-stu-id="16352-157">Next steps</span></span>
* <span data-ttu-id="16352-158">如需有關服務主體的詳細資訊，請參閱太[應用程式與服務主體物件](../active-directory/active-directory-application-objects.md)。</span><span class="sxs-lookup"><span data-stu-id="16352-158">For more information about Service Principals, refer too[Application Objects and Service Principal Objects](../active-directory/active-directory-application-objects.md).</span></span>
* <span data-ttu-id="16352-159">如需有關憑證和 Azure 服務的詳細資訊，請參閱太[Azure 雲端服務憑證概觀](../cloud-services/cloud-services-certs-create.md)。</span><span class="sxs-lookup"><span data-stu-id="16352-159">For more information about certificates and Azure services, refer too[Certificates overview for Azure Cloud Services](../cloud-services/cloud-services-certs-create.md).</span></span>
