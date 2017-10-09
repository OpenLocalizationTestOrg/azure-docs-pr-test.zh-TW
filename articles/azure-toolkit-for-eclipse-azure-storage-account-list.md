---
title: "aaaAzure 儲存體帳戶清單"
description: "管理您使用 hello Azure Toolkit for Eclipse 的儲存體帳戶設定"
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: bbacfcd8-dbf5-4265-a930-59f508de5325
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 35e25881ca95ae4050a26283e4726d9549b37f46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-account-list"></a><span data-ttu-id="1633b-103">Azure 儲存體帳戶清單</span><span class="sxs-lookup"><span data-stu-id="1633b-103">Azure Storage Account List</span></span>
<span data-ttu-id="1633b-104">Azure 儲存體帳戶可讓下載位置 toobe 用於您的 JDK、 應用程式伺服器和任意元件，以及使用快取時儲存狀態。</span><span class="sxs-lookup"><span data-stu-id="1633b-104">Azure storage accounts enable download locations toobe used for your JDK, application server, and arbitrary components, as well as for storing state when using caching.</span></span> <span data-ttu-id="1633b-105">Eclipse 會維護一份您 Eclipse 工作區中的可用 tooyour 專案已知的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="1633b-105">Eclipse maintains a list of known storage accounts that are available tooyour projects in your Eclipse workspace.</span></span> <span data-ttu-id="1633b-106">tooopen hello**儲存體帳戶**對話方塊中，也就是使用的 toomanage 的清單，在 Eclipse 中，按一下**視窗**，按一下 **喜好設定**，依序展開**Azure**，然後按一下**儲存體帳戶**。</span><span class="sxs-lookup"><span data-stu-id="1633b-106">tooopen hello **Storage Accounts** dialog, which is used toomanage that list, within Eclipse, click **Window**, click **Preferences**, expand **Azure**, and then click **Storage Accounts**.</span></span>

<span data-ttu-id="1633b-107">hello 下列範例示範 hello**儲存體帳戶**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="1633b-107">hello following shows hello **Storage Accounts** dialog.</span></span>

![][ic719496]

<span data-ttu-id="1633b-108">此對話方塊也可以從開啟**帳戶**連結上使用儲存體帳戶，例如 hello 下列對話方塊：</span><span class="sxs-lookup"><span data-stu-id="1633b-108">This dialog can also be opened from an **Accounts** link on dialog boxes that use storage accounts, such as hello following:</span></span>

* <span data-ttu-id="1633b-109">hello **JDK**  索引標籤的 hello**伺服器組態**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="1633b-109">hello **JDK** tab of hello **Server Configuration** dialog.</span></span>
* <span data-ttu-id="1633b-110">hello**伺服器** 索引標籤的 hello**伺服器組態**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="1633b-110">hello **Server** tab of hello **Server Configuration** dialog.</span></span>
* <span data-ttu-id="1633b-111">hello**加入元件**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="1633b-111">hello **Add Component** dialog.</span></span>
* <span data-ttu-id="1633b-112">hello**快取**屬性 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="1633b-112">hello **Caching** properties dialog.</span></span>

## <a name="tooimport-your-storage-accounts-using-a-publish-settings-file"></a><span data-ttu-id="1633b-113">您的儲存體帳戶使用 tooimport 的發行設定檔</span><span class="sxs-lookup"><span data-stu-id="1633b-113">tooimport your storage accounts using a publish settings file</span></span>
1. <span data-ttu-id="1633b-114">在 [hello**儲存體帳戶**] 對話方塊中，按一下**從 PUBLISH-SETTINGS 檔案匯入**。</span><span class="sxs-lookup"><span data-stu-id="1633b-114">Within hello **Storage Accounts** dialog, click **Import from PUBLISH-SETTINGS file**.</span></span>

2. <span data-ttu-id="1633b-115">（如果略過此步驟中已儲存發行設定檔案 tooyour 本機電腦。）在 hello**匯入訂用帳戶資訊** 對話方塊中，按一下 **下載發行設定檔案**。</span><span class="sxs-lookup"><span data-stu-id="1633b-115">(Skip this step if you have already saved a publish settings file tooyour local machine.) In hello **Import Subscription Information** dialog, click **Download PUBLISH-SETTINGS File**.</span></span> <span data-ttu-id="1633b-116">如果尚未登入您的 Azure 帳戶，您將會提示的 toolog 中。</span><span class="sxs-lookup"><span data-stu-id="1633b-116">If you are not yet logged into your Azure account, you will be prompted toolog in.</span></span> <span data-ttu-id="1633b-117">然後系統會提示您 toosave Azure 發行設定檔。</span><span class="sxs-lookup"><span data-stu-id="1633b-117">Then you'll be prompted toosave an Azure publish settings file.</span></span> <span data-ttu-id="1633b-118">（您可以忽略 hello hello 登入頁面-上顯示的結果指示他們所提供的 hello Azure 入口網站和適用於 Visual Studio 使用者。）將它儲存 tooyour 本機電腦。</span><span class="sxs-lookup"><span data-stu-id="1633b-118">(You can ignore hello resulting instructions shown on hello logon pages - they are provided by hello Azure portal and are intended for Visual Studio users.) Save it tooyour local machine.</span></span>

