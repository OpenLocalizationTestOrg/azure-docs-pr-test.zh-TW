---
title: "aaaGet 啟動使用儲存體總管 （預覽） |Microsoft 文件"
description: "使用儲存體總管管理 Azure 儲存體資源 (預覽)"
services: storage
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 1ed0f096-494d-49c4-ab71-f4164ee19ec8
ms.service: storage
ms.devlang: multiple
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 7/17/2017
ms.author: kraigb
ms.openlocfilehash: 57737b51baace92858eb07c7dbc3139bd7e041f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-storage-explorer-preview"></a><span data-ttu-id="a4200-103">開始使用儲存體總管 (預覽)</span><span class="sxs-lookup"><span data-stu-id="a4200-103">Get started with Storage Explorer (Preview)</span></span>
## <a name="overview"></a><span data-ttu-id="a4200-104">概觀</span><span class="sxs-lookup"><span data-stu-id="a4200-104">Overview</span></span>
<span data-ttu-id="a4200-105">Azure 儲存體總管 （預覽） 是獨立應用程式，可讓您 tooeasily 使用在 Windows、 macOS 和 Linux 的 Azure 儲存體資料。</span><span class="sxs-lookup"><span data-stu-id="a4200-105">Azure Storage Explorer (Preview) is a standalone app that enables you tooeasily work with Azure Storage data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="a4200-106">在本文中，您會學習 hello 連線 tooand 管理您的 Azure 儲存體帳戶的各種方式。</span><span class="sxs-lookup"><span data-stu-id="a4200-106">In this article, you learn hello various ways of connecting tooand managing your Azure storage accounts.</span></span>

![Microsoft Azure 儲存體 Explorer (預覽)][15]

