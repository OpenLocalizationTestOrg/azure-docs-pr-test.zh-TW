---
title: "aaaAzure 待用資料的儲存體服務加密 |Microsoft 文件"
description: "Hello Azure 儲存體服務加密功能 tooencrypt 您的 Azure Blob 儲存體上使用 hello 服務端儲存 hello 資料時，擷取 hello 資料時將其解密。"
services: storage
documentationcenter: .net
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: edabe3ee-688b-41e0-b34f-613ac9c3fdfd
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/09/2017
ms.author: robinsh
ms.openlocfilehash: 304f1c21200f86f2084ce98788b2fc7ca893d1f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-service-encryption-for-data-at-rest"></a><span data-ttu-id="54259-103">待用資料的 Azure 儲存體服務加密</span><span class="sxs-lookup"><span data-stu-id="54259-103">Azure Storage Service Encryption for Data at Rest</span></span>
<span data-ttu-id="54259-104">Azure 儲存體服務加密 (SSE) 中的靜止資料可協助您保護與防衛資料 toomeet 您組織的安全性和相容性的承諾。</span><span class="sxs-lookup"><span data-stu-id="54259-104">Azure Storage Service Encryption (SSE) for Data at Rest helps you protect and safeguard your data toomeet your organizational security and compliance commitments.</span></span> <span data-ttu-id="54259-105">利用此功能，Azure 儲存體，自動將加密您的資料之前 toopersisting toostorage，並解密先前 tooretrieval。</span><span class="sxs-lookup"><span data-stu-id="54259-105">With this feature, Azure Storage automatically encrypts your data prior toopersisting toostorage and decrypts prior tooretrieval.</span></span> <span data-ttu-id="54259-106">hello 加密、 解密和金鑰管理是完全透明 toousers。</span><span class="sxs-lookup"><span data-stu-id="54259-106">hello encryption, decryption, and key management are totally transparent toousers.</span></span>

<span data-ttu-id="54259-107">hello 下列各節提供詳細的指引如何 toouse hello 儲存體服務加密功能，以及 hello 支援案例和使用者經驗。</span><span class="sxs-lookup"><span data-stu-id="54259-107">hello following sections provide detailed guidance on how toouse hello Storage Service Encryption features as well as hello supported scenarios and user experiences.</span></span>

## <a name="overview"></a><span data-ttu-id="54259-108">概觀</span><span class="sxs-lookup"><span data-stu-id="54259-108">Overview</span></span>
<span data-ttu-id="54259-109">Azure 儲存體提供一組完整的安全性功能，同時讓開發人員 toobuild 安全的應用程式。</span><span class="sxs-lookup"><span data-stu-id="54259-109">Azure Storage provides a comprehensive set of security capabilities which together enable developers toobuild secure applications.</span></span> <span data-ttu-id="54259-110">您可以使用[用戶端加密](storage-client-side-encryption.md)、HTTPs 或 SMB 3.0，在應用程式和 Azure 之間進行傳輸時保護資料的安全。</span><span class="sxs-lookup"><span data-stu-id="54259-110">Data can be secured in transit between an application and Azure by using [Client-Side Encryption](storage-client-side-encryption.md), HTTPs, or SMB 3.0.</span></span> <span data-ttu-id="54259-111">儲存體服務加密可提供待用加密，並以完全透明的方式處理加密、解密和金鑰管理。</span><span class="sxs-lookup"><span data-stu-id="54259-111">Storage Service Encryption provides encryption at rest, handling encryption, decryption, and key management in a totally transparent fashion.</span></span> <span data-ttu-id="54259-112">所有的資料會使用 256 位元加密[AES 加密](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard)，hello 最強的區塊的其中一個這類編碼器使用。</span><span class="sxs-lookup"><span data-stu-id="54259-112">All data is encrypted using 256-bit [AES encryption](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard), one of hello strongest block ciphers available.</span></span>

<span data-ttu-id="54259-113">SSE 的運作方式寫入 tooAzure 存放裝置，並可用於 Azure Blob 儲存體和檔案儲存體加密 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="54259-113">SSE works by encrypting hello data when it is written tooAzure Storage, and can be used for Azure Blob Storage and File Storage.</span></span> <span data-ttu-id="54259-114">這也適用於下列 hello:</span><span class="sxs-lookup"><span data-stu-id="54259-114">It works for hello following:</span></span>

* <span data-ttu-id="54259-115">標準儲存體：Blob 和檔案儲存體的一般用途帳戶及 Blob 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="54259-115">Standard Storage: General purpose storage accounts for Blobs and File storage and Blob storage accounts</span></span>
* <span data-ttu-id="54259-116">進階儲存體</span><span class="sxs-lookup"><span data-stu-id="54259-116">Premium storage</span></span> 
* <span data-ttu-id="54259-117">所有備援層級 (LRS、ZRS、GRS、RA-GRS)</span><span class="sxs-lookup"><span data-stu-id="54259-117">All redundancy levels (LRS, ZRS, GRS, RA-GRS)</span></span>
* <span data-ttu-id="54259-118">Azure Resource Manager 儲存體帳戶 (但不是傳統帳戶)</span><span class="sxs-lookup"><span data-stu-id="54259-118">Azure Resource Manager storage accounts (but not classic)</span></span> 
* <span data-ttu-id="54259-119">所有區域。</span><span class="sxs-lookup"><span data-stu-id="54259-119">All regions.</span></span>