3. <span data-ttu-id="1633b-119">仍在 hello**匯入訂用帳戶資訊** 對話方塊中，按一下 hello**瀏覽**按鈕、 選取 hello 發行設定檔，您先前儲存在本機，，然後按一下**開啟**.</span><span class="sxs-lookup"><span data-stu-id="1633b-119">Still in hello **Import Subscription Information** dialog, click hello **Browse** button, select hello publish settings file that you saved locally previously, and then click **Open**.</span></span>

4. <span data-ttu-id="1633b-120">按一下**確定**tooclose hello**匯入訂用帳戶資訊**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="1633b-120">Click **OK** tooclose hello **Import Subscription Information** dialog.</span></span>

## <a name="toocreate-a-new-storage-account"></a><span data-ttu-id="1633b-121">toocreate 新的儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="1633b-121">toocreate a new storage account</span></span>
1. <span data-ttu-id="1633b-122">在 [hello**儲存體帳戶**] 對話方塊中，按一下**新增**。</span><span class="sxs-lookup"><span data-stu-id="1633b-122">Within hello **Storage Accounts** dialog, click **Add**.</span></span>

2. <span data-ttu-id="1633b-123">在 [hello**新增儲存體帳戶**] 對話方塊中，按一下**新增**。</span><span class="sxs-lookup"><span data-stu-id="1633b-123">Within hello **Add Storage Account** dialog, click **New**.</span></span>

3. <span data-ttu-id="1633b-124">Hello 內**新儲存體帳戶** 對話方塊中，指定的 hello 下列值：</span><span class="sxs-lookup"><span data-stu-id="1633b-124">Within hello **New Storage Account** dialog, specify values for hello following:</span></span>

   * <span data-ttu-id="1633b-125">儲存體帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="1633b-125">Storage account name.</span></span>

   * <span data-ttu-id="1633b-126">Hello 儲存體帳戶的位置。</span><span class="sxs-lookup"><span data-stu-id="1633b-126">Location of hello storage account.</span></span>

   * <span data-ttu-id="1633b-127">Hello 儲存體帳戶的描述。</span><span class="sxs-lookup"><span data-stu-id="1633b-127">Description of hello storage account.</span></span>

   * <span data-ttu-id="1633b-128">所屬 hello 訂用帳戶 toowhich hello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="1633b-128">hello subscription toowhich hello storage account belongs.</span></span>

4. <span data-ttu-id="1633b-129">按一下**確定**tooclose hello**新儲存體帳戶**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="1633b-129">Click **OK** tooclose hello **New Storage Account** dialog.</span></span>

<span data-ttu-id="1633b-130">可能需要您建立的儲存體帳戶 toobe 幾分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="1633b-130">It may take several minutes for your storage account toobe created.</span></span> <span data-ttu-id="1633b-131">建立之後，請按一下**確定**tooclose hello**新增儲存體帳戶** 對話方塊中，新的儲存體帳戶將會新增 toohello 可用的儲存體帳戶清單。</span><span class="sxs-lookup"><span data-stu-id="1633b-131">After it is created, click **OK** tooclose hello **Add Storage Account** dialog, and your new storage account will be added toohello list of available storage accounts.</span></span>

## <a name="tooadd-an-existing-storage-account-toohello-list"></a><span data-ttu-id="1633b-132">tooadd 現有的儲存體帳戶 toohello 清單</span><span class="sxs-lookup"><span data-stu-id="1633b-132">tooadd an existing storage account toohello list</span></span>
1. <span data-ttu-id="1633b-133">如果您還沒有 Azure 儲存體帳戶，來建立 hello 步驟中列出 hello **toocreate 新的儲存體帳戶區段**上方。</span><span class="sxs-lookup"><span data-stu-id="1633b-133">If you do not already have a Azure storage account, create one by following hello steps listed in hello **toocreate a new storage account section** above.</span></span> <span data-ttu-id="1633b-134">(或者，您可以建立新的儲存體帳戶在 hello [Azure 管理入口網站][Azure Management Portal]。)</span><span class="sxs-lookup"><span data-stu-id="1633b-134">(Alternatively, you can create a new storage account at hello [Azure Management Portal][Azure Management Portal].)</span></span>

2. <span data-ttu-id="1633b-135">在 [hello**儲存體帳戶**] 對話方塊中，按一下**新增**。</span><span class="sxs-lookup"><span data-stu-id="1633b-135">Within hello **Storage Accounts** dialog, click **Add**.</span></span>