## <a name="prerequisites"></a><span data-ttu-id="a4200-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="a4200-108">Prerequisites</span></span>
* [<span data-ttu-id="a4200-109">下載並安裝儲存體總管 (預覽)</span><span class="sxs-lookup"><span data-stu-id="a4200-109">Download and install Storage Explorer (Preview)</span></span>](http://www.storageexplorer.com)

## <a name="connect-tooa-storage-account-or-service"></a><span data-ttu-id="a4200-110">連接 tooa 儲存體帳戶或服務</span><span class="sxs-lookup"><span data-stu-id="a4200-110">Connect tooa storage account or service</span></span>
<span data-ttu-id="a4200-111">儲存體總管 （預覽） 提供數種方式 tooconnect toostorage 帳戶。</span><span class="sxs-lookup"><span data-stu-id="a4200-111">Storage Explorer (Preview) provides several ways tooconnect toostorage accounts.</span></span> <span data-ttu-id="a4200-112">例如，您可以：</span><span class="sxs-lookup"><span data-stu-id="a4200-112">For example, you can:</span></span>
* <span data-ttu-id="a4200-113">連接與您 Azure 訂用帳戶相關聯的 toostorage 帳戶。</span><span class="sxs-lookup"><span data-stu-id="a4200-113">Connect toostorage accounts associated with your Azure subscriptions.</span></span>
* <span data-ttu-id="a4200-114">從其他 Azure 訂用帳戶連接 toostorage 帳戶和服務所共用。</span><span class="sxs-lookup"><span data-stu-id="a4200-114">Connect toostorage accounts and services that are shared from other Azure subscriptions.</span></span>
* <span data-ttu-id="a4200-115">連接 tooand 管理使用 hello Azure 儲存體模擬器的本機儲存體。</span><span class="sxs-lookup"><span data-stu-id="a4200-115">Connect tooand manage local storage by using hello Azure Storage Emulator.</span></span> 

<span data-ttu-id="a4200-116">此外，您可以使用全球和國家 Azure 中的儲存體帳戶：</span><span class="sxs-lookup"><span data-stu-id="a4200-116">In addition, you can work with storage accounts in global and national Azure:</span></span>

* <span data-ttu-id="a4200-117">[連接 Azure 訂用帳戶 tooan](#connect-to-an-azure-subscription)： 管理屬於 tooyour Azure 訂用帳戶的儲存體資源。</span><span class="sxs-lookup"><span data-stu-id="a4200-117">[Connect tooan Azure subscription](#connect-to-an-azure-subscription): Manage storage resources that belong tooyour Azure subscription.</span></span>
* <span data-ttu-id="a4200-118">[使用本機開發儲存體](#work-with-local-development-storage)： 管理使用 hello Azure 儲存體模擬器的本機儲存體。</span><span class="sxs-lookup"><span data-stu-id="a4200-118">[Work with local development storage](#work-with-local-development-storage): Manage local storage by using hello Azure Storage Emulator.</span></span>
* <span data-ttu-id="a4200-119">[附加 tooexternal 儲存體](#attach-or-detach-an-external-storage-account)： 管理屬於 tooanother Azure 訂用帳戶的儲存體資源，或已國家 （地區） 的 Azure 雲端 底下使用 hello 儲存體帳戶的名稱、 金鑰和端點。</span><span class="sxs-lookup"><span data-stu-id="a4200-119">[Attach tooexternal storage](#attach-or-detach-an-external-storage-account): Manage storage resources that belong tooanother Azure subscription or that are under national Azure clouds by using hello storage account's name, key, and endpoints.</span></span>
* <span data-ttu-id="a4200-120">[使用 SAS 附加儲存體帳戶](#attach-storage-account-using-sas)： 管理屬於 tooanother Azure 訂用帳戶使用共用的存取簽章 (SAS) 存放裝置資源。</span><span class="sxs-lookup"><span data-stu-id="a4200-120">[Attach a storage account by using an SAS](#attach-storage-account-using-sas): Manage storage resources that belong tooanother Azure subscription by using a shared access signature (SAS).</span></span>
* <span data-ttu-id="a4200-121">[使用 SAS 會將服務附加](#attach-service-using-sas)： 管理使用 SAS 所屬 tooanother Azure 訂用帳戶特定的儲存體服務 （blob 容器、 佇列或資料表）。</span><span class="sxs-lookup"><span data-stu-id="a4200-121">[Attach a service by using an SAS](#attach-service-using-sas): Manage a specific storage service (blob container, queue, or table) that belongs tooanother Azure subscription by using an SAS.</span></span>

## <a name="connect-tooan-azure-subscription"></a><span data-ttu-id="a4200-122">連接 tooan Azure 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="a4200-122">Connect tooan Azure subscription</span></span>
> [!NOTE]
> <span data-ttu-id="a4200-123">如果您沒有 Azure 帳戶，可以[申請免費試用](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F)，或是[啟用自己的 Visual Studio 訂閱者權益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F)。</span><span class="sxs-lookup"><span data-stu-id="a4200-123">If you don't have an Azure account, you can [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) or [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span>
>
>

1. <span data-ttu-id="a4200-124">在儲存體 Explorer (預覽) 中，選取 [Azure 帳戶設定] 。</span><span class="sxs-lookup"><span data-stu-id="a4200-124">In Storage Explorer (Preview), select **Azure Account settings**.</span></span>

    ![Azure 帳戶設定][0]

2. <span data-ttu-id="a4200-126">hello 左的窗格會顯示您已登入的所有 hello Microsoft 帳戶。</span><span class="sxs-lookup"><span data-stu-id="a4200-126">hello left pane displays all hello Microsoft accounts you've signed in to.</span></span> <span data-ttu-id="a4200-127">tooconnect tooanother 帳戶，請選取**將帳戶加入**，然後依照 hello 指示 toosign 使用至少一個有效的 Azure 訂閱相關聯的 Microsoft 帳戶。</span><span class="sxs-lookup"><span data-stu-id="a4200-127">tooconnect tooanother account, select **Add an account**, and then follow hello instructions toosign in with a Microsoft account that is associated with at least one active Azure subscription.</span></span>

    >[!NOTE]
    ><span data-ttu-id="a4200-128">目前不支援連接 toonational Azure （例如 Azure 德國、 Azure 政府和透過登入 Azure China）。</span><span class="sxs-lookup"><span data-stu-id="a4200-128">Connecting toonational Azure (such as Azure Germany, Azure Government, and Azure China via sign-in) is currently not supported.</span></span> <span data-ttu-id="a4200-129">請參閱 hello"附加或卸離外部儲存體帳戶 」 一節以取得如何 tooconnect toonational Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="a4200-129">See hello "Attach or detach an external storage account" section for how tooconnect toonational Azure storage accounts.</span></span>

3. <span data-ttu-id="a4200-130">之後您已成功使用登入 Microsoft 帳戶，hello 左窗格中會填入 hello 與該帳戶相關聯的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="a4200-130">After you successfully sign in with a Microsoft account, hello left pane is populated with hello Azure subscriptions associated with that account.</span></span> <span data-ttu-id="a4200-131">選取 hello Azure 訂用帳戶，您想 toowork，然後選取**套用**。</span><span class="sxs-lookup"><span data-stu-id="a4200-131">Select hello Azure subscriptions that you want toowork with, and then select **Apply**.</span></span> <span data-ttu-id="a4200-132">(選取**所有訂用帳戶**切換選取所有或無 hello 列出 Azure 訂用帳戶。)</span><span class="sxs-lookup"><span data-stu-id="a4200-132">(Selecting **All subscriptions** toggles selecting all or none of hello listed Azure subscriptions.)</span></span>

    ![選取 Azure 訂用帳戶][3]  
    <span data-ttu-id="a4200-134">hello 左的窗格會顯示 hello 與 hello 選取 Azure 訂用帳戶相關聯的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="a4200-134">hello left pane displays hello storage accounts associated with hello selected Azure subscriptions.</span></span>

    ![已選取的 Azure 訂用帳戶][4]

## <a name="connect-tooan-azure-stack-subscription"></a><span data-ttu-id="a4200-136">連接 tooan 堆疊 Azure 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="a4200-136">Connect tooan Azure Stack subscription</span></span>

<span data-ttu-id="a4200-137">如需連接 tooan 堆疊 Azure 訂用帳戶資訊，請參閱[連接儲存體總管 tooan 堆疊 Azure 訂用帳戶](azure-stack/azure-stack-storage-connect-se.md)。</span><span class="sxs-lookup"><span data-stu-id="a4200-137">For information about connecting tooan Azure Stack subscription, see [Connect Storage Explorer tooan Azure Stack subscription](azure-stack/azure-stack-storage-connect-se.md).</span></span>

## <a name="work-with-local-development-storage"></a><span data-ttu-id="a4200-138">使用本機開發儲存體</span><span class="sxs-lookup"><span data-stu-id="a4200-138">Work with local development storage</span></span>
<span data-ttu-id="a4200-139">使用儲存體總管 （預覽），您可以對本機儲存體使用處理 hello Azure 儲存體模擬器。</span><span class="sxs-lookup"><span data-stu-id="a4200-139">With Storage Explorer (Preview), you can work against local storage by using hello Azure Storage Emulator.</span></span> <span data-ttu-id="a4200-140">這種方法可讓您撰寫的程式碼和測試儲存區，而不一定需要在 Azure 上部署儲存體帳戶，因為 hello 儲存體帳戶正在模擬的 hello Azure 儲存體模擬器。</span><span class="sxs-lookup"><span data-stu-id="a4200-140">This approach lets you write code against and test storage without necessarily having a storage account deployed on Azure, because hello storage account is being emulated by hello Azure Storage Emulator.</span></span>

> [!NOTE]
> <span data-ttu-id="a4200-141">目前只適用於 Windows 支援 hello Azure 儲存體模擬器。</span><span class="sxs-lookup"><span data-stu-id="a4200-141">hello Azure Storage Emulator is currently supported only for Windows.</span></span>
>
>

1. <span data-ttu-id="a4200-142">在 hello 的儲存體總管 （預覽） 的左窗格中展開 hello **（本機及附加）** > **儲存體帳戶** > **（開發）**節點。</span><span class="sxs-lookup"><span data-stu-id="a4200-142">In hello left pane of Storage Explorer (Preview), expand hello **(Local and Attached)** > **Storage Accounts** > **(Development)** node.</span></span>

    ![本機開發節點][21]

2. <span data-ttu-id="a4200-144">如果您尚未安裝 hello Azure 儲存體模擬器，您必須提示的 toodo 是透過資料列。</span><span class="sxs-lookup"><span data-stu-id="a4200-144">If you have not yet installed hello Azure Storage Emulator, you are prompted toodo so via an infobar.</span></span> <span data-ttu-id="a4200-145">如果顯示 hello 資訊列，選取**最新版本的下載 hello**，然後再安裝 hello 模擬器。</span><span class="sxs-lookup"><span data-stu-id="a4200-145">If hello infobar is displayed, select **Download hello latest version**, and then install hello emulator.</span></span>

    ![下載 Azure 儲存體模擬器提示字元][22]

3. <span data-ttu-id="a4200-147">Hello 模擬器安裝之後，您可以建立和使用本機 blob、 佇列和資料表。</span><span class="sxs-lookup"><span data-stu-id="a4200-147">After hello emulator is installed, you can create and work with local blobs, queues, and tables.</span></span> <span data-ttu-id="a4200-148">toolearn toowork 與每個儲存體帳戶的型別，請參閱 hello 下列其中一種：</span><span class="sxs-lookup"><span data-stu-id="a4200-148">toolearn how toowork with each storage account type, see one of hello following:</span></span>

    * [<span data-ttu-id="a4200-149">管理 Azure Blob 儲存體資源</span><span class="sxs-lookup"><span data-stu-id="a4200-149">Manage Azure blob storage resources</span></span>](vs-azure-tools-storage-explorer-blobs.md)
    * <span data-ttu-id="a4200-150">管理 Azure 檔案共用儲存體資源：敬請期待 </span><span class="sxs-lookup"><span data-stu-id="a4200-150">Manage Azure file share storage resources: *Coming soon*</span></span>
    * <span data-ttu-id="a4200-151">管理 Azure 佇列儲存體資源：敬請期待 </span><span class="sxs-lookup"><span data-stu-id="a4200-151">Manage Azure queue storage resources: *Coming soon*</span></span>
    * <span data-ttu-id="a4200-152">管理 Azure 表格儲存體資源：敬請期待 </span><span class="sxs-lookup"><span data-stu-id="a4200-152">Manage Azure table storage resources: *Coming soon*</span></span>

## <a name="attach-or-detach-an-external-storage-account"></a><span data-ttu-id="a4200-153">附加或卸離外部儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="a4200-153">Attach or detach an external storage account</span></span>
<span data-ttu-id="a4200-154">使用儲存體總管 （預覽），您可以附加 tooexternal 儲存體帳戶，因此可以輕鬆地共用儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="a4200-154">With Storage Explorer (Preview), you can attach tooexternal storage accounts so that storage accounts can be easily shared.</span></span> <span data-ttu-id="a4200-155">本章節將說明如何 tooattach too(and detach from) 外部儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="a4200-155">This section explains how tooattach too(and detach from) external storage accounts.</span></span>

### <a name="get-hello-storage-account-credentials"></a><span data-ttu-id="a4200-156">取得 hello 儲存體帳戶認證</span><span class="sxs-lookup"><span data-stu-id="a4200-156">Get hello storage account credentials</span></span>
<span data-ttu-id="a4200-157">tooshare 外部儲存體帳戶，hello 該帳戶擁有者必須先取得 hello 帳戶 （帳戶名稱和金鑰） 的 hello 認證並再想 tooattach toothat （外部） 帳戶的 hello 人員分享相關資訊。</span><span class="sxs-lookup"><span data-stu-id="a4200-157">tooshare an external storage account, hello owner of that account must first get hello credentials (account name and key) for hello account and then share that information with hello person who wants tooattach toothat (external) account.</span></span> <span data-ttu-id="a4200-158">您可以藉由 hello 下列取得 hello 儲存體帳戶認證，透過 hello Azure 入口網站：</span><span class="sxs-lookup"><span data-stu-id="a4200-158">You can obtain hello storage account credentials via hello Azure portal by doing hello following:</span></span>

1. <span data-ttu-id="a4200-159">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="a4200-159">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="a4200-160">選取 [瀏覽] 。</span><span class="sxs-lookup"><span data-stu-id="a4200-160">Select **Browse**.</span></span>

3. <span data-ttu-id="a4200-161">選取 [儲存體帳戶] 。</span><span class="sxs-lookup"><span data-stu-id="a4200-161">Select **Storage Accounts**.</span></span>

4. <span data-ttu-id="a4200-162">在 hello**儲存體帳戶**刀鋒視窗中，選取所需的 hello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="a4200-162">On hello **Storage Accounts** blade, select hello desired storage account.</span></span>

5. <span data-ttu-id="a4200-163">在 hello**設定**hello 刀鋒視窗選取儲存體帳戶中，選取**存取金鑰**。</span><span class="sxs-lookup"><span data-stu-id="a4200-163">On hello **Settings** blade for hello selected storage account, select **Access keys**.</span></span>

    ![存取金鑰選項][5]

6. <span data-ttu-id="a4200-165">在 hello**存取金鑰**刀鋒視窗，複製 hello**儲存體帳戶名稱**和**key1**附加 toohello 儲存體帳戶時使用的值。</span><span class="sxs-lookup"><span data-stu-id="a4200-165">On hello **Access keys** blade, copy hello **Storage account name** and **key1** values for use when attaching toohello storage account.</span></span>

    ![存取金鑰][6]

### <a name="attach-tooan-external-storage-account"></a><span data-ttu-id="a4200-167">附加 tooan 外部儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="a4200-167">Attach tooan external storage account</span></span>
<span data-ttu-id="a4200-168">tooattach tooan 外部儲存體帳戶，您需要 hello 帳戶名稱和金鑰。</span><span class="sxs-lookup"><span data-stu-id="a4200-168">tooattach tooan external storage account, you need hello account's name and key.</span></span> <span data-ttu-id="a4200-169">hello < Get hello 儲存體帳戶認證 > 一節說明這些值從 tooobtain hello Azure 入口網站的方式。</span><span class="sxs-lookup"><span data-stu-id="a4200-169">hello "Get hello storage account credentials" section explains how tooobtain these values from hello Azure portal.</span></span> <span data-ttu-id="a4200-170">不過，在 hello 入口網站，hello 帳戶金鑰稱為**key1**。</span><span class="sxs-lookup"><span data-stu-id="a4200-170">However, in hello portal, hello account key is called **key1**.</span></span> <span data-ttu-id="a4200-171">因此在儲存體總管 （預覽） 要求的帳戶金鑰時，您輸入 hello **key1**值。</span><span class="sxs-lookup"><span data-stu-id="a4200-171">So where Storage Explorer (Preview) asks for an account key, you enter hello **key1** value.</span></span>

1. <span data-ttu-id="a4200-172">在儲存體總管 （預覽） 中，選取**tooAzure 存放裝置連線**。</span><span class="sxs-lookup"><span data-stu-id="a4200-172">In Storage Explorer (Preview), select **Connect tooAzure storage**.</span></span>

    ![連接 tooAzure 儲存體選項][23]

2. <span data-ttu-id="a4200-174">在 hello**連接 tooAzure 儲存體**對話方塊方塊中，指定 hello 帳號金鑰 (hello **key1** hello Azure 入口網站中的值)，然後選取**下一步**。</span><span class="sxs-lookup"><span data-stu-id="a4200-174">In hello **Connect tooAzure Storage** dialog box, specify hello account key (hello **key1** value from hello Azure portal), and then select **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="a4200-175">國家 （地區) 在 Azure 上，您可以從儲存體帳戶輸入 hello 儲存體連接字串。</span><span class="sxs-lookup"><span data-stu-id="a4200-175">You can enter hello storage connection string from a storage account on national Azure.</span></span> <span data-ttu-id="a4200-176">例如，tooconnect tooAzure 德國儲存體帳戶，請輸入連接字串類似 toohello 下列：</span><span class="sxs-lookup"><span data-stu-id="a4200-176">For example, tooconnect tooAzure Germany storage accounts, enter connection strings similar toohello following:</span></span> 
    >
    >* <span data-ttu-id="a4200-177">DefaultEndpointsProtocol=https</span><span class="sxs-lookup"><span data-stu-id="a4200-177">DefaultEndpointsProtocol=https</span></span>
    >* <span data-ttu-id="a4200-178">AccountName=cawatest03</span><span class="sxs-lookup"><span data-stu-id="a4200-178">AccountName=cawatest03</span></span>
    >* <span data-ttu-id="a4200-179">AccountKey=<storage_account_key></span><span class="sxs-lookup"><span data-stu-id="a4200-179">AccountKey=<storage_account_key></span></span>
    >* <span data-ttu-id="a4200-180">EndpointSuffix=core.cloudapi.de</span><span class="sxs-lookup"><span data-stu-id="a4200-180">EndpointSuffix=core.cloudapi.de</span></span>
    
    ><span data-ttu-id="a4200-181">您可以取得 hello 連接字串從 hello Azure 入口網站中 hello 相同方式中所述 hello 「 取得 hello 儲存體帳戶認證 」 一節。</span><span class="sxs-lookup"><span data-stu-id="a4200-181">You can get hello connection string from hello Azure portal in hello same way as described in hello "Get hello storage account credentials" section.</span></span>

    ![連接 tooAzure 儲存對話方塊][24]

3. <span data-ttu-id="a4200-183">在 hello**附加外部儲存體**對話方塊中的，在 hello**帳戶名稱**方塊、 輸入 hello 儲存體帳戶名稱，指定所需的設定，，然後選取**下一步**。</span><span class="sxs-lookup"><span data-stu-id="a4200-183">In hello **Attach External Storage** dialog box, in hello **Account name** box, enter hello storage account name, specify any other desired settings, and then select **Next**.</span></span>

    ![連結外部儲存體對話方塊][8]

4. <span data-ttu-id="a4200-185">在 hello**連接摘要**對話方塊方塊中，確認 hello 資訊。</span><span class="sxs-lookup"><span data-stu-id="a4200-185">In hello **Connection Summary** dialog box, verify hello information.</span></span> <span data-ttu-id="a4200-186">如果您想要 toochange 任何項目，選取**回**並重新輸入所需的 hello 設定。</span><span class="sxs-lookup"><span data-stu-id="a4200-186">If you want toochange anything, select **Back** and reenter hello desired settings.</span></span> 

5. <span data-ttu-id="a4200-187">選取 [ **連接**]。</span><span class="sxs-lookup"><span data-stu-id="a4200-187">Select **Connect**.</span></span>

6. <span data-ttu-id="a4200-188">已成功連接之後，會顯示 hello 外部儲存體帳戶**（外部）**附加 toohello 儲存體帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="a4200-188">After it is successfully connected, hello external storage account is displayed with **(External)** appended toohello storage account name.</span></span>

    ![結果的連接 tooan 外部儲存體帳戶][9]

### <a name="detach-from-an-external-storage-account"></a><span data-ttu-id="a4200-190">從外部儲存體帳戶卸離</span><span class="sxs-lookup"><span data-stu-id="a4200-190">Detach from an external storage account</span></span>
1. <span data-ttu-id="a4200-191">以滑鼠右鍵按一下您想 toodetach，，然後選取 hello 外部儲存體帳戶**卸離**。</span><span class="sxs-lookup"><span data-stu-id="a4200-191">Right-click hello external storage account that you want toodetach, and then select **Detach**.</span></span>

    ![中斷與儲存體選項的連結][10]

2. <span data-ttu-id="a4200-193">在 hello 確認訊息中，選取 **是**tooconfirm hello 中斷連結，從 hello 外部儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="a4200-193">In hello confirmation message, select **Yes** tooconfirm hello detachment from hello external storage account.</span></span>

## <a name="attach-a-storage-account-by-using-an-sas"></a><span data-ttu-id="a4200-194">使用 SAS 連結儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="a4200-194">Attach a storage account by using an SAS</span></span>
<span data-ttu-id="a4200-195">[SAS](storage/common/storage-dotnet-shared-access-signature-part-1.md)讓 hello 而不需要 tooprovide Azure 訂用帳戶認證授與的暫時存取 tooa 儲存體帳戶的 Azure 訂用帳戶管理員。</span><span class="sxs-lookup"><span data-stu-id="a4200-195">An [SAS](storage/common/storage-dotnet-shared-access-signature-part-1.md) lets hello admin of an Azure subscription grant temporary access tooa storage account without having tooprovide Azure subscription credentials.</span></span>

<span data-ttu-id="a4200-196">tooillustrate 此案例中，讓我們說該使用者 a 是系統管理員的 Azure 訂用帳戶，而且 UserA 想 tooallow UserB tooaccess 有限的時間以特定的權限的儲存體帳戶：</span><span class="sxs-lookup"><span data-stu-id="a4200-196">tooillustrate this scenario, let's say that UserA is an admin of an Azure subscription, and UserA wants tooallow UserB tooaccess a storage account for a limited time with certain permissions:</span></span>

1. <span data-ttu-id="a4200-197">UserA 會產生 SAS （組成 hello hello 儲存體帳戶的連接字串） 特定的時間週期並以 hello 所需的權限。</span><span class="sxs-lookup"><span data-stu-id="a4200-197">UserA generates an SAS (consisting of hello connection string for hello storage account) for a specific time period and with hello desired permissions.</span></span>

2. <span data-ttu-id="a4200-198">UserA 共用 hello 與 hello 人 (在我們的範例使用者 b)，並想要存取 toohello 儲存體帳戶的 SAS。</span><span class="sxs-lookup"><span data-stu-id="a4200-198">UserA shares hello SAS with hello person (UserB, in our example) who wants access toohello storage account.</span></span>  

3. <span data-ttu-id="a4200-199">使用者 b 會使用儲存體總管 （預覽） tooattach toohello 帳戶屬於 tooUserA 使用 hello 提供 SAS。</span><span class="sxs-lookup"><span data-stu-id="a4200-199">UserB uses Storage Explorer (Preview) tooattach toohello account that belongs tooUserA by using hello supplied SAS.</span></span>

### <a name="get-an-sas-for-hello-account-you-want-tooshare"></a><span data-ttu-id="a4200-200">您想要 tooshare hello 帳戶取得 SAS</span><span class="sxs-lookup"><span data-stu-id="a4200-200">Get an SAS for hello account you want tooshare</span></span>
1. <span data-ttu-id="a4200-201">在儲存體總管 （預覽） 中，以滑鼠右鍵按一下 hello 儲存體帳戶共用，然後再選取您想**取得共用存取簽章**。</span><span class="sxs-lookup"><span data-stu-id="a4200-201">In Storage Explorer (Preview), right-click hello storage account you want share, and then select **Get Shared Access Signature**.</span></span>

    ![取得 SAS 內容功能表選項][13]

2. <span data-ttu-id="a4200-203">在 hello**共用存取簽章**對話方塊方塊中，指定 hello 時間範圍，以及您想要用於 hello 帳戶，然後選取的權限**建立**。</span><span class="sxs-lookup"><span data-stu-id="a4200-203">In hello **Shared Access Signature** dialog box, specify hello time frame and permissions that you want for hello account, and then select **Create**.</span></span>

    <span data-ttu-id="a4200-204">![取得 SAS 對話方塊][14]</span><span class="sxs-lookup"><span data-stu-id="a4200-204">![Get SAS dialog box][14]</span></span>  
    <span data-ttu-id="a4200-205">hello**共用存取簽章** 對話方塊隨即開啟並顯示 hello SAS。</span><span class="sxs-lookup"><span data-stu-id="a4200-205">hello **Shared Access Signature** dialog box opens and displays hello SAS.</span></span>

3. <span data-ttu-id="a4200-206">下一步 toohello**連接字串**，選取**複製**toocopy 它 toohello 剪貼簿，然後選取**關閉**。</span><span class="sxs-lookup"><span data-stu-id="a4200-206">Next toohello **Connection String**, select **Copy** toocopy it toohello clipboard, and then select **Close**.</span></span>

### <a name="attach-toohello-shared-account-by-using-hello-sas"></a><span data-ttu-id="a4200-207">使用 hello SAS 附加 toohello 共用帳戶</span><span class="sxs-lookup"><span data-stu-id="a4200-207">Attach toohello shared account by using hello SAS</span></span>
1. <span data-ttu-id="a4200-208">在儲存體總管 （預覽） 中，選取**tooAzure 存放裝置連線**。</span><span class="sxs-lookup"><span data-stu-id="a4200-208">In Storage Explorer (Preview), select **Connect tooAzure storage**.</span></span>

    ![連接 tooAzure 儲存體選項][23]

2. <span data-ttu-id="a4200-210">在 hello**連接 tooAzure 儲存體**對話方塊中，指定 hello 連接字串，然後再選取**下一步**。</span><span class="sxs-lookup"><span data-stu-id="a4200-210">In hello **Connect tooAzure Storage** dialog box, specify hello connection string, and then select **Next**.</span></span>

    ![連接 tooAzure 儲存對話方塊][24]

3. <span data-ttu-id="a4200-212">在 hello**連接摘要**對話方塊方塊中，確認 hello 資訊。</span><span class="sxs-lookup"><span data-stu-id="a4200-212">In hello **Connection Summary** dialog box, verify hello information.</span></span> <span data-ttu-id="a4200-213">toomake 變更選取**回**，然後輸入您想要的 hello 設定。</span><span class="sxs-lookup"><span data-stu-id="a4200-213">toomake changes, select **Back**, and then enter hello settings you want.</span></span> 

4. <span data-ttu-id="a4200-214">選取 [ **連接**]。</span><span class="sxs-lookup"><span data-stu-id="a4200-214">Select **Connect**.</span></span>

5. <span data-ttu-id="a4200-215">附加之後，會顯示 hello 儲存體帳戶**(SAS)**附加 toohello 您提供的帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="a4200-215">After it is attached, hello storage account is displayed with **(SAS)** appended toohello account name that you supplied.</span></span>

    ![使用 SAS 附加的 tooan 帳戶的結果][17]

## <a name="attach-a-service-by-using-an-sas"></a><span data-ttu-id="a4200-217">使用 SAS 連結服務</span><span class="sxs-lookup"><span data-stu-id="a4200-217">Attach a service by using an SAS</span></span>
<span data-ttu-id="a4200-218">hello < 使用 SAS 附加儲存體帳戶 > 一節將說明如何為 Azure 訂用帳戶系統管理員可以授與的暫時存取 tooa 儲存體帳戶產生及共用 SAS hello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="a4200-218">hello "Attach a storage account by using an SAS" section explains how an Azure subscription admin can grant temporary access tooa storage account by generating and sharing an SAS for hello storage account.</span></span> <span data-ttu-id="a4200-219">同樣地，可以針對儲存體帳戶內的特定服務 (Blob 容器、佇列或資料表) 產生 SAS。</span><span class="sxs-lookup"><span data-stu-id="a4200-219">Similarly, an SAS can be generated for a specific service (blob container, queue, or table) within a storage account.</span></span>  

### <a name="generate-an-sas-for-hello-service-that-you-want-tooshare"></a><span data-ttu-id="a4200-220">產生 SAS，使您想 tooshare hello 服務</span><span class="sxs-lookup"><span data-stu-id="a4200-220">Generate an SAS for hello service that you want tooshare</span></span>
<span data-ttu-id="a4200-221">在此情況下，服務可以是 Blob 容器、佇列或資料表。</span><span class="sxs-lookup"><span data-stu-id="a4200-221">In this context, a service can be a blob container, queue, or table.</span></span> <span data-ttu-id="a4200-222">toogenerate hello SAS 列出的服務，請參閱：</span><span class="sxs-lookup"><span data-stu-id="a4200-222">toogenerate hello SAS for a listed service, see:</span></span>

* [<span data-ttu-id="a4200-223">取得 blob 容器的 SAS hello</span><span class="sxs-lookup"><span data-stu-id="a4200-223">Get hello SAS for a blob container</span></span>](vs-azure-tools-storage-explorer-blobs.md#get-the-sas-for-a-blob-container)
* <span data-ttu-id="a4200-224">取得檔案共用中的 hello SAS:*即將推出*</span><span class="sxs-lookup"><span data-stu-id="a4200-224">Get hello SAS for a file share: *Coming soon*</span></span>
* <span data-ttu-id="a4200-225">取得佇列中的 hello SAS:*即將推出*</span><span class="sxs-lookup"><span data-stu-id="a4200-225">Get hello SAS for a queue: *Coming soon*</span></span>
* <span data-ttu-id="a4200-226">取得資料表中的 hello SAS:*即將推出*</span><span class="sxs-lookup"><span data-stu-id="a4200-226">Get hello SAS for a table: *Coming soon*</span></span>

### <a name="attach-toohello-shared-account-service-by-using-hello-sas"></a><span data-ttu-id="a4200-227">附加服務，方法是使用 hello SAS toohello 共用帳戶</span><span class="sxs-lookup"><span data-stu-id="a4200-227">Attach toohello shared account service by using hello SAS</span></span>
1. <span data-ttu-id="a4200-228">在儲存體總管 （預覽） 中，選取**tooAzure 存放裝置連線**。</span><span class="sxs-lookup"><span data-stu-id="a4200-228">In Storage Explorer (Preview), select **Connect tooAzure storage**.</span></span>

    ![連接 tooAzure 儲存體選項][23]

2. <span data-ttu-id="a4200-230">在 hello**連接 tooAzure 儲存體**對話方塊中，指定 hello SAS URI，然後再選取**下一步**。</span><span class="sxs-lookup"><span data-stu-id="a4200-230">In hello **Connect tooAzure Storage** dialog box, specify hello SAS URI, and then select **Next**.</span></span>

    ![連接 tooAzure 儲存對話方塊][24]

3. <span data-ttu-id="a4200-232">在 hello**連接摘要**對話方塊方塊中，確認 hello 資訊。</span><span class="sxs-lookup"><span data-stu-id="a4200-232">In hello **Connection Summary** dialog box, verify hello information.</span></span> <span data-ttu-id="a4200-233">toomake 變更選取**回**，然後輸入您想要的 hello 設定。</span><span class="sxs-lookup"><span data-stu-id="a4200-233">toomake changes, select **Back**, and then enter hello settings you want.</span></span> 

4. <span data-ttu-id="a4200-234">選取 [ **連接**]。</span><span class="sxs-lookup"><span data-stu-id="a4200-234">Select **Connect**.</span></span>

5. <span data-ttu-id="a4200-235">附加之後，hello 新附加的服務下顯示 hello **(服務 SAS)**節點。</span><span class="sxs-lookup"><span data-stu-id="a4200-235">After it is attached, hello newly attached service is displayed under hello **(Service SAS)** node.</span></span>

    ![使用 SAS 附加 tooa 共用服務的結果][20]

## <a name="search-for-storage-accounts"></a><span data-ttu-id="a4200-237">搜尋儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="a4200-237">Search for storage accounts</span></span>
<span data-ttu-id="a4200-238">如果您有一長串的儲存體帳戶時，快速 toolocate 特定儲存體帳戶是在 hello hello 左窗格頂端 toouse hello 搜尋 方塊。</span><span class="sxs-lookup"><span data-stu-id="a4200-238">If you have a long list of storage accounts, a quick way toolocate a particular storage account is toouse hello search box at hello top of hello left pane.</span></span>

<span data-ttu-id="a4200-239">當您輸入 hello [搜尋] 方塊中，hello 左窗格中會顯示符合您輸入向上 toothat 點 hello 搜尋值的 hello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="a4200-239">As you type in hello search box, hello left pane displays hello storage accounts that match hello search value you've entered up toothat point.</span></span> <span data-ttu-id="a4200-240">例如，搜尋所有儲存體帳戶名稱包含**tarcher** hello 下列螢幕擷取畫面所示：</span><span class="sxs-lookup"><span data-stu-id="a4200-240">For example, a search for all storage accounts whose name contains **tarcher** is shown in hello following screenshot:</span></span>

![儲存體帳戶搜尋][11]

## <a name="next-steps"></a><span data-ttu-id="a4200-242">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a4200-242">Next steps</span></span>
* [<span data-ttu-id="a4200-243">使用儲存體總管 (預覽) 來管理 Azure Blob 儲存體資源</span><span class="sxs-lookup"><span data-stu-id="a4200-243">Manage Azure Blob Storage resources with Storage Explorer (Preview)</span></span>](vs-azure-tools-storage-explorer-blobs.md)

[0]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/settings-icon.png
[1]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/add-account-link.png
[3]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/subscriptions-list.png
[4]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/storage-accounts-list.png
[5]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/access-keys.png
[6]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/access-keys-copy.png
[8]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/attach-external-storage-dlg.png
[9]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/external-storage-account.png
[10]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/detach-external-storage.png
[11]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/storage-account-search.png
[12]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/detach-external-storage-confirmation.png
[13]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/get-sas-context-menu.png
[14]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/get-sas-dlg1.png
[15]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/mase.png
[17]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/attach-account-using-sas-finished.png
[20]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/attach-service-using-sas-finished.png
[21]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/local-storage-drop-down.png
[22]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/download-storage-emulator.png
[23]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/connect-to-azure-storage-icon.png
[24]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/connect-to-azure-storage-next.png
[25]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/add-certificate-azure-stack.png
[26]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/export-root-cert-azure-stack.png
[27]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/import-azure-stack-cert-storage-explorer.png
[28]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/select-target-azure-stack.png
[29]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/add-azure-stack-account.png
[30]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/select-accounts-azure-stack.png
[31]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/azure-stack-storage-account-list.png