<span data-ttu-id="54259-120">toolearn 詳細資訊，請參閱 toohello 常見問題集。</span><span class="sxs-lookup"><span data-stu-id="54259-120">toolearn more, please refer toohello FAQ.</span></span>

<span data-ttu-id="54259-121">tooenable 或停用儲存體服務加密儲存體帳戶，登入到 hello [Azure 入口網站](https://portal.azure.com)並選取儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="54259-121">tooenable or disable Storage Service Encryption for a storage account, log into hello [Azure portal](https://portal.azure.com) and select a storage account.</span></span> <span data-ttu-id="54259-122">Hello 設定 刀鋒視窗上尋找 hello Blob 服務 > 一節中這個螢幕擷取畫面所示並按一下 加密。</span><span class="sxs-lookup"><span data-stu-id="54259-122">On hello Settings blade, look for hello Blob Service section as shown in this screenshot and click Encryption.</span></span>

<span data-ttu-id="54259-123">![顯示 [加密] 選項的入口網站螢幕擷取畫面](./media/storage-service-encryption/image1.png)
</span><span class="sxs-lookup"><span data-stu-id="54259-123">![Portal Screenshot showing Encryption option](./media/storage-service-encryption/image1.png)
</span></span><br/><span data-ttu-id="54259-124">*圖 1：為 Blob 服務啟用 SSE (步驟 1)*</span><span class="sxs-lookup"><span data-stu-id="54259-124">*Figure 1: Enable SSE for Blob Service (Step1)*</span></span>

<span data-ttu-id="54259-125">![顯示 [加密] 選項的入口網站螢幕擷取畫面](./media/storage-service-encryption/image3.png)
</span><span class="sxs-lookup"><span data-stu-id="54259-125">![Portal Screenshot showing Encryption option](./media/storage-service-encryption/image3.png)
</span></span><br/><span data-ttu-id="54259-126">*圖 2：為檔案服務啟用 SSE (步驟 1)*</span><span class="sxs-lookup"><span data-stu-id="54259-126">*Figure 2: Enable SSE for File Service (Step1)*</span></span>

<span data-ttu-id="54259-127">按一下 hello 加密設定之後，您可以啟用或停用儲存體服務加密。</span><span class="sxs-lookup"><span data-stu-id="54259-127">After you click hello Encryption setting, you can enable or disable Storage Service Encryption.</span></span>

<span data-ttu-id="54259-128">![顯示 [加密] 屬性的入口網站螢幕擷取畫面](./media/storage-service-encryption/image2.png)
</span><span class="sxs-lookup"><span data-stu-id="54259-128">![Portal Screenshot showing Encryption properties](./media/storage-service-encryption/image2.png)
</span></span><br/><span data-ttu-id="54259-129">*圖 3：為 Blob 和檔案服務啟用 SSE (步驟 2)*</span><span class="sxs-lookup"><span data-stu-id="54259-129">*Figure 3: Enable SSE for Blob and File Service (Step2)*</span></span>

## <a name="encryption-scenarios"></a><span data-ttu-id="54259-130">加密案例</span><span class="sxs-lookup"><span data-stu-id="54259-130">Encryption Scenarios</span></span>
<span data-ttu-id="54259-131">可以在儲存體帳戶層級啟用儲存體服務加密。</span><span class="sxs-lookup"><span data-stu-id="54259-131">Storage Service Encryption can be enabled at a storage account level.</span></span> <span data-ttu-id="54259-132">啟用之後，客戶將會選擇哪些服務 tooencrypt。</span><span class="sxs-lookup"><span data-stu-id="54259-132">Once enabled, customers will choose which services tooencrypt.</span></span> <span data-ttu-id="54259-133">它支援下列客戶案例 hello:</span><span class="sxs-lookup"><span data-stu-id="54259-133">It supports hello following customer scenarios:</span></span>

* <span data-ttu-id="54259-134">加密 Resource Manager 帳戶中的「Blob 儲存體」和「檔案儲存體」。</span><span class="sxs-lookup"><span data-stu-id="54259-134">Encryption of Blob Storage and File Storage in Resource Manager accounts.</span></span>
* <span data-ttu-id="54259-135">加密的 Blob 和檔案服務在傳統的儲存體帳戶中一次移轉 tooResource 管理員儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="54259-135">Encryption of Blob and File Service in classic storage accounts once migrated tooResource Manager storage accounts.</span></span>

<span data-ttu-id="54259-136">SSE 具有下列限制的 hello:</span><span class="sxs-lookup"><span data-stu-id="54259-136">SSE has hello following limitations:</span></span>

* <span data-ttu-id="54259-137">不支援傳統儲存體帳戶的加密。</span><span class="sxs-lookup"><span data-stu-id="54259-137">Encryption of classic storage accounts is not supported.</span></span>
* <span data-ttu-id="54259-138">啟用 hello 加密之後，現有的資料-SSE 只加密新建立的資料。</span><span class="sxs-lookup"><span data-stu-id="54259-138">Existing Data - SSE only encrypts newly created data after hello encryption is enabled.</span></span> <span data-ttu-id="54259-139">如果例如建立新的資源管理員儲存體帳戶，但不啟用加密，而且您上傳 blob 或封存的 Vhd toothat 儲存體帳戶，然後再開啟 SSE，除非它們可以重新撰寫或複製不會加密這些 blob。</span><span class="sxs-lookup"><span data-stu-id="54259-139">If for example you create a new Resource Manager storage account but don't turn on encryption, and then you upload blobs or archived VHDs toothat storage account and then turn on SSE, those blobs will not be encrypted unless they are rewritten or copied.</span></span>
* <span data-ttu-id="54259-140">Marketplace 支援-啟用從加密的 Vm 建立 hello Marketplace 使用 hello [Azure 入口網站](https://portal.azure.com)，PowerShell 及 Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="54259-140">Marketplace Support - Enable encryption of VMs created from hello Marketplace using hello [Azure portal](https://portal.azure.com), PowerShell, and Azure CLI.</span></span> <span data-ttu-id="54259-141">hello VHD 基底映像將保持未加密狀態。不過，hello VM 已調整大小之後，執行任何寫入將會加密。</span><span class="sxs-lookup"><span data-stu-id="54259-141">hello VHD base image will remain unencrypted; however, any writes done after hello VM has spun up will be encrypted.</span></span>
* <span data-ttu-id="54259-142">系統不會將資料表和佇列資料加密。</span><span class="sxs-lookup"><span data-stu-id="54259-142">Table and Queues data will not be encrypted.</span></span>

## <a name="getting-started"></a><span data-ttu-id="54259-143">開始使用</span><span class="sxs-lookup"><span data-stu-id="54259-143">Getting Started</span></span>
### <a name="step-1-create-a-new-storage-accountstorage-create-storage-accountmd"></a><span data-ttu-id="54259-144">步驟 1：[建立新的儲存體帳戶](storage-create-storage-account.md)。</span><span class="sxs-lookup"><span data-stu-id="54259-144">Step 1: [Create a new storage account](storage-create-storage-account.md).</span></span>
### <a name="step-2-enable-encryption"></a><span data-ttu-id="54259-145">步驟 2︰啟用加密。</span><span class="sxs-lookup"><span data-stu-id="54259-145">Step 2: Enable encryption.</span></span>
<span data-ttu-id="54259-146">您可以啟用加密使用 hello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="54259-146">You can enable encryption using hello [Azure portal](https://portal.azure.com).</span></span>

> [!NOTE]
> <span data-ttu-id="54259-147">如果您想 tooprogrammatically 啟用或停用的儲存體帳戶的儲存體服務加密 hello 時，您可以使用 hello [Azure 儲存體資源提供者 REST API](https://msdn.microsoft.com/library/azure/mt163683.aspx)，hello[儲存體資源提供者用戶端程式庫適用於.NET](https://msdn.microsoft.com/library/azure/mt131037.aspx)， [Azure PowerShell](/powershell/azureps-cmdlets-docs)，或使用 hello [Azure CLI](storage-azure-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="54259-147">If you want tooprogrammatically enable or disable hello Storage Service Encryption on a storage account, you can use hello [Azure Storage Resource Provider REST API](https://msdn.microsoft.com/library/azure/mt163683.aspx), hello [Storage Resource Provider Client Library for .NET](https://msdn.microsoft.com/library/azure/mt131037.aspx), [Azure PowerShell](/powershell/azureps-cmdlets-docs), or hello [Azure CLI](storage-azure-cli.md).</span></span>
> 
> 

### <a name="step-3-copy-data-toostorage-account"></a><span data-ttu-id="54259-148">步驟 3： 複製資料 toostorage 帳戶</span><span class="sxs-lookup"><span data-stu-id="54259-148">Step 3: Copy data toostorage account</span></span>
<span data-ttu-id="54259-149">如果您啟用 SSE hello Blob 服務時，將會加密寫入 toothat 儲存體帳戶的任何 blob。</span><span class="sxs-lookup"><span data-stu-id="54259-149">If you enable SSE for hello Blob service, any blobs written toothat storage account will be encrypted.</span></span> <span data-ttu-id="54259-150">已經位於該儲存體帳戶的任何 Blob 直到改寫後，才會加密。</span><span class="sxs-lookup"><span data-stu-id="54259-150">Any blobs already located in that storage account will not be encrypted until they are rewritten.</span></span> <span data-ttu-id="54259-151">您可以從一個儲存體帳戶 tooone 複製 hello 資料，使用 SSE 加密，或甚至啟用 SSE 和 hello blob 複製一個容器 tooanother toosure 先前的資料都會經過加密。</span><span class="sxs-lookup"><span data-stu-id="54259-151">You can copy hello data from one storage account tooone with SSE encrypted, or even enable SSE and copy hello blobs from one container tooanother toosure that previous data is encrypted.</span></span> <span data-ttu-id="54259-152">您可以使用任何下列工具 tooaccomplish hello 這。</span><span class="sxs-lookup"><span data-stu-id="54259-152">You can use any of hello following tools tooaccomplish this.</span></span> <span data-ttu-id="54259-153">這是儲存檔案以及 hello 相同的行為。</span><span class="sxs-lookup"><span data-stu-id="54259-153">This is hello same behavior for File Storage as well.</span></span>

#### <a name="using-azcopy"></a><span data-ttu-id="54259-154">使用 AzCopy</span><span class="sxs-lookup"><span data-stu-id="54259-154">Using AzCopy</span></span>
<span data-ttu-id="54259-155">AzCopy 是設計來複製資料 tooand 從 Microsoft Azure Blob、 檔案和資料表儲存體使用簡單的命令，以獲得最佳效能的 Windows 命令列公用程式。</span><span class="sxs-lookup"><span data-stu-id="54259-155">AzCopy is a Windows command-line utility designed for copying data tooand from Microsoft Azure Blob, File, and Table storage using simple commands with optimal performance.</span></span> <span data-ttu-id="54259-156">您的 blob 或檔案從一個儲存體帳戶 tooanother 具有 SSE 啟用，您可以使用這個 toocopy。</span><span class="sxs-lookup"><span data-stu-id="54259-156">You can use this toocopy your blobs or files from one storage account tooanother one that has SSE enabled.</span></span> 

<span data-ttu-id="54259-157">toolearn 詳細資訊，請瀏覽[hello AzCopy 命令列公用程式使用傳輸資料](storage-use-azcopy.md)。</span><span class="sxs-lookup"><span data-stu-id="54259-157">toolearn more, please visit [Transfer data with hello AzCopy Command-Line Utility](storage-use-azcopy.md).</span></span>

#### <a name="using-smb"></a><span data-ttu-id="54259-158">使用 SMB</span><span class="sxs-lookup"><span data-stu-id="54259-158">Using SMB</span></span>
<span data-ttu-id="54259-159">Azure 檔案儲存體提供使用標準 SMB 通訊協定 hello hello 雲端中的檔案共用。</span><span class="sxs-lookup"><span data-stu-id="54259-159">Azure File storage offers file shares in hello cloud using hello standard SMB protocol.</span></span> <span data-ttu-id="54259-160">您可以從內部部署或 Azure 中的用戶端掛接檔案共用。</span><span class="sxs-lookup"><span data-stu-id="54259-160">You can mount a file share from a client on premises or in Azure.</span></span> <span data-ttu-id="54259-161">掛接之後，如 Robocopy 工具可以使用的 toocopy 檔案經由 tooAzure 檔案共用。</span><span class="sxs-lookup"><span data-stu-id="54259-161">Once mounted, tools such as Robocopy can be used toocopy files over tooAzure File shares.</span></span> <span data-ttu-id="54259-162">如需詳細資訊，請參閱[如何 toomount Azure 檔案共用上 Windows](storage-file-how-to-use-files-windows.md)和[toomount Azure 檔案在 Linux 上的共用方式](storage-how-to-use-files-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="54259-162">For more information, see [how toomount Azure File Share on Windows](storage-file-how-to-use-files-windows.md) and [how toomount Azure File share on Linux](storage-how-to-use-files-linux.md).</span></span>


#### <a name="using-hello-storage-client-libraries"></a><span data-ttu-id="54259-163">使用 hello 儲存體用戶端程式庫</span><span class="sxs-lookup"><span data-stu-id="54259-163">Using hello Storage Client Libraries</span></span>
<span data-ttu-id="54259-164">您可以複製 blob 或檔案資料 tooand 從 blob 儲存體或使用我們一組豐富的儲存體用戶端程式庫，包括.NET、 c + +、 Java、 Android、 Node.js、 PHP、 Python 和 Ruby 的儲存體帳戶之間。</span><span class="sxs-lookup"><span data-stu-id="54259-164">You can copy blob or file data tooand from blob storage or between storage accounts using our rich set of Storage Client Libraries including .NET, C++, Java, Android, Node.js, PHP, Python, and Ruby.</span></span>

<span data-ttu-id="54259-165">toolearn 詳細資訊，請造訪我們[開始使用適用於.NET 的 Azure Blob 儲存體使用](storage-dotnet-how-to-use-blobs.md)。</span><span class="sxs-lookup"><span data-stu-id="54259-165">toolearn more, please visit our [Get started with Azure Blob storage using .NET](storage-dotnet-how-to-use-blobs.md).</span></span>

#### <a name="using-a-storage-explorer"></a><span data-ttu-id="54259-166">使用儲存體總管</span><span class="sxs-lookup"><span data-stu-id="54259-166">Using a Storage Explorer</span></span>
<span data-ttu-id="54259-167">您可以使用儲存體總管 toocreate 儲存體帳戶，請上傳和下載資料、 檢視內容的 blob，並瀏覽目錄。</span><span class="sxs-lookup"><span data-stu-id="54259-167">You can use a Storage explorer toocreate storage accounts, upload and download data, view contents of blobs, and navigate through directories.</span></span> <span data-ttu-id="54259-168">您可以使用其中一個這些 tooupload blob tooyour 儲存體帳戶並啟用加密。</span><span class="sxs-lookup"><span data-stu-id="54259-168">You can use one of these tooupload blobs tooyour storage account with encryption enabled.</span></span> <span data-ttu-id="54259-169">使用一些儲存體總管中，您也可以複製現有 blob 儲存體 tooa 不同容器 hello 儲存體帳戶中的資料或新的儲存體帳戶具有 SSE 啟用。</span><span class="sxs-lookup"><span data-stu-id="54259-169">With some storage explorers, you can also copy data from existing blob storage tooa different container in hello storage account or a new storage account that has SSE enabled.</span></span>

<span data-ttu-id="54259-170">toolearn 詳細資訊，請瀏覽[Azure 儲存體總管](storage-explorers.md)。</span><span class="sxs-lookup"><span data-stu-id="54259-170">toolearn more, please visit [Azure Storage Explorers](storage-explorers.md).</span></span>

### <a name="step-4-query-hello-status-of-hello-encrypted-data"></a><span data-ttu-id="54259-171">步驟 4: Hello 查詢 hello 狀態加密資料</span><span class="sxs-lookup"><span data-stu-id="54259-171">Step 4: Query hello status of hello encrypted data</span></span>
<span data-ttu-id="54259-172">已部署可讓您有物件 toodetermine tooquery hello 狀態或不加密過的 hello 儲存體用戶端程式庫的更新的版本。</span><span class="sxs-lookup"><span data-stu-id="54259-172">An updated version of hello Storage Client libraries has been deployed that allows you tooquery hello state of an object toodetermine if it is encrypted or not.</span></span> <span data-ttu-id="54259-173">這目前只能供 Blob 儲存體使用。</span><span class="sxs-lookup"><span data-stu-id="54259-173">This is currently only available for Blob storage.</span></span> <span data-ttu-id="54259-174">支援的檔案儲存體位於 hello 藍圖。</span><span class="sxs-lookup"><span data-stu-id="54259-174">Support for File storage is on hello roadmap.</span></span> 

<span data-ttu-id="54259-175">在 hello 同時，您可以呼叫[取得帳戶屬性](https://msdn.microsoft.com/library/azure/mt163553.aspx)hello 儲存體帳戶的 tooverify 已啟用加密或 hello hello Azure 入口網站中的儲存體帳戶屬性的檢視。</span><span class="sxs-lookup"><span data-stu-id="54259-175">In hello meantime, you can call [Get Account Properties](https://msdn.microsoft.com/library/azure/mt163553.aspx) tooverify that hello storage account has encryption enabled or view hello storage account properties in hello Azure portal.</span></span>

## <a name="encryption-and-decryption-workflow"></a><span data-ttu-id="54259-176">加密和解密工作流程</span><span class="sxs-lookup"><span data-stu-id="54259-176">Encryption and Decryption Workflow</span></span>
<span data-ttu-id="54259-177">以下是 hello 加密/解密工作流程的簡短描述：</span><span class="sxs-lookup"><span data-stu-id="54259-177">Here is a brief description of hello encryption/decryption workflow:</span></span>

* <span data-ttu-id="54259-178">hello 客戶上啟用加密 hello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="54259-178">hello customer enables encryption on hello storage account.</span></span>
* <span data-ttu-id="54259-179">Hello 客戶時寫入新的資料 （PUT Blob，將區塊、 PUT Page、 放置檔案等） tooBlob 或檔案的儲存體。使用 256 位元加密每次寫入[AES 加密](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard)，hello 最強的區塊的其中一個這類編碼器使用。</span><span class="sxs-lookup"><span data-stu-id="54259-179">When hello customer writes new data (PUT Blob, PUT Block, PUT Page, PUT File etc.) tooBlob or File storage; every write is encrypted using 256-bit [AES encryption](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard), one of hello strongest block ciphers available.</span></span>
* <span data-ttu-id="54259-180">Hello 客戶需要 tooaccess 資料 （取得 Blob 等） 時，資料時，會自動解密後再傳回 toohello 使用者。</span><span class="sxs-lookup"><span data-stu-id="54259-180">When hello customer needs tooaccess data (GET Blob, etc.), data is automatically decrypted before returning toohello user.</span></span>
* <span data-ttu-id="54259-181">如果已停用加密，已不再加密新的寫入，直到 hello 使用者來重新撰寫現有加密的資料仍會維持加密。</span><span class="sxs-lookup"><span data-stu-id="54259-181">If encryption is disabled, new writes are no longer encrypted and existing encrypted data remains encrypted until rewritten by hello user.</span></span> <span data-ttu-id="54259-182">雖然加密啟用狀態，將寫入 tooBlob 或檔案的儲存體將會加密。</span><span class="sxs-lookup"><span data-stu-id="54259-182">While encryption is enabled, writes tooBlob or File storage will be encrypted.</span></span> <span data-ttu-id="54259-183">hello 狀態的資料不會變更與 hello 切換 啟用/停用加密 hello 儲存體帳戶的使用者。</span><span class="sxs-lookup"><span data-stu-id="54259-183">hello state of data does not change with hello user toggling between enabling/disabling encryption for hello storage account.</span></span>
* <span data-ttu-id="54259-184">所有加密金鑰會由 Microsoft 儲存、加密及管理。</span><span class="sxs-lookup"><span data-stu-id="54259-184">All encryption keys are stored, encrypted, and managed by Microsoft.</span></span>

## <a name="frequently-asked-questions-about-storage-service-encryption-for-data-at-rest"></a><span data-ttu-id="54259-185">待用資料的儲存體服務加密的常見問題集</span><span class="sxs-lookup"><span data-stu-id="54259-185">Frequently asked questions about Storage Service Encryption for Data at Rest</span></span>
<span data-ttu-id="54259-186">**問：我有現有的傳統儲存體帳戶。可以在其上啟用 SSE 嗎？**</span><span class="sxs-lookup"><span data-stu-id="54259-186">**Q: I have an existing classic storage account. Can I enable SSE on it?**</span></span>

<span data-ttu-id="54259-187">答︰否，只有 Resource Manager 儲存體帳戶支援 SSE。</span><span class="sxs-lookup"><span data-stu-id="54259-187">A: No, SSE is only supported on Resource Manager storage accounts.</span></span>

<span data-ttu-id="54259-188">**問：我要如何在我的傳統儲存體帳戶中加密資料？**</span><span class="sxs-lookup"><span data-stu-id="54259-188">**Q: How can I encrypt data in my classic storage account?**</span></span>

<span data-ttu-id="54259-189">答： 您可以建立新的資源管理員儲存體帳戶，並將複製程式資料，請使用[AzCopy](storage-use-azcopy.md)從現有的傳統儲存體帳戶 tooyour 新建立的資源管理員儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="54259-189">A: You can create a new Resource Manager storage account and copy your data using [AzCopy](storage-use-azcopy.md) from your existing classic storage account tooyour newly created Resource Manager storage account.</span></span> 

<span data-ttu-id="54259-190">如果您移轉您的傳統儲存體帳戶 tooa 資源管理員儲存體帳戶，這項作業是在瞬間完成，您的帳戶 hello 類型變更，但不會影響現有的資料。</span><span class="sxs-lookup"><span data-stu-id="54259-190">If you migrate your classic storage account tooa Resource Manager storage account, this operation is instantaneous, it changes hello type of your account but does not effect your existing data.</span></span> <span data-ttu-id="54259-191">只有在啟用加密之後，才會加密所有新資料。</span><span class="sxs-lookup"><span data-stu-id="54259-191">Any new data written will be encrypted only after enabling encryption.</span></span> <span data-ttu-id="54259-192">如需詳細資訊，請參閱[平台支援移轉的 IaaS 資源從傳統 tooResource 管理員](https://azure.microsoft.com/blog/iaas-migration-classic-resource-manager/)。</span><span class="sxs-lookup"><span data-stu-id="54259-192">For more information, see [Platform Supported Migration of IaaS Resources from Classic tooResource Manager](https://azure.microsoft.com/blog/iaas-migration-classic-resource-manager/).</span></span> <span data-ttu-id="54259-193">請注意，只有針對 Blob 和「檔案」服務才支援此功能。</span><span class="sxs-lookup"><span data-stu-id="54259-193">Please note that this is supported only for Blob and File services.</span></span>

<span data-ttu-id="54259-194">**問：我有現有的 Resource Manager 儲存體帳戶。可以在其上啟用 SSE 嗎？**</span><span class="sxs-lookup"><span data-stu-id="54259-194">**Q: I have an existing Resource Manager storage account. Can I enable SSE on it?**</span></span>

<span data-ttu-id="54259-195">答︰是，但只會加密新寫入的資料。</span><span class="sxs-lookup"><span data-stu-id="54259-195">A: Yes, but only newly written data will be encrypted.</span></span> <span data-ttu-id="54259-196">並不會返回及加密已經存在的資料。</span><span class="sxs-lookup"><span data-stu-id="54259-196">It does not go back and encrypt data that was already present.</span></span> <span data-ttu-id="54259-197">這是尚未支援 hello 檔案儲存體預覽。</span><span class="sxs-lookup"><span data-stu-id="54259-197">This is not yet supported for hello File Storage Preview.</span></span>

<span data-ttu-id="54259-198">**問： 我想要 tooencrypt hello 目前資料中現有的資源管理員儲存體帳戶？**</span><span class="sxs-lookup"><span data-stu-id="54259-198">**Q: I would like tooencrypt hello current data in an existing Resource Manager storage account?**</span></span>

<span data-ttu-id="54259-199">答︰您可以在 Resource Manager 儲存體帳戶中隨時啟用 SSE。</span><span class="sxs-lookup"><span data-stu-id="54259-199">A: You can enable SSE at any time in a Resource Manager storage account.</span></span> <span data-ttu-id="54259-200">不過，不會加密已經存在的資料。</span><span class="sxs-lookup"><span data-stu-id="54259-200">However, data that were already present will not be encrypted.</span></span> <span data-ttu-id="54259-201">tooencrypt 現有的資料，您可以將它們複製 tooanother 名稱或另一個容器，然後再移除 hello 未加密版本。</span><span class="sxs-lookup"><span data-stu-id="54259-201">tooencrypt existing data, you can copy them tooanother name or another container and then remove hello unencrypted versions.</span></span>

<span data-ttu-id="54259-202">**問︰我正在使用進階儲存體，我是否可以使用 SSE？**</span><span class="sxs-lookup"><span data-stu-id="54259-202">**Q: I'm using Premium storage; can I use SSE?**</span></span>

<span data-ttu-id="54259-203">答︰是，SSE 支援標準儲存體和進階儲存體。</span><span class="sxs-lookup"><span data-stu-id="54259-203">A: Yes, SSE is supported on both Standard Storage and Premium Storage.</span></span>  <span data-ttu-id="54259-204">Hello 檔案服務不支援進階儲存體。</span><span class="sxs-lookup"><span data-stu-id="54259-204">Premium Storage is not supported for hello File Service.</span></span>

<span data-ttu-id="54259-205">**問︰如果我建立新的儲存體帳戶，並啟用 SSE，然後使用該儲存體帳戶建立新的 VM，是否表示我的 VM 會加密？**</span><span class="sxs-lookup"><span data-stu-id="54259-205">**Q: If I create a new storage account and enable SSE, then create a new VM using that storage account, does that mean my VM is encrypted?**</span></span>

<span data-ttu-id="54259-206">答： 會。</span><span class="sxs-lookup"><span data-stu-id="54259-206">A: Yes.</span></span> <span data-ttu-id="54259-207">建立使用 hello 新儲存體帳戶的任何磁碟都將加密，只要在建立之後啟用 SSE。</span><span class="sxs-lookup"><span data-stu-id="54259-207">Any disks created that use hello new storage account will be encrypted, as long as they are created after SSE is enabled.</span></span> <span data-ttu-id="54259-208">如果已在使用 Azure Market Place hello VHD 基底映像建立 VM 的 hello 將保持未加密狀態。不過，hello VM 已調整大小之後，執行任何寫入將會加密。</span><span class="sxs-lookup"><span data-stu-id="54259-208">If hello VM was created using Azure Market Place, hello VHD base image will remain unencrypted; however, any writes done after hello VM has spun up will be encrypted.</span></span>

<span data-ttu-id="54259-209">**問︰是否可以使用 Azure PowerShell 和 Azure CLI 建立新的儲存體帳戶並且啟用 SSE？**</span><span class="sxs-lookup"><span data-stu-id="54259-209">**Q: Can I create new storage accounts with SSE enabled using Azure PowerShell and Azure CLI?**</span></span>

<span data-ttu-id="54259-210">答： 會。</span><span class="sxs-lookup"><span data-stu-id="54259-210">A: Yes.</span></span>

<span data-ttu-id="54259-211">**問︰如果已啟用 SSE，Azure 儲存體的成本會多出多少？**</span><span class="sxs-lookup"><span data-stu-id="54259-211">**Q: How much more does Azure Storage cost if SSE is enabled?**</span></span>

<span data-ttu-id="54259-212">答：沒有任何額外成本。</span><span class="sxs-lookup"><span data-stu-id="54259-212">A: There is no additional cost.</span></span>

<span data-ttu-id="54259-213">**問： 誰管理 hello 加密金鑰？**</span><span class="sxs-lookup"><span data-stu-id="54259-213">**Q: Who manages hello encryption keys?**</span></span>

<span data-ttu-id="54259-214">答： hello 金鑰是由 Microsoft 管理。</span><span class="sxs-lookup"><span data-stu-id="54259-214">A: hello keys are managed by Microsoft.</span></span>

<span data-ttu-id="54259-215">**問︰我可以使用自己的加密金鑰嗎？**</span><span class="sxs-lookup"><span data-stu-id="54259-215">**Q: Can I use my own encryption keys?**</span></span>

<span data-ttu-id="54259-216">答： 我們會努力提供功能以客戶 toobring 他們自己的加密金鑰。</span><span class="sxs-lookup"><span data-stu-id="54259-216">A: We are working on providing capabilities for customers toobring their own encryption keys.</span></span>

<span data-ttu-id="54259-217">**問： 是否可以撤銷存取 toohello 加密金鑰？**</span><span class="sxs-lookup"><span data-stu-id="54259-217">**Q: Can I revoke access toohello encryption keys?**</span></span>

<span data-ttu-id="54259-218">答： 不是在這個階段中。hello 金鑰完全是由 Microsoft 管理。</span><span class="sxs-lookup"><span data-stu-id="54259-218">A: Not at this time; hello keys are fully managed by Microsoft.</span></span>

<span data-ttu-id="54259-219">**問︰我建立新的儲存體帳戶時是否預設啟用 SSE？**</span><span class="sxs-lookup"><span data-stu-id="54259-219">**Q: Is SSE enabled by default when I create a new storage account?**</span></span>

<span data-ttu-id="54259-220">答： SSE 不會啟用預設值;您可以使用 Azure 入口網站 tooenable hello 它。</span><span class="sxs-lookup"><span data-stu-id="54259-220">A: SSE is not enabled by default; you can use hello Azure portal tooenable it.</span></span> <span data-ttu-id="54259-221">您可以也以程式設計方式啟用此功能使用 hello 儲存體資源提供者 REST API。</span><span class="sxs-lookup"><span data-stu-id="54259-221">You can also programmatically enable this feature using hello Storage Resource Provider REST API.</span></span>

<span data-ttu-id="54259-222">**問︰這項功能與 Azure 磁碟加密有什麼不同？**</span><span class="sxs-lookup"><span data-stu-id="54259-222">**Q: How is this different from Azure Disk Encryption?**</span></span>

<span data-ttu-id="54259-223">答： 這項功能是使用的 tooencrypt Azure Blob 儲存體中的資料。</span><span class="sxs-lookup"><span data-stu-id="54259-223">A: This feature is used tooencrypt data in Azure Blob storage.</span></span> <span data-ttu-id="54259-224">hello Azure 磁碟加密是使用的 tooencrypt 中 IaaS Vm 的 OS 和資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="54259-224">hello Azure Disk Encryption is used tooencrypt OS and Data disks in IaaS VMs.</span></span> <span data-ttu-id="54259-225">如需詳細資訊，請參閱我們的[儲存體安全性指南](storage-security-guide.md)。</span><span class="sxs-lookup"><span data-stu-id="54259-225">For more details, please visit our [Storage Security Guide](storage-security-guide.md).</span></span>

<span data-ttu-id="54259-226">**問： 如果我啟用 SSE，然後在並 hello 磁碟上啟用 Azure 磁碟加密？**</span><span class="sxs-lookup"><span data-stu-id="54259-226">**Q: What if I enable SSE, and then go in and enable Azure Disk Encryption on hello disks?**</span></span>

<span data-ttu-id="54259-227">答︰這會順暢地運作。</span><span class="sxs-lookup"><span data-stu-id="54259-227">A: This will work seamlessly.</span></span> <span data-ttu-id="54259-228">這兩種方法都會加密您的資料。</span><span class="sxs-lookup"><span data-stu-id="54259-228">Your data will be encrypted by both methods.</span></span>

<span data-ttu-id="54259-229">**問： 我的儲存體帳戶設定 toobe 無法重複地理複寫。如果啟用 SSE，我的備援複本是否也會加密？**</span><span class="sxs-lookup"><span data-stu-id="54259-229">**Q: My storage account is set up toobe replicated geo-redundantly. If I enable SSE, will my redundant copy also be encrypted?**</span></span>

<span data-ttu-id="54259-230">A: [是]，加密 hello 儲存體帳戶的所有副本，並支援所有的備援選項 – 在本機備援儲存體 (LRS)、 區域備援儲存體 (ZRS)、 地理備援儲存體 (GRS) 和讀取權異地備援儲存體 (RA-GRS) –。</span><span class="sxs-lookup"><span data-stu-id="54259-230">A: Yes, all copies of hello storage account are encrypted, and all redundancy options – Locally Redundant Storage (LRS), Zone-Redundant Storage (ZRS), Geo-Redundant Storage (GRS), and Read Access Geo-Redundant Storage (RA-GRS) – are supported.</span></span>

<span data-ttu-id="54259-231">**問︰我無法在我的儲存體帳戶上啟用加密。**</span><span class="sxs-lookup"><span data-stu-id="54259-231">**Q: I can't enable encryption on my storage account.**</span></span>

<span data-ttu-id="54259-232">答︰這是 Resource Manager 儲存體帳戶嗎？</span><span class="sxs-lookup"><span data-stu-id="54259-232">A: Is it a Resource Manager storage account?</span></span> <span data-ttu-id="54259-233">不支援傳統儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="54259-233">Classic storage accounts are not supported.</span></span> 

<span data-ttu-id="54259-234">**問︰是否只有在特定區域中允許 SSE？**</span><span class="sxs-lookup"><span data-stu-id="54259-234">**Q: Is SSE only permitted in specific regions?**</span></span>

<span data-ttu-id="54259-235">答： hello SSE 可在所有區域的 Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="54259-235">A: hello SSE is available in all regions for Blob storage.</span></span> <span data-ttu-id="54259-236">請檢查檔案儲存的 hello 可用性一節。</span><span class="sxs-lookup"><span data-stu-id="54259-236">Please check hello Availability Section for File storage.</span></span> 

<span data-ttu-id="54259-237">**問： 如何連絡有人如果我有任何問題或想 tooprovide 意見反應？**</span><span class="sxs-lookup"><span data-stu-id="54259-237">**Q: How do I contact someone if I have any issues or want tooprovide feedback?**</span></span>

<span data-ttu-id="54259-238">答： 請連絡[ ssediscussions@microsoft.com ](mailto:ssediscussions@microsoft.com)是否有任何問題相關 tooStorage 服務加密。</span><span class="sxs-lookup"><span data-stu-id="54259-238">A: Please contact [ssediscussions@microsoft.com](mailto:ssediscussions@microsoft.com) for any issues related tooStorage Service Encryption.</span></span>

## <a name="next-steps"></a><span data-ttu-id="54259-239">後續步驟</span><span class="sxs-lookup"><span data-stu-id="54259-239">Next Steps</span></span>
<span data-ttu-id="54259-240">Azure 儲存體提供一組完整的安全性功能，同時讓開發人員 toobuild 安全的應用程式。</span><span class="sxs-lookup"><span data-stu-id="54259-240">Azure Storage provides a comprehensive set of security capabilities which together enable developers toobuild secure applications.</span></span> <span data-ttu-id="54259-241">如需詳細資訊，請瀏覽 hello[存放安全性指南 》](storage-security-guide.md)。</span><span class="sxs-lookup"><span data-stu-id="54259-241">For more details, visit hello [Storage Security Guide](storage-security-guide.md).</span></span>

