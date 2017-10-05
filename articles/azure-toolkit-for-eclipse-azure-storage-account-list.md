---
title: "Azure 儲存體帳戶清單"
description: "使用 Azure Toolkit for Eclipse 來管理您的儲存體帳戶設定"
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
ms.openlocfilehash: f859efa389d3fe0b4b7b16255d57f1aa13123319
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-storage-account-list"></a><span data-ttu-id="61be4-103">Azure 儲存體帳戶清單</span><span class="sxs-lookup"><span data-stu-id="61be4-103">Azure Storage Account List</span></span>
<span data-ttu-id="61be4-104">Azure 儲存體帳戶可讓下載位置用於您的 JDK、應用程式伺服器和任意元件，以及在使用快取時用於儲存狀態。</span><span class="sxs-lookup"><span data-stu-id="61be4-104">Azure storage accounts enable download locations to be used for your JDK, application server, and arbitrary components, as well as for storing state when using caching.</span></span> <span data-ttu-id="61be4-105">Eclipse 維護一份已知儲存體帳戶清單，可供 Eclipse 工作區中的專案使用。</span><span class="sxs-lookup"><span data-stu-id="61be4-105">Eclipse maintains a list of known storage accounts that are available to your projects in your Eclipse workspace.</span></span> <span data-ttu-id="61be4-106">若要在 Eclipse 內開啟用來管理該清單的 [儲存體帳戶] 對話方塊，請依序按一下 [視窗] 和 [喜好設定]，展開 [Azure]，然後按一下 [儲存體帳戶]。</span><span class="sxs-lookup"><span data-stu-id="61be4-106">To open the **Storage Accounts** dialog, which is used to manage that list, within Eclipse, click **Window**, click **Preferences**, expand **Azure**, and then click **Storage Accounts**.</span></span>

<span data-ttu-id="61be4-107">下圖顯示 [儲存體帳戶]  對話方塊。</span><span class="sxs-lookup"><span data-stu-id="61be4-107">The following shows the **Storage Accounts** dialog.</span></span>

![][ic719496]

<span data-ttu-id="61be4-108">您也可以在使用儲存體帳戶的下列對話方塊上，從 [帳戶]  連結開啟這個對話方塊：</span><span class="sxs-lookup"><span data-stu-id="61be4-108">This dialog can also be opened from an **Accounts** link on dialog boxes that use storage accounts, such as the following:</span></span>

* <span data-ttu-id="61be4-109">[伺服器組態] 對話方塊的 [JDK] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="61be4-109">The **JDK** tab of the **Server Configuration** dialog.</span></span>
* <span data-ttu-id="61be4-110">[伺服器組態] 對話方塊的 [伺服器] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="61be4-110">The **Server** tab of the **Server Configuration** dialog.</span></span>
* <span data-ttu-id="61be4-111">[加入元件]  對話方塊。</span><span class="sxs-lookup"><span data-stu-id="61be4-111">The **Add Component** dialog.</span></span>
* <span data-ttu-id="61be4-112">[快取]  屬性對話方塊。</span><span class="sxs-lookup"><span data-stu-id="61be4-112">The **Caching** properties dialog.</span></span>

## <a name="to-import-your-storage-accounts-using-a-publish-settings-file"></a><span data-ttu-id="61be4-113">使用發行設定檔匯入您的儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="61be4-113">To import your storage accounts using a publish settings file</span></span>
1. <span data-ttu-id="61be4-114">在 [儲存體帳戶] 對話方塊中，按一下 [從發佈設定檔匯入]。</span><span class="sxs-lookup"><span data-stu-id="61be4-114">Within the **Storage Accounts** dialog, click **Import from PUBLISH-SETTINGS file**.</span></span>

2. <span data-ttu-id="61be4-115">(如果您已將發行設定檔儲存至本機電腦，則略過這個步驟)。在 [匯入訂用帳戶資訊] 對話方塊中，按一下 [下載發佈設定檔]。</span><span class="sxs-lookup"><span data-stu-id="61be4-115">(Skip this step if you have already saved a publish settings file to your local machine.) In the **Import Subscription Information** dialog, click **Download PUBLISH-SETTINGS File**.</span></span> <span data-ttu-id="61be4-116">如果您尚未登入 Azure 帳戶，系統會提示您登入。</span><span class="sxs-lookup"><span data-stu-id="61be4-116">If you are not yet logged into your Azure account, you will be prompted to log in.</span></span> <span data-ttu-id="61be4-117">然後會提示您儲存 Azure 發行設定檔</span><span class="sxs-lookup"><span data-stu-id="61be4-117">Then you'll be prompted to save an Azure publish settings file.</span></span> <span data-ttu-id="61be4-118">(您可以忽略登入頁面上所顯示的產生指示，這是由 Azure 入口網站提供給 Visual Studio 使用者的指示)。請將其儲存至本機電腦。</span><span class="sxs-lookup"><span data-stu-id="61be4-118">(You can ignore the resulting instructions shown on the logon pages - they are provided by the Azure portal and are intended for Visual Studio users.) Save it to your local machine.</span></span>

