---
<span data-ttu-id="ad247-101">標題： aaa"PowerShell： 為附加元件的存放裝置的資料湖存放區與 Azure HDInsight 叢集 |Microsoft 文件 」 服務： 資料湖存放，hdinsight documentationcenter: ' 作者： nitinme 管理員： jhubbard 編輯器： cgronlun</span><span class="sxs-lookup"><span data-stu-id="ad247-101">title: aaa"PowerShell: Azure HDInsight cluster with Data Lake Store as add-on storage | Microsoft Docs" services: data-lake-store,hdinsight documentationcenter: '' author: nitinme manager: jhubbard editor: cgronlun</span></span>

<span data-ttu-id="ad247-102">ms.assetid: 164ada5a-222e-4be2-bd32-e51dbe993bc0 ms.service： 資料湖存放區 ms.devlang: na ms.topic： 文章 ms.tgt_pltfrm: na ms.workload： 巨量資料 ms.date: 06/08/2017 ms.author: nitinme</span><span class="sxs-lookup"><span data-stu-id="ad247-102">ms.assetid: 164ada5a-222e-4be2-bd32-e51dbe993bc0 ms.service: data-lake-store ms.devlang: na ms.topic: article ms.tgt_pltfrm: na ms.workload: big-data ms.date: 06/08/2017 ms.author: nitinme</span></span>

