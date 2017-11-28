---
title: "aaaConnect 存放裝置總管 tooan 堆疊 Azure 訂用帳戶"
description: "深入了解如何 tooconnect 儲存體 Exporer tooan 堆疊 Azure 訂用帳戶"
services: azure-stack
documentationcenter: 
author: xiaofmao
manager: 
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 7/24/2017
ms.author: xiaofmao
ms.openlocfilehash: 8508fcf41a114ff58f57582b4a6021d8050aabe9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-storage-explorer-tooan-azure-stack-subscription"></a><span data-ttu-id="47cef-103">連接儲存體總管 tooan 堆疊 Azure 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="47cef-103">Connect Storage Explorer tooan Azure Stack subscription</span></span>

<span data-ttu-id="47cef-104">Azure 儲存體總管 （預覽） 是獨立應用程式，可讓您 tooeasily 使用在 Windows、 macOS 和 Linux 的 Azure 堆疊儲存體資料。</span><span class="sxs-lookup"><span data-stu-id="47cef-104">Azure Storage Explorer (Preview) is a standalone app that enables you tooeasily work with Azure Stack Storage data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="47cef-105">有數個工具相配 toomove 資料 tooand 從 Azure 堆疊儲存體。</span><span class="sxs-lookup"><span data-stu-id="47cef-105">There are several tools avaialble toomove data tooand from Azure Stack Storage.</span></span> <span data-ttu-id="47cef-106">如需詳細資訊，請參閱 [Azure Stack 儲存體適用的資料傳輸工具](azure-stack-storage-transfer.md)。</span><span class="sxs-lookup"><span data-stu-id="47cef-106">For more information, see [Data transfer tools for Azure Stack storage](azure-stack-storage-transfer.md).</span></span>

<span data-ttu-id="47cef-107">在本文中，您將學習如何 tooconnect tooyour 堆疊 Azure 儲存體帳戶使用儲存體總管。</span><span class="sxs-lookup"><span data-stu-id="47cef-107">In this article, you learn how tooconnect tooyour Azure Stack storage accounts using Storage Explorer.</span></span> 