3. <span data-ttu-id="61be4-119">同樣在 [匯入訂用帳戶資訊] 對話方塊中，按一下 [瀏覽] 按鈕，選取您先前在本機儲存的發佈設定檔，然後按一下 [開啟]。</span><span class="sxs-lookup"><span data-stu-id="61be4-119">Still in the **Import Subscription Information** dialog, click the **Browse** button, select the publish settings file that you saved locally previously, and then click **Open**.</span></span>

4. <span data-ttu-id="61be4-120">按一下 [確定] 關閉 [匯入訂用帳戶資訊] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="61be4-120">Click **OK** to close the **Import Subscription Information** dialog.</span></span>

## <a name="to-create-a-new-storage-account"></a><span data-ttu-id="61be4-121">建立新的儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="61be4-121">To create a new storage account</span></span>
1. <span data-ttu-id="61be4-122">在 [儲存體帳戶] 對話方塊中，按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="61be4-122">Within the **Storage Accounts** dialog, click **Add**.</span></span>

2. <span data-ttu-id="61be4-123">在 [新增儲存體帳戶] 對話方塊中，按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="61be4-123">Within the **Add Storage Account** dialog, click **New**.</span></span>

3. <span data-ttu-id="61be4-124">在 [新增儲存體帳戶]  對話方塊中，指定下列值：</span><span class="sxs-lookup"><span data-stu-id="61be4-124">Within the **New Storage Account** dialog, specify values for the following:</span></span>

   * <span data-ttu-id="61be4-125">儲存體帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="61be4-125">Storage account name.</span></span>

   * <span data-ttu-id="61be4-126">儲存體帳戶的位置。</span><span class="sxs-lookup"><span data-stu-id="61be4-126">Location of the storage account.</span></span>

   * <span data-ttu-id="61be4-127">儲存體帳戶的描述。</span><span class="sxs-lookup"><span data-stu-id="61be4-127">Description of the storage account.</span></span>

   * <span data-ttu-id="61be4-128">儲存體帳戶所屬的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="61be4-128">The subscription to which the storage account belongs.</span></span>

4. <span data-ttu-id="61be4-129">按一下 [確定] 關閉 [新增儲存體帳戶] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="61be4-129">Click **OK** to close the **New Storage Account** dialog.</span></span>

<span data-ttu-id="61be4-130">建立儲存體帳戶可能需要幾分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="61be4-130">It may take several minutes for your storage account to be created.</span></span> <span data-ttu-id="61be4-131">建立後，請按一下 [確定] 關閉 [新增儲存體帳戶] 對話方塊，新的儲存體帳戶會新增至可用的儲存體帳戶清單。</span><span class="sxs-lookup"><span data-stu-id="61be4-131">After it is created, click **OK** to close the **Add Storage Account** dialog, and your new storage account will be added to the list of available storage accounts.</span></span>

## <a name="to-add-an-existing-storage-account-to-the-list"></a><span data-ttu-id="61be4-132">將現有的儲存體帳戶加入清單中</span><span class="sxs-lookup"><span data-stu-id="61be4-132">To add an existing storage account to the list</span></span>
1. <span data-ttu-id="61be4-133">如果您還沒有 Azure 儲存體帳戶，請遵循上一節＜建立新的儲存體帳戶＞  中所列的步驟，建立一個帳戶。</span><span class="sxs-lookup"><span data-stu-id="61be4-133">If you do not already have a Azure storage account, create one by following the steps listed in the **To create a new storage account section** above.</span></span> <span data-ttu-id="61be4-134">(您也可以在 [Azure 管理入口網站][Azure Management Portal]中建立新的儲存體帳戶)。</span><span class="sxs-lookup"><span data-stu-id="61be4-134">(Alternatively, you can create a new storage account at the [Azure Management Portal][Azure Management Portal].)</span></span>

2. <span data-ttu-id="61be4-135">在 [儲存體帳戶] 對話方塊中，按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="61be4-135">Within the **Storage Accounts** dialog, click **Add**.</span></span>

3. <span data-ttu-id="61be4-136">在 [新增儲存體帳戶] 對話方塊中，輸入 [名稱] 和 [存取金鑰] 的值。</span><span class="sxs-lookup"><span data-stu-id="61be4-136">Within the **Add Storage Account** dialog, enter values for **Name** and **Access Key**.</span></span> <span data-ttu-id="61be4-137">這必須是現有 Azure 儲存體帳戶的帳戶名稱和存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="61be4-137">The account name and access key must be for an existing Azure storage account.</span></span> <span data-ttu-id="61be4-138">請使用 [Azure 管理入口網站][Azure Management Portal]的 [儲存體] 區段，來檢視您的儲存體帳戶名稱和金鑰。</span><span class="sxs-lookup"><span data-stu-id="61be4-138">Use the **Storage** section of the [Azure Management Portal][Azure Management Portal] to view your storage account names and keys.</span></span> <span data-ttu-id="61be4-139">您的 [加入儲存體帳戶]  對話方塊將會類似如下。</span><span class="sxs-lookup"><span data-stu-id="61be4-139">Your **Add Storage Account** dialog will look similar to the following.</span></span>
   
   ![][ic719497]