3. <span data-ttu-id="1633b-136">Hello 內**新增儲存體帳戶** 對話方塊中，輸入的值**名稱**和**便捷鍵**。</span><span class="sxs-lookup"><span data-stu-id="1633b-136">Within hello **Add Storage Account** dialog, enter values for **Name** and **Access Key**.</span></span> <span data-ttu-id="1633b-137">hello 帳戶名稱和存取金鑰必須是現有的 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="1633b-137">hello account name and access key must be for an existing Azure storage account.</span></span> <span data-ttu-id="1633b-138">使用 hello**儲存體**區段 hello [Azure 管理入口網站][ Azure Management Portal] tooview 儲存體帳戶名稱和金鑰。</span><span class="sxs-lookup"><span data-stu-id="1633b-138">Use hello **Storage** section of hello [Azure Management Portal][Azure Management Portal] tooview your storage account names and keys.</span></span> <span data-ttu-id="1633b-139">您**新增儲存體帳戶**對話方塊看起來類似 toohello 下列。</span><span class="sxs-lookup"><span data-stu-id="1633b-139">Your **Add Storage Account** dialog will look similar toohello following.</span></span>
   
   ![][ic719497]

4. <span data-ttu-id="1633b-140">按一下**確定**tooclose hello**新增儲存體帳戶**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="1633b-140">Click **OK** tooclose hello **Add Storage Account** dialog.</span></span>

## <a name="toomodify-a-storage-account-toouse-a-new-access-key"></a><span data-ttu-id="1633b-141">新的存取金鑰的儲存體帳戶 toouse toomodify</span><span class="sxs-lookup"><span data-stu-id="1633b-141">toomodify a storage account toouse a new access key</span></span>
1. <span data-ttu-id="1633b-142">在 [hello**儲存體帳戶**] 對話方塊中，按一下您想 tooedit，然後按一下 hello 儲存體帳戶**編輯**。</span><span class="sxs-lookup"><span data-stu-id="1633b-142">Within hello **Storage Accounts** dialog, click hello storage account that you want tooedit and then click **Edit**.</span></span>

2. <span data-ttu-id="1633b-143">在 [hello**編輯儲存體帳戶存取金鑰**] 對話方塊中，修改 hello**便捷鍵**值。</span><span class="sxs-lookup"><span data-stu-id="1633b-143">Within hello **Edit Storage Account Access Key** dialog, modify hello **Access Key** value.</span></span>

3. <span data-ttu-id="1633b-144">按一下**確定**tooclose hello**編輯儲存體帳戶存取金鑰**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="1633b-144">Click **OK** tooclose hello **Edit Storage Account Access Key** dialog.</span></span>

## <a name="tooremove-a-storage-account-from-hello-list-maintained-in-eclipse"></a><span data-ttu-id="1633b-145">在 Eclipse 中維護的 tooremove hello 清單中的儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="1633b-145">tooremove a storage account from hello list maintained in Eclipse</span></span>
1. <span data-ttu-id="1633b-146">在 [hello**儲存體帳戶**] 對話方塊中，按一下您想 tooedit，然後按一下 hello 儲存體帳戶**移除**。</span><span class="sxs-lookup"><span data-stu-id="1633b-146">Within hello **Storage Accounts** dialog, click hello storage account that you want tooedit and then click **Remove**.</span></span>

2. <span data-ttu-id="1633b-147">按一下**確定**時提示的 tooremove hello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="1633b-147">Click **OK** when prompted tooremove hello storage account.</span></span>

> [!NOTE]
> <span data-ttu-id="1633b-148">移除 hello 儲存體帳戶，透過 hello**儲存體帳戶**對話方塊只會移除它從 hello 可在 Eclipse 內檢視的儲存體帳戶清單。</span><span class="sxs-lookup"><span data-stu-id="1633b-148">Removing hello storage account through hello **Storage Accounts** dialog only removes it from hello list of storage accounts viewable within Eclipse.</span></span> <span data-ttu-id="1633b-149">它不會從 Azure 訂用帳戶移除 hello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="1633b-149">It does not remove hello storage account from your Azure subscription.</span></span> <span data-ttu-id="1633b-150">此外，hello 儲存體帳戶可能會再次出現在清單中後 Eclipse 重新載入您訂用帳戶的 hello 詳細資料。</span><span class="sxs-lookup"><span data-stu-id="1633b-150">Additionally, hello storage account could appear again in your list after Eclipse reloads hello details of your subscription.</span></span>
> 
> 

## <a name="see-also"></a><span data-ttu-id="1633b-151">另請參閱</span><span class="sxs-lookup"><span data-stu-id="1633b-151">See Also</span></span>
<span data-ttu-id="1633b-152">[適用於 Eclipse 的 Azure 工具組][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="1633b-152">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="1633b-153">[安裝 Azure Toolkit for Eclipse hello][Installing hello Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="1633b-153">[Installing hello Azure Toolkit for Eclipse][Installing hello Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="1633b-154">[在 Eclipse 中為 Azure 建立 Hello World 應用程式][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="1633b-154">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="1633b-155">如需有關使用 Azure 與 Java 的詳細資訊，請參閱 hello [Azure Java 開發人員中心][Azure Java Developer Center]。</span><span class="sxs-lookup"><span data-stu-id="1633b-155">For more information about using Azure with Java, see hello [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546
[What's New in hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699552

<!-- IMG List -->

[ic719496]: ./media/azure-toolkit-for-eclipse-azure-storage-account-list/ic719496.png
[ic719497]: ./media/azure-toolkit-for-eclipse-azure-storage-account-list/ic719497.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/dn205108.aspx -->