<span data-ttu-id="47cef-108">如果您尚未安裝儲存體總管，請[下載](http://www.storageexplorer.com/)並安裝它。</span><span class="sxs-lookup"><span data-stu-id="47cef-108">If you haven't installed Storage Explorer yet, [download](http://www.storageexplorer.com/) and and install it.</span></span>

<span data-ttu-id="47cef-109">連接 tooyour 堆疊 Azure 訂用帳戶之後，您可以使用 hello [Azure 儲存體總管文章](../vs-azure-tools-storage-manage-with-storage-explorer.md)toowork 與您 Azure 堆疊的資料。</span><span class="sxs-lookup"><span data-stu-id="47cef-109">After you connect tooyour Azure Stack subscription, you can use hello [Azure Storage Explorer articles](../vs-azure-tools-storage-manage-with-storage-explorer.md) toowork with your Azure Stack data.</span></span> 

## <a name="prepare-an-azure-stack-subscription"></a><span data-ttu-id="47cef-110">準備 Azure Stack 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="47cef-110">Prepare an Azure Stack subscription</span></span>

<span data-ttu-id="47cef-111">您需要存取 toohello Azure 堆疊主機電腦的桌面] 或 [儲存體總管 tooaccess hello Azure 堆疊訂用帳戶的 VPN 連線。</span><span class="sxs-lookup"><span data-stu-id="47cef-111">You need access toohello Azure Stack host machine's desktop or a VPN connection for Storage Explorer tooaccess hello Azure Stack subscription.</span></span> <span data-ttu-id="47cef-112">如何 tooset 設定 VPN 連線 tooAzure 堆疊，請參閱的 toolearn[與 VPN 連線 tooAzure 堆疊](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn)。</span><span class="sxs-lookup"><span data-stu-id="47cef-112">toolearn how tooset up a VPN connection tooAzure Stack, see [Connect tooAzure Stack with VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn).</span></span>

<span data-ttu-id="47cef-113">Hello Azure 堆疊開發套件，您需要 tooexport hello Azure 堆疊授權單位的根憑證。</span><span class="sxs-lookup"><span data-stu-id="47cef-113">For hello Azure Stack Development Kit, you need tooexport hello Azure Stack authority root certificate.</span></span>

### <a name="tooexport-and-then-import-hello-azure-stack-certificate"></a><span data-ttu-id="47cef-114">tooexport 然後再匯入 hello Azure 堆疊憑證</span><span class="sxs-lookup"><span data-stu-id="47cef-114">tooexport and then import hello Azure Stack certificate</span></span>

1. <span data-ttu-id="47cef-115">開啟`mmc.exe`Azure 堆疊主機電腦上或 VPN 連線 tooAzure 堆疊的本機電腦上。</span><span class="sxs-lookup"><span data-stu-id="47cef-115">Open `mmc.exe` on an Azure Stack host machine, or a local machine with a VPN connection tooAzure Stack.</span></span> 

2. <span data-ttu-id="47cef-116">在**檔案**，選取**新增/移除嵌入式管理單元**，然後再加入**憑證**toomanage**電腦帳戶**的**本機電腦**。</span><span class="sxs-lookup"><span data-stu-id="47cef-116">In **File**, select **Add/Remove Snap-in**, and then add **Certificates** toomanage **Computer account** of **Local Computer**.</span></span>



3. <span data-ttu-id="47cef-117">在 **Console Root\Certificated (Local Computer)\Trusted Root Certification Authorities\Certificates** 之下尋找 **AzureStackSelfSignedRootCert**。</span><span class="sxs-lookup"><span data-stu-id="47cef-117">Under **Console Root\Certificated (Local Computer)\Trusted Root Certification Authorities\Certificates** find **AzureStackSelfSignedRootCert**.</span></span>

    ![透過 mmc.exe 負載 hello Azure 堆疊的根憑證][25]

4. <span data-ttu-id="47cef-119">以滑鼠右鍵按一下 hello 憑證，請選取**所有工作** > **匯出**，然後依照與 hello 指示 tooexport hello 憑證**base-64 編碼 X.509 (。CER)**。</span><span class="sxs-lookup"><span data-stu-id="47cef-119">Right-click hello certificate, select **All Tasks** > **Export**, and then follow hello instructions tooexport hello certificate with **Base-64 encoded X.509 (.CER)**.</span></span>  

    <span data-ttu-id="47cef-120">hello 匯出的憑證將用於 hello 下一個步驟。</span><span class="sxs-lookup"><span data-stu-id="47cef-120">hello exported certificate will be used in hello next step.</span></span>
5. <span data-ttu-id="47cef-121">啟動儲存體總管 （預覽），而且如果您看到 hello**連接儲存體 tooAzure**對話方塊方塊中，請將它取消。</span><span class="sxs-lookup"><span data-stu-id="47cef-121">Start Storage Explorer (Preview), and if you see hello **Connect tooAzure Storage** dialog box, cancel it.</span></span>

6. <span data-ttu-id="47cef-122">在 hello**編輯**功能表上，點太**SSL 憑證**，然後按一下**匯入憑證**。</span><span class="sxs-lookup"><span data-stu-id="47cef-122">On hello **Edit** menu, point too**SSL Certificates**, and then click **Import Certificates**.</span></span> <span data-ttu-id="47cef-123">使用 hello 檔案選擇器對話方塊方塊 toofind 和您匯出 hello 上一個步驟中的 hello 開啟憑證。</span><span class="sxs-lookup"><span data-stu-id="47cef-123">Use hello file picker dialog box toofind and open hello certificate that you exported in hello previous step.</span></span>

    <span data-ttu-id="47cef-124">匯入之後，您將會提示的 toorestart 儲存體總管。</span><span class="sxs-lookup"><span data-stu-id="47cef-124">After importing, you are prompted toorestart Storage Explorer.</span></span>

    ![Hello 憑證匯入到儲存體總管 （預覽）][27]

<span data-ttu-id="47cef-126">現在您已準備好 tooconnect 存放裝置總管 tooan 堆疊 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="47cef-126">Now you are ready tooconnect Storage Explorer tooan Azure Stack subscription.</span></span>

### <a name="tooconnect-an-azure-stack-subscription"></a><span data-ttu-id="47cef-127">tooconnect 堆疊 Azure 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="47cef-127">tooconnect an Azure Stack subscription</span></span>


1. <span data-ttu-id="47cef-128">儲存體總管 （預覽） 重新啟動之後，請選取 hello**編輯**功能表，然後確定**目標 Azure 堆疊**已選取。</span><span class="sxs-lookup"><span data-stu-id="47cef-128">After Storage Explorer (Preview) restarts, select hello **Edit** menu, and then ensure that **Target Azure Stack** is selected.</span></span> <span data-ttu-id="47cef-129">如果未選取，並加以選取，然後重新啟動後，儲存體總管 hello 變更 tootake 效果。</span><span class="sxs-lookup"><span data-stu-id="47cef-129">If it is not selected, select it, and then restart Storage Explorer for hello change tootake effect.</span></span> <span data-ttu-id="47cef-130">不需要進行此設定，即可相容於 Azure Stack 環境。</span><span class="sxs-lookup"><span data-stu-id="47cef-130">This configuration is required for compatibility with your Azure Stack environment.</span></span>

    ![確保已選取目標 Azure Stack][28]

7. <span data-ttu-id="47cef-132">Hello 左窗格中，選取**管理帳戶**。</span><span class="sxs-lookup"><span data-stu-id="47cef-132">In hello left pane, select **Manage Accounts**.</span></span>  
    <span data-ttu-id="47cef-133">您已登入 tooare 顯示所有 hello Microsoft 帳戶。</span><span class="sxs-lookup"><span data-stu-id="47cef-133">All hello Microsoft accounts that you are signed in tooare displayed.</span></span>

8. <span data-ttu-id="47cef-134">tooconnect toohello Azure 堆疊帳戶選取**將帳戶加入**。</span><span class="sxs-lookup"><span data-stu-id="47cef-134">tooconnect toohello Azure Stack account, select **Add an account**.</span></span>

    ![新增 Azure Stack 帳戶][29]

9. <span data-ttu-id="47cef-136">在 hello**連接儲存體 tooAzure**對話方塊的  **Azure 環境**，選取**使用 Azure 堆疊環境**，然後按一下**下一步**.</span><span class="sxs-lookup"><span data-stu-id="47cef-136">In hello **Connect tooAzure Storage** dialog box, under **Azure environment**, select **Use Azure Stack Environment**, and then click **Next**.</span></span>

10. <span data-ttu-id="47cef-137">toosign hello 與至少一個有效的 Azure 堆疊訂用帳戶相關聯的 Azure 堆疊帳戶，以填入 hello**登入 tooAzure 堆疊環境** 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="47cef-137">toosign in with hello Azure Stack account that's associated with at least one active Azure Stack subscription, fill in hello **Sign in tooAzure Stack Environment** dialog box.</span></span>  

    <span data-ttu-id="47cef-138">每個欄位的 hello 詳細資料如下所示：</span><span class="sxs-lookup"><span data-stu-id="47cef-138">hello details for each field are as follows:</span></span>

    * <span data-ttu-id="47cef-139">**環境名稱**: hello 欄位可以由使用者自訂。</span><span class="sxs-lookup"><span data-stu-id="47cef-139">**Environment name**: hello field can be customized by user.</span></span>
    * <span data-ttu-id="47cef-140">**ARM 資源端點**: hello Azure 資源管理員資源端點的範例：</span><span class="sxs-lookup"><span data-stu-id="47cef-140">**ARM resource endpoint**: hello samples of Azure Resource Manager resource endpoints:</span></span>

        * <span data-ttu-id="47cef-141">若是雲端操作員：</span><span class="sxs-lookup"><span data-stu-id="47cef-141">For cloud operator:</span></span><br> <span data-ttu-id="47cef-142">https://adminmanagement.local.azurestack.external</span><span class="sxs-lookup"><span data-stu-id="47cef-142">https://adminmanagement.local.azurestack.external</span></span>   
        * <span data-ttu-id="47cef-143">若是租用戶：</span><span class="sxs-lookup"><span data-stu-id="47cef-143">For tenant:</span></span><br> <span data-ttu-id="47cef-144">https://management.local.azurestack.external</span><span class="sxs-lookup"><span data-stu-id="47cef-144">https://management.local.azurestack.external</span></span>
 
    * <span data-ttu-id="47cef-145">**租用戶識別碼**：選擇性。</span><span class="sxs-lookup"><span data-stu-id="47cef-145">**Tenant Id**: Optional.</span></span> <span data-ttu-id="47cef-146">必須指定 hello 目錄時，才指定 hello 值。</span><span class="sxs-lookup"><span data-stu-id="47cef-146">hello value is given only when hello directory must be specified.</span></span>

12. <span data-ttu-id="47cef-147">您已成功的帳戶登入 Azure 堆疊之後，hello 左的窗格會填入該帳戶相關聯的 hello Azure 堆疊訂閱。</span><span class="sxs-lookup"><span data-stu-id="47cef-147">After you successfully sign in with an Azure Stack account, hello left pane is populated with hello Azure Stack subscriptions associated with that account.</span></span> <span data-ttu-id="47cef-148">選取您要的 toowork，然後選取 hello Azure 堆疊訂閱**套用**。</span><span class="sxs-lookup"><span data-stu-id="47cef-148">Select hello Azure Stack subscriptions that you want toowork with, and then select **Apply**.</span></span> <span data-ttu-id="47cef-149">(選取或清除 hello**所有訂用帳戶**核取方塊切換全部選取或列出任何 hello Azure 堆疊訂用帳戶。)</span><span class="sxs-lookup"><span data-stu-id="47cef-149">(Selecting or clearing hello **All subscriptions** check box toggles selecting all or none of hello listed Azure Stack subscriptions.)</span></span>

    ![選取後填寫 hello 自訂雲端環境 對話方塊中的 hello Azure 堆疊訂用帳戶][30]  
    <span data-ttu-id="47cef-151">hello 左的窗格會顯示 hello hello 選取堆疊 Azure 訂閱相關聯的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="47cef-151">hello left pane displays hello storage accounts associated with hello selected Azure Stack subscriptions.</span></span>

    ![包含 Azure Stack 訂用帳戶的儲存體帳戶清單][31]

## <a name="next-steps"></a><span data-ttu-id="47cef-153">後續步驟</span><span class="sxs-lookup"><span data-stu-id="47cef-153">Next steps</span></span>
* [<span data-ttu-id="47cef-154">開始使用儲存體總管 (預覽)</span><span class="sxs-lookup"><span data-stu-id="47cef-154">Get started with Storage Explorer (Preview)</span></span>](../vs-azure-tools-storage-manage-with-storage-explorer.md)
* [<span data-ttu-id="47cef-155">Azure Stack 儲存體：差異與注意事項</span><span class="sxs-lookup"><span data-stu-id="47cef-155">Azure Stack Storage: differences and considerations</span></span>](azure-stack-acs-differences.md)


* <span data-ttu-id="47cef-156">toolearn 進一步了解 Azure 儲存體，請參閱[簡介 tooMicrosoft Azure 儲存體](../storage/common/storage-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="47cef-156">toolearn more about Azure Storage, see [Introduction tooMicrosoft Azure Storage](../storage/common/storage-introduction.md)</span></span>

[25]: ./media/azure-stack-storage-connect-se/add-certificate-azure-stack.png
[26]: ./media/azure-stack-storage-connect-se/export-root-cert-azure-stack.png
[27]: ./media/azure-stack-storage-connect-se/import-azure-stack-cert-storage-explorer.png
[28]: ./media/azure-stack-storage-connect-se/select-target-azure-stack.png
[29]: ./media/azure-stack-storage-connect-se/add-azure-stack-account.png
[30]: ./media/azure-stack-storage-connect-se/select-accounts-azure-stack.png
[31]: ./media/azure-stack-storage-connect-se/azure-stack-storage-account-list.png