4. <span data-ttu-id="61be4-140">按一下 [確定] 關閉 [新增儲存體帳戶] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="61be4-140">Click **OK** to close the **Add Storage Account** dialog.</span></span>

## <a name="to-modify-a-storage-account-to-use-a-new-access-key"></a><span data-ttu-id="61be4-141">修改儲存體帳戶以使用新的存取金鑰</span><span class="sxs-lookup"><span data-stu-id="61be4-141">To modify a storage account to use a new access key</span></span>
1. <span data-ttu-id="61be4-142">在 [儲存體帳戶] 對話方塊中，按一下您要編輯的儲存體帳戶，然後按一下 [編輯]。</span><span class="sxs-lookup"><span data-stu-id="61be4-142">Within the **Storage Accounts** dialog, click the storage account that you want to edit and then click **Edit**.</span></span>

2. <span data-ttu-id="61be4-143">在 [編輯儲存體帳戶存取金鑰] 對話方塊中，修改 [存取金鑰] 值。</span><span class="sxs-lookup"><span data-stu-id="61be4-143">Within the **Edit Storage Account Access Key** dialog, modify the **Access Key** value.</span></span>

3. <span data-ttu-id="61be4-144">按一下 [確定] 關閉 [編輯儲存體帳戶存取金鑰] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="61be4-144">Click **OK** to close the **Edit Storage Account Access Key** dialog.</span></span>

## <a name="to-remove-a-storage-account-from-the-list-maintained-in-eclipse"></a><span data-ttu-id="61be4-145">從 Eclipse 所維護的清單中移除儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="61be4-145">To remove a storage account from the list maintained in Eclipse</span></span>
1. <span data-ttu-id="61be4-146">在 [儲存體帳戶] 對話方塊中，按一下您要編輯的儲存體帳戶，然後按一下 [移除]。</span><span class="sxs-lookup"><span data-stu-id="61be4-146">Within the **Storage Accounts** dialog, click the storage account that you want to edit and then click **Remove**.</span></span>

2. <span data-ttu-id="61be4-147">出現提示時，按一下 [確定]  以移除儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="61be4-147">Click **OK** when prompted to remove the storage account.</span></span>

> [!NOTE]
> <span data-ttu-id="61be4-148">透過 [儲存體帳戶] 對話方塊移除儲存體帳戶，只會將其從可在 Eclipse 中檢視的儲存體帳戶清單中移除，</span><span class="sxs-lookup"><span data-stu-id="61be4-148">Removing the storage account through the **Storage Accounts** dialog only removes it from the list of storage accounts viewable within Eclipse.</span></span> <span data-ttu-id="61be4-149">而不會從您的 Azure 訂用帳戶中移除此儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="61be4-149">It does not remove the storage account from your Azure subscription.</span></span> <span data-ttu-id="61be4-150">此外，當 Eclipse 重新載入您訂用帳戶的詳細資料之後，該儲存體帳戶可能會再次出現於清單中。</span><span class="sxs-lookup"><span data-stu-id="61be4-150">Additionally, the storage account could appear again in your list after Eclipse reloads the details of your subscription.</span></span>
> 
> 

## <a name="see-also"></a><span data-ttu-id="61be4-151">另請參閱</span><span class="sxs-lookup"><span data-stu-id="61be4-151">See Also</span></span>
<span data-ttu-id="61be4-152">[適用於 Eclipse 的 Azure 工具組][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="61be4-152">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="61be4-153">[安裝適用於 Eclipse 的 Azure 工具組][Installing the Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="61be4-153">[Installing the Azure Toolkit for Eclipse][Installing the Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="61be4-154">[在 Eclipse 中為 Azure 建立 Hello World 應用程式][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="61be4-154">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="61be4-155">如需有關如何搭配使用 Azure 與 Java 的詳細資訊，請參閱 [Azure Java 開發人員中心][Azure Java Developer Center]。</span><span class="sxs-lookup"><span data-stu-id="61be4-155">For more information about using Azure with Java, see the [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546
[What's New in the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699552

<!-- IMG List -->

[ic719496]: ./media/azure-toolkit-for-eclipse-azure-storage-account-list/ic719496.png
[ic719497]: ./media/azure-toolkit-for-eclipse-azure-storage-account-list/ic719497.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/dn205108.aspx -->