---
# <a name="use-azure-powershell-toocreate-an-hdinsight-cluster-with-data-lake-store-as-additional-storage"></a><span data-ttu-id="ad247-103">Data Lake Store 的 HDInsight 叢集的 Azure PowerShell toocreate 使用 （做為額外的存放裝置）</span><span class="sxs-lookup"><span data-stu-id="ad247-103">Use Azure PowerShell toocreate an HDInsight cluster with Data Lake Store (as additional storage)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ad247-104">使用入口網站</span><span class="sxs-lookup"><span data-stu-id="ad247-104">Using Portal</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
> * [<span data-ttu-id="ad247-105">使用 PowerShell (針對預設儲存體)</span><span class="sxs-lookup"><span data-stu-id="ad247-105">Using PowerShell (for default storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
> * [<span data-ttu-id="ad247-106">使用 PowerShell (針對額外儲存體)</span><span class="sxs-lookup"><span data-stu-id="ad247-106">Using PowerShell (for additional storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell.md)
> * [<span data-ttu-id="ad247-107">使用 Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ad247-107">Using Resource Manager</span></span>](data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)
>
>

<span data-ttu-id="ad247-108">了解如何 toouse Azure PowerShell tooconfigure 在 HDInsight 叢集與 Azure 資料湖存放區**做為額外的儲存體**。</span><span class="sxs-lookup"><span data-stu-id="ad247-108">Learn how toouse Azure PowerShell tooconfigure an HDInsight cluster with Azure Data Lake Store, **as additional storage**.</span></span> <span data-ttu-id="ad247-109">如需有關如何 toocreate 在 HDInsight 叢集做為預設儲存體的 Azure Data Lake Store 的指示，請參閱[建立為預設的存放裝置的 Data Lake Store 的 HDInsight 叢集](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)。</span><span class="sxs-lookup"><span data-stu-id="ad247-109">For instructions on how toocreate an HDInsight cluster with Azure Data Lake Store as default storage, see [Create an HDInsight cluster with Data Lake Store as default storage](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md).</span></span>

> [!NOTE]
> <span data-ttu-id="ad247-110">如果您正在 toouse Azure Data Lake Store 為 HDInsight 叢集的其他存放裝置中，我們強烈建議您採用這種這篇文章中所述，建立 hello 叢集時。</span><span class="sxs-lookup"><span data-stu-id="ad247-110">If you are going toouse Azure Data Lake Store as additional storage for HDInsight cluster, we strongly recommend that you do this while you create hello cluster as described in this article.</span></span> <span data-ttu-id="ad247-111">將 Azure Data Lake Store 新增額外的儲存體 tooan 為現有 HDInsight 叢集是複雜的程序和 tooerrors 容易出錯。</span><span class="sxs-lookup"><span data-stu-id="ad247-111">Adding Azure Data Lake Store as additional storage tooan existing HDInsight cluster is a complicated process and prone tooerrors.</span></span>
>

<span data-ttu-id="ad247-112">Data Lake Store 對於支援的叢集類型，是做為預設儲存體或額外儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="ad247-112">For supported cluster types, Data Lake Store can be used as a default storage or additional storage account.</span></span> <span data-ttu-id="ad247-113">資料湖存放區是作為額外的存放裝置，hello hello 叢集的預設儲存體帳戶仍會 Azure 儲存體 Blob (WASB) 和受 hello 叢集相關的檔案 （例如記錄檔等） 仍會寫入 toohello 預設儲存體，hello 資料時，您想 tooprocess 可以儲存在 Data Lake Store 帳戶。</span><span class="sxs-lookup"><span data-stu-id="ad247-113">When Data Lake Store is used as additional storage, hello default storage account for hello clusters will still be Azure Storage Blobs (WASB) and hello cluster-related files (such as logs, etc.) are still written toohello default storage, while hello data that you want tooprocess can be stored in a Data Lake Store account.</span></span> <span data-ttu-id="ad247-114">使用資料湖存放區做為額外的儲存體帳戶不會影響效能或 hello 能力 tooread/寫入 toohello 叢集中存放裝置 hello。</span><span class="sxs-lookup"><span data-stu-id="ad247-114">Using Data Lake Store as an additional storage account does not impact performance or hello ability tooread/write toohello storage from hello cluster.</span></span>

## <a name="using-data-lake-store-for-hdinsight-cluster-storage"></a><span data-ttu-id="ad247-115">針對 HDInsight 叢集儲存體使用 Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="ad247-115">Using Data Lake Store for HDInsight cluster storage</span></span>

<span data-ttu-id="ad247-116">以下是使用 HDInsight 搭配 Data Lake Store 的一些重要考量：</span><span class="sxs-lookup"><span data-stu-id="ad247-116">Here are some important considerations for using HDInsight with Data Lake Store:</span></span>

* <span data-ttu-id="ad247-117">選項 toocreate HDInsight 叢集的存取是適用於 HDInsight 版本 3.2、 3.4、 3.5 和 3.6 tooData 湖存放區做為額外的存放裝置。</span><span class="sxs-lookup"><span data-stu-id="ad247-117">Option toocreate HDInsight clusters with access tooData Lake Store as additional storage is available for HDInsight versions 3.2, 3.4, 3.5, and 3.6.</span></span>

<span data-ttu-id="ad247-118">設定 HDInsight toowork 與使用 PowerShell 的資料湖存放區會包含 hello 下列步驟：</span><span class="sxs-lookup"><span data-stu-id="ad247-118">Configuring HDInsight toowork with Data Lake Store using PowerShell involves hello following steps:</span></span>

* <span data-ttu-id="ad247-119">建立 Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="ad247-119">Create an Azure Data Lake Store</span></span>
* <span data-ttu-id="ad247-120">設定以角色為基礎的驗證存取 tooData 湖存放區</span><span class="sxs-lookup"><span data-stu-id="ad247-120">Set up authentication for role-based access tooData Lake Store</span></span>
* <span data-ttu-id="ad247-121">建立與驗證 tooData Lake Store 的 HDInsight 叢集</span><span class="sxs-lookup"><span data-stu-id="ad247-121">Create HDInsight cluster with authentication tooData Lake Store</span></span>
* <span data-ttu-id="ad247-122">Hello 叢集上執行測試工作</span><span class="sxs-lookup"><span data-stu-id="ad247-122">Run a test job on hello cluster</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ad247-123">必要條件</span><span class="sxs-lookup"><span data-stu-id="ad247-123">Prerequisites</span></span>
<span data-ttu-id="ad247-124">開始本教學課程之前，您必須擁有 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="ad247-124">Before you begin this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="ad247-125">**Azure 訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="ad247-125">**An Azure subscription**.</span></span> <span data-ttu-id="ad247-126">請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="ad247-126">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="ad247-127">**Azure PowerShell 1.0 或更新版本**。</span><span class="sxs-lookup"><span data-stu-id="ad247-127">**Azure PowerShell 1.0 or greater**.</span></span> <span data-ttu-id="ad247-128">請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="ad247-128">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="ad247-129">**Windows SDK**。</span><span class="sxs-lookup"><span data-stu-id="ad247-129">**Windows SDK**.</span></span> <span data-ttu-id="ad247-130">您可以從[這裡](https://dev.windows.com/en-us/downloads)安裝它。</span><span class="sxs-lookup"><span data-stu-id="ad247-130">You can install it from [here](https://dev.windows.com/en-us/downloads).</span></span> <span data-ttu-id="ad247-131">您使用此 toocreate 安全性憑證。</span><span class="sxs-lookup"><span data-stu-id="ad247-131">You use this toocreate a security certificate.</span></span>
* <span data-ttu-id="ad247-132">**Azure Active Directory 服務主體**。</span><span class="sxs-lookup"><span data-stu-id="ad247-132">**Azure Active Directory Service Principal**.</span></span> <span data-ttu-id="ad247-133">本教學課程步驟提供如何指示 toocreate Azure AD 中的服務主體。</span><span class="sxs-lookup"><span data-stu-id="ad247-133">Steps in this tutorial provide instructions on how toocreate a service principal in Azure AD.</span></span> <span data-ttu-id="ad247-134">不過，您必須是 Azure AD 管理員 toobe 無法 toocreate 服務主體。</span><span class="sxs-lookup"><span data-stu-id="ad247-134">However, you must be an Azure AD administrator toobe able toocreate a service principal.</span></span> <span data-ttu-id="ad247-135">如果您是 Azure AD 管理員，則可以略過這項必要條件，並繼續進行 hello 教學課程。</span><span class="sxs-lookup"><span data-stu-id="ad247-135">If you are an Azure AD administrator, you can skip this prerequisite and proceed with hello tutorial.</span></span>

    <span data-ttu-id="ad247-136">**如果您不是 Azure AD 管理員**，就能 tooperform hello 步驟需要的 toocreate 服務主體。</span><span class="sxs-lookup"><span data-stu-id="ad247-136">**If you are not an Azure AD administrator**, you will not be able tooperform hello steps required toocreate a service principal.</span></span> <span data-ttu-id="ad247-137">在這樣的情況下，您的 Azure AD 系統管理員必須先建立服務主體，您才能建立搭配 Data Lake Store 的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="ad247-137">In such a case, your Azure AD administrator must first create a service principal before you can create an HDInsight cluster with Data Lake Store.</span></span> <span data-ttu-id="ad247-138">此外，hello 服務主體必須建立使用的認證，依照[建立服務主體與憑證](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority)。</span><span class="sxs-lookup"><span data-stu-id="ad247-138">Also, hello service principal must be created using a certificate, as described at [Create a service principal with certificate](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).</span></span>

## <a name="create-an-azure-data-lake-store"></a><span data-ttu-id="ad247-139">建立 Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="ad247-139">Create an Azure Data Lake Store</span></span>
<span data-ttu-id="ad247-140">請遵循這些步驟 toocreate 資料湖存放區。</span><span class="sxs-lookup"><span data-stu-id="ad247-140">Follow these steps toocreate a Data Lake Store.</span></span>

1. <span data-ttu-id="ad247-141">從您的桌面，開啟新的 Azure PowerShell 視窗，並輸入下列程式碼片段的 hello。</span><span class="sxs-lookup"><span data-stu-id="ad247-141">From your desktop, open a new Azure PowerShell window, and enter hello following snippet.</span></span> <span data-ttu-id="ad247-142">當提示的 toolog 中，請確定您登入做為其中一個 hello 訂用帳戶管理員/擁有者：</span><span class="sxs-lookup"><span data-stu-id="ad247-142">When prompted toolog in, make sure you log in as one of hello subscription administrator/owner:</span></span>

        # Log in tooyour Azure account
        Login-AzureRmAccount

        # List all hello subscriptions associated tooyour account
        Get-AzureRmSubscription

        # Select a subscription
        Set-AzureRmContext -SubscriptionId <subscription ID>

        # Register for Data Lake Store
        Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.DataLakeStore"

   > [!NOTE]
   > <span data-ttu-id="ad247-143">如果您收到類似的錯誤太`Register-AzureRmResourceProvider : InvalidResourceNamespace: hello resource namespace 'Microsoft.DataLakeStore' is invalid`當註冊 hello 資料湖存放區資源提供者，您就可以確認您的訂用帳戶不是在 Azure Data Lake Store 的允許清單。</span><span class="sxs-lookup"><span data-stu-id="ad247-143">If you receive an error similar too`Register-AzureRmResourceProvider : InvalidResourceNamespace: hello resource namespace 'Microsoft.DataLakeStore' is invalid` when registering hello Data Lake Store resource provider, it is possible that your subscription is not whitelisted for Azure Data Lake Store.</span></span> <span data-ttu-id="ad247-144">請遵循這些 [指示](data-lake-store-get-started-portal.md)，確保您會啟用 Azure 訂用帳戶來使用 Data Lake Store 公開預覽版。</span><span class="sxs-lookup"><span data-stu-id="ad247-144">Make sure you enable your Azure subscription for Data Lake Store public preview by following these [instructions](data-lake-store-get-started-portal.md).</span></span>
   >
   >
2. <span data-ttu-id="ad247-145">Azure Data Lake Store 帳戶與 Azure 資源群組相關聯。</span><span class="sxs-lookup"><span data-stu-id="ad247-145">An Azure Data Lake Store account is associated with an Azure Resource Group.</span></span> <span data-ttu-id="ad247-146">從建立 Azure 資源群組開始。</span><span class="sxs-lookup"><span data-stu-id="ad247-146">Start by creating an Azure Resource Group.</span></span>

        $resourceGroupName = "<your new resource group name>"
        New-AzureRmResourceGroup -Name $resourceGroupName -Location "East US 2"

    <span data-ttu-id="ad247-147">您應該會看到如下的輸出：</span><span class="sxs-lookup"><span data-stu-id="ad247-147">You should see an output like this:</span></span>

        ResourceGroupName : hdiadlgrp
        Location          : eastus2
        ProvisioningState : Succeeded
        Tags              :
        ResourceId        : /subscriptions/<subscription-id>/resourceGroups/hdiadlgrp

3. <span data-ttu-id="ad247-148">建立 Azure Data Lake Store 帳戶。</span><span class="sxs-lookup"><span data-stu-id="ad247-148">Create an Azure Data Lake Store account.</span></span> <span data-ttu-id="ad247-149">您指定的名稱只能包含小寫字母和數字的 hello 帳戶。</span><span class="sxs-lookup"><span data-stu-id="ad247-149">hello account name you specify must only contain lowercase letters and numbers.</span></span>

        $dataLakeStoreName = "<your new Data Lake Store name>"
        New-AzureRmDataLakeStoreAccount -ResourceGroupName $resourceGroupName -Name $dataLakeStoreName -Location "East US 2"

    <span data-ttu-id="ad247-150">您應該會看到類似 hello 下列輸出：</span><span class="sxs-lookup"><span data-stu-id="ad247-150">You should see an output like hello following:</span></span>

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

5. <span data-ttu-id="ad247-151">上傳某些範例資料 tooAzure Data Lake。</span><span class="sxs-lookup"><span data-stu-id="ad247-151">Upload some sample data tooAzure Data Lake.</span></span> <span data-ttu-id="ad247-152">我們會使用它在 hello 資料是從 HDInsight 叢集，您可存取此文件 tooverify 稍後。</span><span class="sxs-lookup"><span data-stu-id="ad247-152">We'll use this later in this article tooverify that hello data is accessible from an HDInsight cluster.</span></span> <span data-ttu-id="ad247-153">如果您要尋找的一些範例資料 tooupload，您可以取得 hello**政策救護車資料**資料夾從 hello [Azure 資料湖 Git 儲存機制](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData)。</span><span class="sxs-lookup"><span data-stu-id="ad247-153">If you are looking for some sample data tooupload, you can get hello **Ambulance Data** folder from hello [Azure Data Lake Git Repository](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span></span>

        $myrootdir = "/"
        Import-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path "C:\<path toodata>\vehicle1_09142014.csv" -Destination $myrootdir\vehicle1_09142014.csv


## <a name="set-up-authentication-for-role-based-access-toodata-lake-store"></a><span data-ttu-id="ad247-154">設定以角色為基礎的驗證存取 tooData 湖存放區</span><span class="sxs-lookup"><span data-stu-id="ad247-154">Set up authentication for role-based access tooData Lake Store</span></span>
<span data-ttu-id="ad247-155">每一個 Azure 訂用帳戶都與 Azure Active Directory 相關聯。</span><span class="sxs-lookup"><span data-stu-id="ad247-155">Every Azure subscription is associated with an Azure Active Directory.</span></span> <span data-ttu-id="ad247-156">使用者和服務存取 hello 訂用帳戶使用 hello Azure 傳統入口網站或 Azure 資源管理員 API 的資源，必須先通過驗證 Azure Active Directory。</span><span class="sxs-lookup"><span data-stu-id="ad247-156">Users and services that access resources of hello subscription using hello Azure Classic Portal or Azure Resource Manager API must first authenticate with that Azure Active Directory.</span></span> <span data-ttu-id="ad247-157">已授與存取 tooAzure 訂閱和服務由將其指派 hello Azure 資源上的適當角色。</span><span class="sxs-lookup"><span data-stu-id="ad247-157">Access is granted tooAzure subscriptions and services by assigning them hello appropriate role on an Azure resource.</span></span>  <span data-ttu-id="ad247-158">為服務，服務主體識別 hello Azure Active Directory (AAD) 中的 hello 服務。</span><span class="sxs-lookup"><span data-stu-id="ad247-158">For services, a service principal identifies hello service in hello Azure Active Directory (AAD).</span></span> <span data-ttu-id="ad247-159">本節說明 toogrant 應用程式的服務方式，例如 HDInsight，存取 tooan Azure 資源 (您先前建立的 Azure Data Lake Store 帳戶 hello) 藉由建立 hello 應用程式的服務主體，並指派透過 Azure 角色 toothatPowerShell。</span><span class="sxs-lookup"><span data-stu-id="ad247-159">This section illustrates how toogrant an application service, like HDInsight, access tooan Azure resource (hello Azure Data Lake Store account you created earlier) by creating a service principal for hello application and assigning roles toothat via Azure PowerShell.</span></span>

<span data-ttu-id="ad247-160">設定 Active Directory 驗證的 Azure 資料湖 tooset，您必須執行下列工作的 hello。</span><span class="sxs-lookup"><span data-stu-id="ad247-160">tooset up Active Directory authentication for Azure Data Lake, you must perform hello following tasks.</span></span>

* <span data-ttu-id="ad247-161">建立自我簽署憑證</span><span class="sxs-lookup"><span data-stu-id="ad247-161">Create a self-signed certificate</span></span>
* <span data-ttu-id="ad247-162">在 Azure Active Directory 和服務主體中建立應用程式</span><span class="sxs-lookup"><span data-stu-id="ad247-162">Create an application in Azure Active Directory and a Service Principal</span></span>

### <a name="create-a-self-signed-certificate"></a><span data-ttu-id="ad247-163">建立自我簽署憑證</span><span class="sxs-lookup"><span data-stu-id="ad247-163">Create a self-signed certificate</span></span>
<span data-ttu-id="ad247-164">請確定您有[Windows SDK](https://dev.windows.com/en-us/downloads) hello 進行這一節的步驟之前安裝。</span><span class="sxs-lookup"><span data-stu-id="ad247-164">Make sure you have [Windows SDK](https://dev.windows.com/en-us/downloads) installed before proceeding with hello steps in this section.</span></span> <span data-ttu-id="ad247-165">您必須也建立目錄，例如**C:\mycertdir**、 建立 hello 憑證的位置。</span><span class="sxs-lookup"><span data-stu-id="ad247-165">You must have also created a directory, such as **C:\mycertdir**, where hello certificate will be created.</span></span>

1. <span data-ttu-id="ad247-166">從 hello PowerShell 視窗中，瀏覽 toohello 安裝 Windows SDK 的位置 (通常`C:\Program Files (x86)\Windows Kits\10\bin\x86`並用 hello [MakeCert] [ makecert]公用程式 toocreate 自我簽署憑證和私用的索引鍵。</span><span class="sxs-lookup"><span data-stu-id="ad247-166">From hello PowerShell window, navigate toohello location where you installed Windows SDK (typically, `C:\Program Files (x86)\Windows Kits\10\bin\x86` and use hello [MakeCert][makecert] utility toocreate a self-signed certificate and a private key.</span></span> <span data-ttu-id="ad247-167">使用下列命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="ad247-167">Use hello following commands.</span></span>

        $certificateFileDir = "<my certificate directory>"
        cd $certificateFileDir

        makecert -sv mykey.pvk -n "cn=HDI-ADL-SP" CertFile.cer -r -len 2048

    <span data-ttu-id="ad247-168">系統會提示的 tooenter hello 私密金鑰密碼。</span><span class="sxs-lookup"><span data-stu-id="ad247-168">You will be prompted tooenter hello private key password.</span></span> <span data-ttu-id="ad247-169">Hello 命令執行成功，您應該會看到之後**CertFile.cer**和**mykey.pvk**您指定的 hello 憑證目錄中。</span><span class="sxs-lookup"><span data-stu-id="ad247-169">After hello command successfully executes, you should see a **CertFile.cer** and **mykey.pvk** in hello certificate directory you specified.</span></span>
2. <span data-ttu-id="ad247-170">使用 hello [Pvk2Pfx] [ pvk2pfx]公用程式 tooconvert hello.pvk 和.cer 檔案 MakeCert 建立的 tooa.pfx 檔案。</span><span class="sxs-lookup"><span data-stu-id="ad247-170">Use hello [Pvk2Pfx][pvk2pfx] utility tooconvert hello .pvk and .cer files that MakeCert created tooa .pfx file.</span></span> <span data-ttu-id="ad247-171">執行下列命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="ad247-171">Run hello following command.</span></span>

        pvk2pfx -pvk mykey.pvk -spc CertFile.cer -pfx CertFile.pfx -po <password>

    <span data-ttu-id="ad247-172">出現提示時輸入 hello 私密金鑰密碼您稍早指定。</span><span class="sxs-lookup"><span data-stu-id="ad247-172">When prompted enter hello private key password you specified earlier.</span></span> <span data-ttu-id="ad247-173">hello 指定 hello 值**po**參數是 hello 與 hello.pfx 檔相關聯的密碼。</span><span class="sxs-lookup"><span data-stu-id="ad247-173">hello value you specify for hello **-po** parameter is hello password that is associated with hello .pfx file.</span></span> <span data-ttu-id="ad247-174">Hello 命令成功完成後，您也應該會看到 CertFile.pfx 您指定的 hello 憑證目錄中。</span><span class="sxs-lookup"><span data-stu-id="ad247-174">After hello command successfully completes, you should also see a CertFile.pfx in hello certificate directory you specified.</span></span>

### <a name="create-an-azure-active-directory-and-a-service-principal"></a><span data-ttu-id="ad247-175">建立 Azure Active Directory 和服務主體</span><span class="sxs-lookup"><span data-stu-id="ad247-175">Create an Azure Active Directory and a service principal</span></span>
<span data-ttu-id="ad247-176">在本節中，您的 Azure Active Directory 應用程式執行 hello 步驟 toocreate 服務主體、 指派角色 toohello 服務主體，以及 hello 服務主體以驗證所提供的憑證。</span><span class="sxs-lookup"><span data-stu-id="ad247-176">In this section, you perform hello steps toocreate a service principal for an Azure Active Directory application, assign a role toohello service principal, and authenticate as hello service principal by providing a certificate.</span></span> <span data-ttu-id="ad247-177">Azure Active Directory 中執行下列命令 toocreate hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ad247-177">Run hello following commands toocreate an application in Azure Active Directory.</span></span>

1. <span data-ttu-id="ad247-178">貼上下列指令程式 hello PowerShell 主控台視窗中的 hello。</span><span class="sxs-lookup"><span data-stu-id="ad247-178">Paste hello following cmdlets in hello PowerShell console window.</span></span> <span data-ttu-id="ad247-179">確定您指定 hello 的 hello 值**-DisplayName**屬性是唯一的。</span><span class="sxs-lookup"><span data-stu-id="ad247-179">Make sure hello value you specify for hello **-DisplayName** property is unique.</span></span> <span data-ttu-id="ad247-180">此外，hello 值**-首頁**和**-IdentiferUris**預留位置值，並不會驗證。</span><span class="sxs-lookup"><span data-stu-id="ad247-180">Also, hello values for **-HomePage** and **-IdentiferUris** are placeholder values and are not verified.</span></span>

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
2. <span data-ttu-id="ad247-181">建立服務主體使用 hello 應用程式識別碼。</span><span class="sxs-lookup"><span data-stu-id="ad247-181">Create a service principal using hello application ID.</span></span>

        $servicePrincipal = New-AzureRmADServicePrincipal -ApplicationId $applicationId

        $objectId = $servicePrincipal.Id
3. <span data-ttu-id="ad247-182">授與 hello 服務主體存取 toohello Data Lake Store 資料夾和您將從 hello HDInsight 叢集存取的 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="ad247-182">Grant hello service principal access toohello Data Lake Store folder and hello file that you will access from hello HDInsight cluster.</span></span> <span data-ttu-id="ad247-183">hello 以下程式碼片段提供存取 toohello 根目錄的 hello Data Lake Store 帳戶 （您複製 hello 範例資料檔），並 hello 檔案本身。</span><span class="sxs-lookup"><span data-stu-id="ad247-183">hello snippet below provides access toohello root of hello Data Lake Store account (where you copied hello sample data file), and hello file itself.</span></span>

        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path / -AceType User -Id $objectId -Permissions All
        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path /vehicle1_09142014.csv -AceType User -Id $objectId -Permissions All

## <a name="create-an-hdinsight-linux-cluster-with-data-lake-store-as-additional-storage"></a><span data-ttu-id="ad247-184">建立 HDInsight Linux 叢集搭配 Data Lake Store 做為額外儲存體</span><span class="sxs-lookup"><span data-stu-id="ad247-184">Create an HDInsight Linux cluster with Data Lake Store as additional storage</span></span>

<span data-ttu-id="ad247-185">在本節中，我們會建立一個 HDInsight Hadoop Linux 叢集搭配 Data Lake Store 做為額外儲存體。</span><span class="sxs-lookup"><span data-stu-id="ad247-185">In this section, we create an HDInsight Hadoop Linux cluster with Data Lake Store as additional storage.</span></span> <span data-ttu-id="ad247-186">此版本中，hello HDInsight 叢集與 hello 資料湖存放區必須在 hello 相同的位置。</span><span class="sxs-lookup"><span data-stu-id="ad247-186">For this release, hello HDInsight cluster and hello Data Lake Store must be in hello same location.</span></span>

1. <span data-ttu-id="ad247-187">開始擷取 hello 訂用帳戶的租用戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="ad247-187">Start with retrieving hello subscription tenant ID.</span></span> <span data-ttu-id="ad247-188">稍後您將會需要此資訊。</span><span class="sxs-lookup"><span data-stu-id="ad247-188">You will need that later.</span></span>

        $tenantID = (Get-AzureRmContext).Tenant.TenantId
2. <span data-ttu-id="ad247-189">此版本中，Hadoop 叢集中，資料湖存放區可以只當做額外的存放裝置 hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="ad247-189">For this release, for a Hadoop cluster, Data Lake Store can only be used as an additional storage for hello cluster.</span></span> <span data-ttu-id="ad247-190">hello 預設儲存體仍會 hello Azure 儲存體 blob (WASB)。</span><span class="sxs-lookup"><span data-stu-id="ad247-190">hello default storage will still be hello Azure storage blobs (WASB).</span></span> <span data-ttu-id="ad247-191">因此，我們將先建立 hello hello 叢集所需的儲存體帳戶和儲存體容器。</span><span class="sxs-lookup"><span data-stu-id="ad247-191">So, we'll first create hello storage account and storage containers required for hello cluster.</span></span>

        # Create an Azure storage account
        $location = "East US 2"
        $storageAccountName = "<StorageAcccountName>"   # Provide a Storage account name

        New-AzureRmStorageAccount -ResourceGroupName $resourceGroupName -StorageAccountName $storageAccountName -Location $location -Type Standard_GRS

        # Create an Azure Blob Storage container
        $containerName = "<ContainerName>"              # Provide a container name
        $storageAccountKey = (Get-AzureRmStorageAccountKey -Name $storageAccountName -ResourceGroupName $resourceGroupName)[0].Value
        $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey
        New-AzureStorageContainer -Name $containerName -Context $destContext
3. <span data-ttu-id="ad247-192">建立 hello HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="ad247-192">Create hello HDInsight cluster.</span></span> <span data-ttu-id="ad247-193">使用下列 cmdlet 的 hello。</span><span class="sxs-lookup"><span data-stu-id="ad247-193">Use hello following cmdlets.</span></span>

        # Set these variables
        $clusterName = $containerName                   # As a best practice, have hello same name for hello cluster and container
        $clusterNodes = <ClusterSizeInNodes>            # hello number of nodes in hello HDInsight cluster
        $httpCredentials = Get-Credential
        $sshCredentials = Get-Credential

        New-AzureRmHDInsightCluster -ClusterName $clusterName -ResourceGroupName $resourceGroupName -HttpCredential $httpCredentials -Location $location -DefaultStorageAccountName "$storageAccountName.blob.core.windows.net" -DefaultStorageAccountKey $storageAccountKey -DefaultStorageContainer $containerName  -ClusterSizeInNodes $clusterNodes -ClusterType Hadoop -Version "3.4" -OSType Linux -SshCredential $sshCredentials -ObjectID $objectId -AadTenantId $tenantID -CertificateFilePath $certificateFilePath -CertificatePassword $password

    <span data-ttu-id="ad247-194">Hello cmdlet 順利完成之後，您應該會看到列出 hello 叢集詳細資料的輸出。</span><span class="sxs-lookup"><span data-stu-id="ad247-194">After hello cmdlet successfully completes, you should see an output listing hello cluster details.</span></span>


## <a name="run-test-jobs-on-hello-hdinsight-cluster-toouse-hello-data-lake-store"></a><span data-ttu-id="ad247-195">Hello HDInsight 叢集 toouse hello 資料湖存放區上執行測試工作</span><span class="sxs-lookup"><span data-stu-id="ad247-195">Run test jobs on hello HDInsight cluster toouse hello Data Lake Store</span></span>
<span data-ttu-id="ad247-196">您已設定的 HDInsight 叢集之後，您可以測試工作上執行 hello 叢集 tootest 該 hello HDInsight 叢集可以存取資料湖存放區。</span><span class="sxs-lookup"><span data-stu-id="ad247-196">After you have configured an HDInsight cluster, you can run test jobs on hello cluster tootest that hello HDInsight cluster can access Data Lake Store.</span></span> <span data-ttu-id="ad247-197">toodo 因此，我們會執行使用您上傳先前 tooyour Data Lake Store 的 hello 範例資料建立資料表的範例 Hive 工作。</span><span class="sxs-lookup"><span data-stu-id="ad247-197">toodo so, we will run a sample Hive job that creates a table using hello sample data that you uploaded earlier tooyour Data Lake Store.</span></span>

<span data-ttu-id="ad247-198">在本節中，您可以將 SSH 到 hello HDInsight Linux 叢集您建立及執行 hello 範例 Hive 查詢。</span><span class="sxs-lookup"><span data-stu-id="ad247-198">In this section you will SSH into hello HDInsight Linux cluster you created and run hello a sample Hive query.</span></span>

* <span data-ttu-id="ad247-199">如果您使用 Windows 用戶端 tooSSH 到 hello 叢集中，請參閱[搭配使用 SSH 和從 Windows 的 HDInsight 上的 Linux Hadoop](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md)。</span><span class="sxs-lookup"><span data-stu-id="ad247-199">If you are using a Windows client tooSSH into hello cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span></span>
* <span data-ttu-id="ad247-200">如果您使用 Linux 用戶端 tooSSH 到 hello 叢集中，請參閱[搭配使用 SSH 和 Linux 的 HDInsight 上的 Linux Hadoop](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md)</span><span class="sxs-lookup"><span data-stu-id="ad247-200">If you are using a Linux client tooSSH into hello cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md)</span></span>

1. <span data-ttu-id="ad247-201">一旦連接之後，請使用下列命令的 hello 啟動 hello Hive CLI:</span><span class="sxs-lookup"><span data-stu-id="ad247-201">Once connected, start hello Hive CLI by using hello following command:</span></span>

        hive
2. <span data-ttu-id="ad247-202">使用 hello CLI 中，輸入下列陳述式 toocreate 名為的新資料表的 hello**車輛**利用 hello 資料湖存放區中的 hello 範例資料：</span><span class="sxs-lookup"><span data-stu-id="ad247-202">Using hello CLI, enter hello following statements toocreate a new table named **vehicles** by using hello sample data in hello Data Lake Store:</span></span>

        DROP TABLE vehicles;
        CREATE EXTERNAL TABLE vehicles (str string) LOCATION 'adl://<mydatalakestore>.azuredatalakestore.net:443/';
        SELECT * FROM vehicles LIMIT 10;

    <span data-ttu-id="ad247-203">您應該會看到類似 toohello 下列輸出：</span><span class="sxs-lookup"><span data-stu-id="ad247-203">You should see an output similar toohello following:</span></span>

        1,1,2014-09-14 00:00:03,46.81006,-92.08174,51,S,1
        1,2,2014-09-14 00:00:06,46.81006,-92.08174,13,NE,1
        1,3,2014-09-14 00:00:09,46.81006,-92.08174,48,NE,1
        1,4,2014-09-14 00:00:12,46.81006,-92.08174,30,W,1
        1,5,2014-09-14 00:00:15,46.81006,-92.08174,47,S,1
        1,6,2014-09-14 00:00:18,46.81006,-92.08174,9,S,1
        1,7,2014-09-14 00:00:21,46.81006,-92.08174,53,N,1
        1,8,2014-09-14 00:00:24,46.81006,-92.08174,63,SW,1
        1,9,2014-09-14 00:00:27,46.81006,-92.08174,4,NE,1
        1,10,2014-09-14 00:00:30,46.81006,-92.08174,31,N,1

## <a name="access-data-lake-store-using-hdfs-commands"></a><span data-ttu-id="ad247-204">使用 HDFS 命令存取 Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="ad247-204">Access Data Lake Store using HDFS commands</span></span>
<span data-ttu-id="ad247-205">一旦您已設定 hello HDInsight 叢集 toouse 資料湖存放區，您可以使用 hello HDFS 殼層命令 tooaccess hello 存放區。</span><span class="sxs-lookup"><span data-stu-id="ad247-205">Once you have configured hello HDInsight cluster toouse Data Lake Store, you can use hello HDFS shell commands tooaccess hello store.</span></span>

<span data-ttu-id="ad247-206">在本節中，您可以將 SSH 到 hello HDInsight Linux 叢集您建立及執行 hello HDFS 命令。</span><span class="sxs-lookup"><span data-stu-id="ad247-206">In this section you will SSH into hello HDInsight Linux cluster you created and run hello HDFS commands.</span></span>

* <span data-ttu-id="ad247-207">如果您使用 Windows 用戶端 tooSSH 到 hello 叢集中，請參閱[搭配使用 SSH 和從 Windows 的 HDInsight 上的 Linux Hadoop](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md)。</span><span class="sxs-lookup"><span data-stu-id="ad247-207">If you are using a Windows client tooSSH into hello cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span></span>
* <span data-ttu-id="ad247-208">如果您使用 Linux 用戶端 tooSSH 到 hello 叢集中，請參閱[搭配使用 SSH 和 Linux 的 HDInsight 上的 Linux Hadoop](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md)</span><span class="sxs-lookup"><span data-stu-id="ad247-208">If you are using a Linux client tooSSH into hello cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md)</span></span>

<span data-ttu-id="ad247-209">一旦連接之後，請使用下列 HDFS 檔案系統命令 toolist hello 檔案 hello 資料湖存放區中的 hello。</span><span class="sxs-lookup"><span data-stu-id="ad247-209">Once connected, use hello following HDFS filesystem command toolist hello files in hello Data Lake Store.</span></span>

    hdfs dfs -ls adl://<Data Lake Store account name>.azuredatalakestore.net:443/

<span data-ttu-id="ad247-210">這應該會列出您上傳先前 toohello Data Lake Store 的 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="ad247-210">This should list hello file that you uploaded earlier toohello Data Lake Store.</span></span>

    15/09/17 21:41:15 INFO web.CaboWebHdfsFileSystem: Replacing original urlConnectionFactory with org.apache.hadoop.hdfs.web.URLConnectionFactory@21a728d6
    Found 1 items
    -rwxrwxrwx   0 NotSupportYet NotSupportYet     671388 2015-09-16 22:16 adl://mydatalakestore.azuredatalakestore.net:443/mynewfolder

<span data-ttu-id="ad247-211">您也可以使用 hello`hdfs dfs -put`命令 tooupload 某些檔案 toohello 資料湖存放區，然後再使用`hdfs dfs -ls`tooverify 是否 hello 檔案已成功上傳。</span><span class="sxs-lookup"><span data-stu-id="ad247-211">You can also use hello `hdfs dfs -put` command tooupload some files toohello Data Lake Store, and then use `hdfs dfs -ls` tooverify whether hello files were successfully uploaded.</span></span>

## <a name="see-also"></a><span data-ttu-id="ad247-212">另請參閱</span><span class="sxs-lookup"><span data-stu-id="ad247-212">See Also</span></span>
* [<span data-ttu-id="ad247-213">入口網站： 建立 HDInsight 叢集 toouse 資料湖存放區</span><span class="sxs-lookup"><span data-stu-id="ad247-213">Portal: Create an HDInsight cluster toouse Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)

[makecert]: https://msdn.microsoft.com/library/windows/desktop/ff548309(v=vs.85).aspx
[pvk2pfx]: https://msdn.microsoft.com/library/windows/desktop/ff550672(v=vs.85).aspx
