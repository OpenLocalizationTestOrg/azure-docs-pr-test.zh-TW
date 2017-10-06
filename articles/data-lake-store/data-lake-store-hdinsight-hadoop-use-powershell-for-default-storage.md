---
title: "aaaCreate HDInsight 叢集與資料湖存放區作為預設儲存體使用 PowerShell |Microsoft 文件 '"
description: "使用 Azure PowerShell toocreate 和使用 Azure Data Lake Store 的 HDInsight 叢集"
services: data-lake-store,hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 8917af15-8e37-46cf-87ad-4e6d5d67ecdb
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/08/2017
ms.author: nitinme
ms.openlocfilehash: a5c0ad416da6ad9bd07204af2ebb6b7470916085
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-hdinsight-clusters-with-data-lake-store-as-default-storage-by-using-powershell"></a><span data-ttu-id="af116-103">使用 PowerShell 建立以 Data Lake Store 做為預設儲存體的 HDInsight 叢集</span><span class="sxs-lookup"><span data-stu-id="af116-103">Create HDInsight clusters with Data Lake Store as default storage by using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="af116-104">使用 hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="af116-104">Use hello Azure portal</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
> * [<span data-ttu-id="af116-105">使用 PowerShell (針對預設儲存體)</span><span class="sxs-lookup"><span data-stu-id="af116-105">Use PowerShell (for default storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
> * [<span data-ttu-id="af116-106">使用 PowerShell (針對額外儲存體)</span><span class="sxs-lookup"><span data-stu-id="af116-106">Use PowerShell (for additional storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell.md)
> * [<span data-ttu-id="af116-107">使用 Resource Manager</span><span class="sxs-lookup"><span data-stu-id="af116-107">Use Resource Manager</span></span>](data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)

<span data-ttu-id="af116-108">了解如何 toouse Azure PowerShell tooconfigure Azure HDInsight 叢集與 Azure Data Lake Store，做為預設儲存體。</span><span class="sxs-lookup"><span data-stu-id="af116-108">Learn how toouse Azure PowerShell tooconfigure Azure HDInsight clusters with Azure Data Lake Store, as default storage.</span></span> <span data-ttu-id="af116-109">如需有關如何建立以 Data Lake Store 做為額外儲存體的 HDInsight 叢集之指示，請參閱[建立以 Data Lake Store 做為額外儲存體的 HDInsight 叢集](data-lake-store-hdinsight-hadoop-use-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="af116-109">For instructions on creating an HDInsight cluster with Data Lake Store as additional storage, see [Create an HDInsight cluster with Data Lake Store as additional storage](data-lake-store-hdinsight-hadoop-use-powershell.md).</span></span>

<span data-ttu-id="af116-110">以下是使用 HDInsight 搭配 Data Lake Store 的一些重要考量：</span><span class="sxs-lookup"><span data-stu-id="af116-110">Here are some important considerations for using HDInsight with Data Lake Store:</span></span>

* <span data-ttu-id="af116-111">hello 選項 toocreate 具有存取權的 HDInsight 叢集已可供 HDInsight 版本 3.5 和 3.6 tooData 湖存放區做為預設儲存體。</span><span class="sxs-lookup"><span data-stu-id="af116-111">hello option toocreate HDInsight clusters with access tooData Lake Store as default storage is available for HDInsight version 3.5 and 3.6.</span></span>

* <span data-ttu-id="af116-112">HDInsight 叢集與 hello 選項 toocreate 存取 tooData 湖存放區，因為預設儲存體*無法使用*的高階 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="af116-112">hello option toocreate HDInsight clusters with access tooData Lake Store as default storage is *not available* for HDInsight Premium clusters.</span></span>

<span data-ttu-id="af116-113">tooconfigure HDInsight toowork 與資料湖存放區使用 PowerShell，請遵循 hello 接下來五個區段中的 hello 指示。</span><span class="sxs-lookup"><span data-stu-id="af116-113">tooconfigure HDInsight toowork with Data Lake Store by using PowerShell, follow hello instructions in hello next five sections.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="af116-114">必要條件</span><span class="sxs-lookup"><span data-stu-id="af116-114">Prerequisites</span></span>
<span data-ttu-id="af116-115">開始本教學課程之前，請確定您符合下列需求的 hello:</span><span class="sxs-lookup"><span data-stu-id="af116-115">Before you begin this tutorial, make sure that you meet hello following requirements:</span></span>

* <span data-ttu-id="af116-116">**Azure 訂用帳戶**： 跳過[取得 Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="af116-116">**An Azure subscription**: Go too[Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="af116-117">**Azure PowerShell 1.0 或更高**： 請參閱[如何 tooinstall 和設定 PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="af116-117">**Azure PowerShell 1.0 or greater**: See [How tooinstall and configure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="af116-118">**Windows 軟體開發套件 (SDK)**: tooinstall Windows SDK，跳過[下載和工具適用於 Windows 10](https://dev.windows.com/en-us/downloads)。</span><span class="sxs-lookup"><span data-stu-id="af116-118">**Windows Software Development Kit (SDK)**: tooinstall Windows SDK, go too[Downloads and tools for Windows 10](https://dev.windows.com/en-us/downloads).</span></span> <span data-ttu-id="af116-119">hello SDK 會使用的 toocreate 安全性憑證。</span><span class="sxs-lookup"><span data-stu-id="af116-119">hello SDK is used toocreate a security certificate.</span></span>
* <span data-ttu-id="af116-120">**Azure Active Directory 服務主體**： 這個教學課程描述如何 toocreate Azure Active Directory (Azure AD) 中的服務主體。</span><span class="sxs-lookup"><span data-stu-id="af116-120">**Azure Active Directory service principal**: This tutorial describes how toocreate a service principal in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="af116-121">不過，toocreate 服務主體，您必須是 Azure AD 系統管理員。</span><span class="sxs-lookup"><span data-stu-id="af116-121">However, toocreate a service principal, you must be an Azure AD administrator.</span></span> <span data-ttu-id="af116-122">如果您是系統管理員，則可以略過這項必要條件，並繼續進行 hello 教學課程。</span><span class="sxs-lookup"><span data-stu-id="af116-122">If you are an administrator, you can skip this prerequisite and proceed with hello tutorial.</span></span>

    >[!NOTE]
    ><span data-ttu-id="af116-123">唯有您是 Azure AD 系統管理員，才可以建立服務主體。</span><span class="sxs-lookup"><span data-stu-id="af116-123">You can create a service principal only if you are an Azure AD administrator.</span></span> <span data-ttu-id="af116-124">您的 Azure AD 系統管理員必須先建立服務主體，您才能建立搭配 Data Lake Store 的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="af116-124">Your Azure AD administrator must create a service principal before you can create an HDInsight cluster with Data Lake Store.</span></span> <span data-ttu-id="af116-125">hello 服務主體必須以建立憑證，如中所述[建立服務主體與憑證](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority)。</span><span class="sxs-lookup"><span data-stu-id="af116-125">hello service principal must be created with a certificate, as described in [Create a service principal with certificate](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).</span></span>
    >

## <a name="create-a-data-lake-store-account"></a><span data-ttu-id="af116-126">建立 Data Lake Store 帳戶</span><span class="sxs-lookup"><span data-stu-id="af116-126">Create a Data Lake Store account</span></span>
<span data-ttu-id="af116-127">toocreate Data Lake Store 帳戶，不要 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="af116-127">toocreate a Data Lake Store account, do hello following:</span></span>

1. <span data-ttu-id="af116-128">從您的桌面上，開啟 PowerShell 視窗，，然後輸入下列程式片段 hello。</span><span class="sxs-lookup"><span data-stu-id="af116-128">From your desktop, open a PowerShell window, and then enter hello snippets below.</span></span> <span data-ttu-id="af116-129">當您準備提示的 toosign 中做為其中一個 hello 訂用帳戶管理員或擁有者的登入。</span><span class="sxs-lookup"><span data-stu-id="af116-129">When you are prompted toosign in, sign in as one of hello subscription administrators or owners.</span></span> 

        # Sign in tooyour Azure account
        Login-AzureRmAccount

        # List all hello subscriptions associated tooyour account
        Get-AzureRmSubscription

        # Select a subscription
        Set-AzureRmContext -SubscriptionId <subscription ID>

        # Register for Data Lake Store
        Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.DataLakeStore"

    > [!NOTE]
    > <span data-ttu-id="af116-130">如果您註冊 hello 資料湖存放區資源提供者，會收到類似的錯誤太`Register-AzureRmResourceProvider : InvalidResourceNamespace: hello resource namespace 'Microsoft.DataLakeStore' is invalid`，您的訂閱可能無法在允許清單中的資料湖存放區。</span><span class="sxs-lookup"><span data-stu-id="af116-130">If you register hello Data Lake Store resource provider and receive an error similar too`Register-AzureRmResourceProvider : InvalidResourceNamespace: hello resource namespace 'Microsoft.DataLakeStore' is invalid`, your subscription might not be whitelisted for Data Lake Store.</span></span> <span data-ttu-id="af116-131">tooenable Azure 的訂用帳戶 hello Data Lake Store 公開預覽，請依照中的 hello 指示[使用 hello Azure 入口網站開始使用 Azure Data Lake Store](data-lake-store-get-started-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="af116-131">tooenable your Azure subscription for hello Data Lake Store public preview, follow hello instructions in [Get started with Azure Data Lake Store by using hello Azure portal](data-lake-store-get-started-portal.md).</span></span>
    >

2. <span data-ttu-id="af116-132">Data Lake Store 帳戶與 Azure 資源群組相關聯。</span><span class="sxs-lookup"><span data-stu-id="af116-132">A Data Lake Store account is associated with an Azure resource group.</span></span> <span data-ttu-id="af116-133">從建立資源群組著手。</span><span class="sxs-lookup"><span data-stu-id="af116-133">Start by creating a resource group.</span></span>

        $resourceGroupName = "<your new resource group name>"
        New-AzureRmResourceGroup -Name $resourceGroupName -Location "East US 2"

    <span data-ttu-id="af116-134">您應該會看到如下的輸出：</span><span class="sxs-lookup"><span data-stu-id="af116-134">You should see an output like this:</span></span>

        ResourceGroupName : hdiadlgrp
        Location          : eastus2
        ProvisioningState : Succeeded
        Tags              :
        ResourceId        : /subscriptions/<subscription-id>/resourceGroups/hdiadlgrp

3. <span data-ttu-id="af116-135">建立 Data Lake Store 帳戶。</span><span class="sxs-lookup"><span data-stu-id="af116-135">Create a Data Lake Store account.</span></span> <span data-ttu-id="af116-136">您指定的名稱必須包含小寫字母和數字的 hello 帳戶。</span><span class="sxs-lookup"><span data-stu-id="af116-136">hello account name you specify must contain only lowercase letters and numbers.</span></span>

        $dataLakeStoreName = "<your new Data Lake Store name>"
        New-AzureRmDataLakeStoreAccount -ResourceGroupName $resourceGroupName -Name $dataLakeStoreName -Location "East US 2"

    <span data-ttu-id="af116-137">您應該會看到類似 hello 下列輸出：</span><span class="sxs-lookup"><span data-stu-id="af116-137">You should see an output like hello following:</span></span>

        ...
        ProvisioningState           : Succeeded
        State                       : Active
        CreationTime                : 5/5/2017 10:53:56 PM
        EncryptionState             : Enabled
        ...
        LastModifiedTime            : 5/5/2017 10:53:56 PM
        Endpoint                    : hdiadlstore.azuredatalakestore.net
        DefaultGroup                :
        Id                          : /subscriptions/<subscription-id>/resourceGroups/hdiadlgrp/providers/Microsoft.DataLakeStore/accounts/hdiadlstore
        Name                        : hdiadlstore
        Type                        : Microsoft.DataLakeStore/accounts
        Location                    : East US 2
        Tags                        : {}

4. <span data-ttu-id="af116-138">使用 Data Lake Store 當做預設儲存體需要您 toospecify 根路徑 toowhich hello 特定叢集的檔案會複製在叢集建立期間。</span><span class="sxs-lookup"><span data-stu-id="af116-138">Using Data Lake Store as default storage requires you toospecify a root path toowhich hello cluster-specific files are copied during cluster creation.</span></span> <span data-ttu-id="af116-139">根的路徑，也就是 toocreate **/叢集/hdiadlcluster** hello 片段中使用下列 cmdlet 的 hello:</span><span class="sxs-lookup"><span data-stu-id="af116-139">toocreate a root path, which is **/clusters/hdiadlcluster** in hello  snippet, use hello following cmdlets:</span></span>

        $myrootdir = "/"
        New-AzureRmDataLakeStoreItem -Folder -AccountName $dataLakeStoreName -Path $myrootdir/clusters/hdiadlcluster


## <a name="set-up-authentication-for-role-based-access-toodata-lake-store"></a><span data-ttu-id="af116-140">設定以角色為基礎的驗證存取 tooData 湖存放區</span><span class="sxs-lookup"><span data-stu-id="af116-140">Set up authentication for role-based access tooData Lake Store</span></span>
<span data-ttu-id="af116-141">每一個 Azure 訂用帳戶都與 Azure AD 實體相關聯。</span><span class="sxs-lookup"><span data-stu-id="af116-141">Every Azure subscription is associated with an Azure AD entity.</span></span> <span data-ttu-id="af116-142">使用者和服務存取訂用帳戶資源使用 hello Azure 入口網站或 hello Azure 資源管理員 API 首先必須向 Azure AD。</span><span class="sxs-lookup"><span data-stu-id="af116-142">Users and services that access subscription resources by using hello Azure portal or hello Azure Resource Manager API must first authenticate with Azure AD.</span></span> <span data-ttu-id="af116-143">已授與存取 tooAzure 訂閱和服務由將其指派 hello Azure 資源上的適當角色。</span><span class="sxs-lookup"><span data-stu-id="af116-143">Access is granted tooAzure subscriptions and services by assigning them hello appropriate role on an Azure resource.</span></span> <span data-ttu-id="af116-144">為服務，服務主體識別 Azure AD 中的 hello 服務。</span><span class="sxs-lookup"><span data-stu-id="af116-144">For services, a service principal identifies hello service in Azure AD.</span></span>

<span data-ttu-id="af116-145">本節說明 toogrant 應用程式的服務方式，例如 HDInsight，存取 tooan Azure 資源 (hello 您稍早建立的 Data Lake Store 帳戶)。</span><span class="sxs-lookup"><span data-stu-id="af116-145">This section illustrates how toogrant an application service, such as HDInsight, access tooan Azure resource (hello Data Lake Store account that you created earlier).</span></span> <span data-ttu-id="af116-146">您藉由建立服務主體的 hello 應用程式，並指派角色 tooit 透過 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="af116-146">You do so by creating a service principal for hello application and assigning roles tooit via PowerShell.</span></span>

<span data-ttu-id="af116-147">設定 Active Directory 驗證的 Azure 資料湖，tooset hello 中執行下列兩個區段的 hello。</span><span class="sxs-lookup"><span data-stu-id="af116-147">tooset up Active Directory authentication for Azure Data Lake, perform hello tasks in hello following two sections.</span></span>

### <a name="create-a-self-signed-certificate"></a><span data-ttu-id="af116-148">建立自我簽署憑證</span><span class="sxs-lookup"><span data-stu-id="af116-148">Create a self-signed certificate</span></span>
<span data-ttu-id="af116-149">請確定您有[Windows SDK](https://dev.windows.com/en-us/downloads) hello 進行這一節的步驟之前安裝。</span><span class="sxs-lookup"><span data-stu-id="af116-149">Make sure you have [Windows SDK](https://dev.windows.com/en-us/downloads) installed before proceeding with hello steps in this section.</span></span> <span data-ttu-id="af116-150">您必須也建立目錄，例如*C:\mycertdir*您用來建立 hello 憑證。</span><span class="sxs-lookup"><span data-stu-id="af116-150">You must have also created a directory, such as *C:\mycertdir*, where you create hello certificate.</span></span>

1. <span data-ttu-id="af116-151">從 hello PowerShell 視窗，請移 toohello 安裝 Windows SDK 的位置 (通常*C:\Program Files (x86) \Windows Kits\10\bin\x86*)，並使用 hello [MakeCert] [ makecert]公用程式 toocreate 自我簽署的憑證和私密金鑰。</span><span class="sxs-lookup"><span data-stu-id="af116-151">From hello PowerShell window, go toohello location where you installed Windows SDK (typically, *C:\Program Files (x86)\Windows Kits\10\bin\x86*) and use hello [MakeCert][makecert] utility toocreate a self-signed certificate and a private key.</span></span> <span data-ttu-id="af116-152">使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="af116-152">Use hello following commands:</span></span>

        $certificateFileDir = "<my certificate directory>"
        cd $certificateFileDir

        makecert -sv mykey.pvk -n "cn=HDI-ADL-SP" CertFile.cer -r -len 2048

    <span data-ttu-id="af116-153">系統會提示的 tooenter hello 私密金鑰密碼。</span><span class="sxs-lookup"><span data-stu-id="af116-153">You will be prompted tooenter hello private key password.</span></span> <span data-ttu-id="af116-154">Hello 命令執行成功之後，您應該會看到**CertFile.cer**和**mykey.pvk** hello 憑證，您所指定目錄中。</span><span class="sxs-lookup"><span data-stu-id="af116-154">After hello command is successfully executed, you should see **CertFile.cer** and **mykey.pvk** in hello certificate directory that you specified.</span></span>
2. <span data-ttu-id="af116-155">使用 hello [Pvk2Pfx] [ pvk2pfx]公用程式 tooconvert hello.pvk 和.cer 檔案 MakeCert 建立的 tooa.pfx 檔案。</span><span class="sxs-lookup"><span data-stu-id="af116-155">Use hello [Pvk2Pfx][pvk2pfx] utility tooconvert hello .pvk and .cer files that MakeCert created tooa .pfx file.</span></span> <span data-ttu-id="af116-156">執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="af116-156">Run hello following command:</span></span>

        pvk2pfx -pvk mykey.pvk -spc CertFile.cer -pfx CertFile.pfx -po <password>

    <span data-ttu-id="af116-157">當系統提示您時，輸入 hello 私密金鑰密碼您稍早指定。</span><span class="sxs-lookup"><span data-stu-id="af116-157">When you are prompted, enter hello private key password that you specified earlier.</span></span> <span data-ttu-id="af116-158">hello 指定 hello 值**po**參數是 hello 與 hello.pfx 檔案相關聯的密碼。</span><span class="sxs-lookup"><span data-stu-id="af116-158">hello value you specify for hello **-po** parameter is hello password that's associated with hello .pfx file.</span></span> <span data-ttu-id="af116-159">Hello 命令已順利完成之後，您應該也會看到**CertFile.pfx** hello 憑證，您所指定目錄中。</span><span class="sxs-lookup"><span data-stu-id="af116-159">After hello command has been completed successfully, you should also see a **CertFile.pfx** in hello certificate directory that you specified.</span></span>

### <a name="create-an-azure-ad-and-a-service-principal"></a><span data-ttu-id="af116-160">建立 Azure AD 和服務主體</span><span class="sxs-lookup"><span data-stu-id="af116-160">Create an Azure AD and a service principal</span></span>
<span data-ttu-id="af116-161">在本節中，您可以建立 Azure AD 應用程式的服務主體、 指派角色 toohello 服務主體，以及 hello 服務主體以驗證所提供的憑證。</span><span class="sxs-lookup"><span data-stu-id="af116-161">In this section, you create a service principal for an Azure AD application, assign a role toohello service principal, and authenticate as hello service principal by providing a certificate.</span></span> <span data-ttu-id="af116-162">toocreate 應用程式在 Azure AD 中，執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="af116-162">toocreate an application in Azure AD, run hello following commands:</span></span>

1. <span data-ttu-id="af116-163">貼上下列指令程式 hello PowerShell 主控台視窗中的 hello。</span><span class="sxs-lookup"><span data-stu-id="af116-163">Paste hello following cmdlets in hello PowerShell console window.</span></span> <span data-ttu-id="af116-164">請確定您指定 hello 的 hello 該值**-DisplayName**屬性是唯一的。</span><span class="sxs-lookup"><span data-stu-id="af116-164">Make sure that hello value you specify for hello **-DisplayName** property is unique.</span></span> <span data-ttu-id="af116-165">hello 值**-首頁**和**-IdentiferUris**預留位置值，並不會驗證。</span><span class="sxs-lookup"><span data-stu-id="af116-165">hello values for **-HomePage** and **-IdentiferUris** are placeholder values and are not verified.</span></span>

        $certificateFilePath = "$certificateFileDir\CertFile.pfx"

        $password = Read-Host –Prompt "Enter hello password" # This is hello password you specified for hello .pfx file

        $certificatePFX = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2($certificateFilePath, $password)

        $rawCertificateData = $certificatePFX.GetRawCertData()

        $credential = [System.Convert]::ToBase64String($rawCertificateData)

        $application = New-AzureRmADApplication `
            -DisplayName "HDIADL" `
            -HomePage "https://contoso.com" `
            -IdentifierUris "https://mycontoso.com" `
            -CertValue $credential  `
            -StartDate $certificatePFX.NotBefore  `
            -EndDate $certificatePFX.NotAfter

        $applicationId = $application.ApplicationId
2. <span data-ttu-id="af116-166">建立服務主體使用 hello 應用程式識別碼。</span><span class="sxs-lookup"><span data-stu-id="af116-166">Create a service principal by using hello application ID.</span></span>

        $servicePrincipal = New-AzureRmADServicePrincipal -ApplicationId $applicationId

        $objectId = $servicePrincipal.Id
3. <span data-ttu-id="af116-167">授與 hello 服務主體存取 toohello Data Lake Store 根和您稍早指定的 hello 根路徑中的所有 hello 資料夾。</span><span class="sxs-lookup"><span data-stu-id="af116-167">Grant hello service principal access toohello Data Lake Store root and all hello folders in hello root path that you specified earlier.</span></span> <span data-ttu-id="af116-168">使用下列 cmdlet 的 hello:</span><span class="sxs-lookup"><span data-stu-id="af116-168">Use hello following cmdlets:</span></span>

        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path / -AceType User -Id $objectId -Permissions All
        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path /clusters -AceType User -Id $objectId -Permissions All
        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path /clusters/hdiadlcluster -AceType User -Id $objectId -Permissions All

## <a name="create-an-hdinsight-linux-cluster-with-data-lake-store-as-hello-default-storage"></a><span data-ttu-id="af116-169">建立具有 Data Lake Store 的 HDInsight Linux 叢集為 hello 預設儲存體</span><span class="sxs-lookup"><span data-stu-id="af116-169">Create an HDInsight Linux cluster with Data Lake Store as hello default storage</span></span>

<span data-ttu-id="af116-170">在本節中，您建立 HDInsight Hadoop Linux 叢集與資料湖存放區作為 hello 預設儲存體。</span><span class="sxs-lookup"><span data-stu-id="af116-170">In this section, you create an HDInsight Hadoop Linux cluster with Data Lake Store as hello default storage.</span></span> <span data-ttu-id="af116-171">此版本中，hello HDInsight 叢集，且資料湖存放區必須為 hello 相同的位置。</span><span class="sxs-lookup"><span data-stu-id="af116-171">For this release, hello HDInsight cluster and Data Lake Store must be in hello same location.</span></span>

1. <span data-ttu-id="af116-172">擷取 hello 訂用帳戶的租用戶識別碼，並將它儲存 toouse 更新版本。</span><span class="sxs-lookup"><span data-stu-id="af116-172">Retrieve hello subscription tenant ID, and store it toouse later.</span></span>

        $tenantID = (Get-AzureRmContext).Tenant.TenantId

2. <span data-ttu-id="af116-173">使用下列 cmdlet 的 hello 建立 hello HDInsight 叢集：</span><span class="sxs-lookup"><span data-stu-id="af116-173">Create hello HDInsight cluster by using hello following cmdlets:</span></span>

        # Set these variables

        $location = "East US 2"
        $storageAccountName = $dataLakeStoreName                       # Data Lake Store account name
        $storageRootPath = "<Storage root path you specified earlier>" # E.g. /clusters/hdiadlcluster
        $clusterName = "<unique cluster name>"
        $clusterNodes = <ClusterSizeInNodes>            # hello number of nodes in hello HDInsight cluster
        $httpCredentials = Get-Credential
        $sshCredentials = Get-Credential

        New-AzureRmHDInsightCluster `
               -ClusterType Hadoop `
               -OSType Linux `
               -ClusterSizeInNodes $clusterNodes `
               -ResourceGroupName $resourceGroupName `
               -ClusterName $clusterName `
               -HttpCredential $httpCredentials `
               -Location $location `
               -DefaultStorageAccountType AzureDataLakeStore `
               -DefaultStorageAccountName "$storageAccountName.azuredatalakestore.net" `
               -DefaultStorageRootPath $storageRootPath `
               -Version "3.6" `
               -SshCredential $sshCredentials `
               -AadTenantId $tenantId `
               -ObjectId $objectId `
               -CertificateFilePath $certificateFilePath `
               -CertificatePassword $password

    <span data-ttu-id="af116-174">Hello 指令程式已順利完成之後，您應該會看到列出 hello 叢集詳細資料的輸出。</span><span class="sxs-lookup"><span data-stu-id="af116-174">After hello cmdlet has been successfully completed, you should see an output that lists hello cluster details.</span></span>

## <a name="run-test-jobs-on-hello-hdinsight-cluster-toouse-data-lake-store"></a><span data-ttu-id="af116-175">Hello HDInsight 叢集 toouse 資料湖存放區上執行測試工作</span><span class="sxs-lookup"><span data-stu-id="af116-175">Run test jobs on hello HDInsight cluster toouse Data Lake Store</span></span>
<span data-ttu-id="af116-176">您已設定的 HDInsight 叢集之後，您可以測試工作在其上執行 tooensure 能夠存取資料湖存放區。</span><span class="sxs-lookup"><span data-stu-id="af116-176">After you have configured an HDInsight cluster, you can run test jobs on it tooensure that it can access Data Lake Store.</span></span> <span data-ttu-id="af116-177">toodo，執行範例 Hive 工作 toocreate 使用已經在資料湖存放區中的 hello 範例資料的資料表 *<cluster root>/example/data/sample.log*。</span><span class="sxs-lookup"><span data-stu-id="af116-177">toodo so, run a sample Hive job toocreate a table that uses hello sample data that's already available in Data Lake Store at *<cluster root>/example/data/sample.log*.</span></span>

<span data-ttu-id="af116-178">在本節中，您進行安全殼層 (SSH) 連線到 hello 您建立 HDInsight Linux 叢集，然後您執行範例 Hive 查詢。</span><span class="sxs-lookup"><span data-stu-id="af116-178">In this section, you make a Secure Shell (SSH) connection into hello HDInsight Linux cluster that you created, and then you run a sample Hive query.</span></span>

* <span data-ttu-id="af116-179">如果您使用 Windows 用戶端 toomake SSH 連線到 hello 叢集中，請參閱[搭配使用 SSH 和從 Windows 的 HDInsight 上的 Linux Hadoop](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md)。</span><span class="sxs-lookup"><span data-stu-id="af116-179">If you are using a Windows client toomake an SSH connection into hello cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span></span>
* <span data-ttu-id="af116-180">如果您使用 Linux 用戶端 toomake SSH 連線到 hello 叢集中，請參閱[搭配使用 SSH 和 Linux 的 HDInsight 上的 Linux Hadoop](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="af116-180">If you are using a Linux client toomake an SSH connection into hello cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

1. <span data-ttu-id="af116-181">Hello 連接之後，請使用下列命令的 hello 啟動 hello Hive 命令列介面 (CLI):</span><span class="sxs-lookup"><span data-stu-id="af116-181">After you have made hello connection, start hello Hive command-line interface (CLI) by using hello following command:</span></span>

        hive
2. <span data-ttu-id="af116-182">下列陳述式 toocreate 名為的新資料表使用 hello CLI tooenter hello**車輛**利用資料湖存放區中的 hello 範例資料：</span><span class="sxs-lookup"><span data-stu-id="af116-182">Use hello CLI tooenter hello following statements toocreate a new table named **vehicles** by using hello sample data in Data Lake Store:</span></span>

        DROP TABLE log4jLogs;
        CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
        STORED AS TEXTFILE LOCATION 'adl:///example/data/';
        SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

    <span data-ttu-id="af116-183">您應該會看到 hello 查詢輸出 hello SSH 主控台上。</span><span class="sxs-lookup"><span data-stu-id="af116-183">You should see hello query output on hello SSH console.</span></span>

    >[!NOTE]
    ><span data-ttu-id="af116-184">hello hello 上述 CREATE TABLE 命令中的路徑 toohello 範例資料是`adl:///example/data/`，其中`adl:///`hello 叢集根目錄。</span><span class="sxs-lookup"><span data-stu-id="af116-184">hello path toohello sample data in hello preceding CREATE TABLE command is `adl:///example/data/`, where `adl:///` is hello cluster root.</span></span> <span data-ttu-id="af116-185">指定在此教學課程中的 hello 叢集根目錄 hello 範例，下列是 hello 命令`adl://hdiadlstore.azuredatalakestore.net/clusters/hdiadlcluster`。</span><span class="sxs-lookup"><span data-stu-id="af116-185">Following hello example of hello cluster root that's specified in this tutorial, hello command is `adl://hdiadlstore.azuredatalakestore.net/clusters/hdiadlcluster`.</span></span> <span data-ttu-id="af116-186">您可以使用 hello 較短的替代方案，或提供 hello 完整路徑 toohello 叢集根目錄。</span><span class="sxs-lookup"><span data-stu-id="af116-186">You can either use hello shorter alternative or provide hello complete path toohello cluster root.</span></span>
    >

## <a name="access-data-lake-store-by-using-hdfs-commands"></a><span data-ttu-id="af116-187">使用 HDFS 命令存取 Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="af116-187">Access Data Lake Store by using HDFS commands</span></span>
<span data-ttu-id="af116-188">設定 hello HDInsight 叢集 toouse 資料湖存放區之後，您可以使用 Hadoop 分散式檔案系統 (HDFS) 殼層命令 tooaccess hello 存放區。</span><span class="sxs-lookup"><span data-stu-id="af116-188">After you have configured hello HDInsight cluster toouse Data Lake Store, you can use Hadoop Distributed File System (HDFS) shell commands tooaccess hello store.</span></span>

<span data-ttu-id="af116-189">在本節中，確定 SSH 連線到 hello 您建立 HDInsight Linux 叢集，然後您執行 hello HDFS 命令。</span><span class="sxs-lookup"><span data-stu-id="af116-189">In this section, you make an SSH connection into hello HDInsight Linux cluster that you created, and then you run hello HDFS commands.</span></span>

* <span data-ttu-id="af116-190">如果您使用 Windows 用戶端 toomake SSH 連線到 hello 叢集中，請參閱[搭配使用 SSH 和從 Windows 的 HDInsight 上的 Linux Hadoop](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md)。</span><span class="sxs-lookup"><span data-stu-id="af116-190">If you are using a Windows client toomake an SSH connection into hello cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span></span>
* <span data-ttu-id="af116-191">如果您使用 Linux 用戶端 toomake SSH 連線到 hello 叢集中，請參閱[搭配使用 SSH 和 Linux 的 HDInsight 上的 Linux Hadoop](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="af116-191">If you are using a Linux client toomake an SSH connection into hello cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="af116-192">進行 hello 連線之後，請使用下列 HDFS 檔案系統命令 hello 列出資料湖存放區中的 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="af116-192">After you've made hello connection, list hello files in Data Lake Store by using hello following HDFS file system command.</span></span>

    hdfs dfs -ls adl:///

<span data-ttu-id="af116-193">您也可以使用 hello`hdfs dfs -put`命令 tooupload 某些檔案 tooData 湖存放區，然後使用`hdfs dfs -ls`tooverify 是否 hello 檔案已成功上傳。</span><span class="sxs-lookup"><span data-stu-id="af116-193">You can also use hello `hdfs dfs -put` command tooupload some files tooData Lake Store, and then use `hdfs dfs -ls` tooverify whether hello files were successfully uploaded.</span></span>

## <a name="see-also"></a><span data-ttu-id="af116-194">另請參閱</span><span class="sxs-lookup"><span data-stu-id="af116-194">See also</span></span>
* [<span data-ttu-id="af116-195">Azure 入口網站： 建立 HDInsight 叢集 toouse 資料湖存放區</span><span class="sxs-lookup"><span data-stu-id="af116-195">Azure portal: Create an HDInsight cluster toouse Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)

[makecert]: https://msdn.microsoft.com/library/windows/desktop/ff548309(v=vs.85).aspx
[pvk2pfx]: https://msdn.microsoft.com/library/windows/desktop/ff550672(v=vs.85).aspx
