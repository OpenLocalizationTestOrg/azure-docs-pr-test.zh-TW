---
title: "將儲存體總管連線到 Azure Stack 訂用帳戶"
description: "了解如何將儲存體總管連線到 Azure Stack 訂用帳戶"
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
ms.date: 9/25/2017
ms.author: xiaofmao
ms.openlocfilehash: c7e6d70148d39fd74f6409a0a239833f8e9f7614
ms.sourcegitcommit: 90e2cced6a773b1b52f999ba73cd8877305d270b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/13/2017
---
# <a name="connect-storage-explorer-to-an-azure-stack-subscription"></a><span data-ttu-id="1297b-103">將儲存體總管連線到 Azure Stack 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="1297b-103">Connect Storage Explorer to an Azure Stack subscription</span></span>

<span data-ttu-id="1297b-104">適用於：Azure Stack 整合系統和 Azure Stack 開發套件</span><span class="sxs-lookup"><span data-stu-id="1297b-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span></span>

<span data-ttu-id="1297b-105">Azure 儲存體總管 (預覽) 是一個獨立應用程式，可讓您在 Windows、macOS 和 Linux 上輕鬆使用 Azure Stack 儲存體資料。</span><span class="sxs-lookup"><span data-stu-id="1297b-105">Azure Storage Explorer (Preview) is a standalone app that enables you to easily work with Azure Stack Storage data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="1297b-106">將資料移動至 Azure Stack 儲存體以及從 Azure Stack 儲存體移動資料有數個工具可供使用。</span><span class="sxs-lookup"><span data-stu-id="1297b-106">There are several tools avaialble to move data to and from Azure Stack Storage.</span></span> <span data-ttu-id="1297b-107">如需詳細資訊，請參閱 [Azure Stack 儲存體適用的資料傳輸工具](azure-stack-storage-transfer.md)。</span><span class="sxs-lookup"><span data-stu-id="1297b-107">For more information, see [Data transfer tools for Azure Stack storage](azure-stack-storage-transfer.md).</span></span>

<span data-ttu-id="1297b-108">在本文中，您將了解如何使用儲存體總管連線到 Azure Stack 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="1297b-108">In this article, you learn how to connect to your Azure Stack storage accounts using Storage Explorer.</span></span> 

<span data-ttu-id="1297b-109">如果您尚未安裝儲存體總管，請[下載](http://www.storageexplorer.com/)並安裝它。</span><span class="sxs-lookup"><span data-stu-id="1297b-109">If you haven't installed Storage Explorer yet, [download](http://www.storageexplorer.com/) and and install it.</span></span>

<span data-ttu-id="1297b-110">連線到 Azure Stack 訂用帳戶之後，您可以使用 [Azure 儲存體總管文章](../../vs-azure-tools-storage-manage-with-storage-explorer.md)來處理 Azure Stack 資料。</span><span class="sxs-lookup"><span data-stu-id="1297b-110">After you connect to your Azure Stack subscription, you can use the [Azure Storage Explorer articles](../../vs-azure-tools-storage-manage-with-storage-explorer.md) to work with your Azure Stack data.</span></span> 

## <a name="prepare-an-azure-stack-subscription"></a><span data-ttu-id="1297b-111">準備 Azure Stack 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="1297b-111">Prepare an Azure Stack subscription</span></span>

<span data-ttu-id="1297b-112">您必須可以存取 Azure Stack 主機電腦桌面或 VPN 連線，儲存體總管才能存取 Azure Stack 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="1297b-112">You need access to the Azure Stack host machine's desktop or a VPN connection for Storage Explorer to access the Azure Stack subscription.</span></span> <span data-ttu-id="1297b-113">若要深入了解如何設定 Azure Stack 的 VPN 連線，請參閱[使用 VPN 連線到 Azure Stack](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn)。</span><span class="sxs-lookup"><span data-stu-id="1297b-113">To learn how to set up a VPN connection to Azure Stack, see [Connect to Azure Stack with VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn).</span></span>

<span data-ttu-id="1297b-114">若是 Azure Stack 開發套件，您必須匯出 Azure Stack 授權單位根憑證。</span><span class="sxs-lookup"><span data-stu-id="1297b-114">For the Azure Stack Development Kit, you need to export the Azure Stack authority root certificate.</span></span>

### <a name="to-export-and-then-import-the-azure-stack-certificate"></a><span data-ttu-id="1297b-115">匯出 Azure Stack 憑證後再匯入</span><span class="sxs-lookup"><span data-stu-id="1297b-115">To export and then import the Azure Stack certificate</span></span>

1. <span data-ttu-id="1297b-116">在 Azure Stack 主機電腦或可使用 VPN 連線到 Azure Stack 的本機電腦上開啟 `mmc.exe`。</span><span class="sxs-lookup"><span data-stu-id="1297b-116">Open `mmc.exe` on an Azure Stack host machine, or a local machine with a VPN connection to Azure Stack.</span></span> 

2. <span data-ttu-id="1297b-117">在**檔案**，選取**新增/移除嵌入式管理單元**，然後再加入**憑證**管理**我的使用者帳戶**。</span><span class="sxs-lookup"><span data-stu-id="1297b-117">In **File**, select **Add/Remove Snap-in**, and then add **Certificates** to manage **My user account**.</span></span>



3. <span data-ttu-id="1297b-118">在 **Console Root\Certificated (Local Computer)\Trusted Root Certification Authorities\Certificates** 之下尋找 **AzureStackSelfSignedRootCert**。</span><span class="sxs-lookup"><span data-stu-id="1297b-118">Under **Console Root\Certificated (Local Computer)\Trusted Root Certification Authorities\Certificates** find **AzureStackSelfSignedRootCert**.</span></span>

    ![透過 mmc.exe 載入 Azure Stack 根憑證][25]

4. <span data-ttu-id="1297b-120">以滑鼠右鍵按一下憑證，選取 [所有工作] > [匯出]，然後依照指示，匯出 **Base-64 encoded X.509 (.CER)** 憑證。</span><span class="sxs-lookup"><span data-stu-id="1297b-120">Right-click the certificate, select **All Tasks** > **Export**, and then follow the instructions to export the certificate with **Base-64 encoded X.509 (.CER)**.</span></span>  

    <span data-ttu-id="1297b-121">下一個步驟中會使用所匯出的憑證。</span><span class="sxs-lookup"><span data-stu-id="1297b-121">The exported certificate will be used in the next step.</span></span>
5. <span data-ttu-id="1297b-122">啟動儲存體總管 (預覽)，如果您看到 [連線至 Azure 儲存體] 對話方塊，請將它取消。</span><span class="sxs-lookup"><span data-stu-id="1297b-122">Start Storage Explorer (Preview), and if you see the **Connect to Azure Storage** dialog box, cancel it.</span></span>

6. <span data-ttu-id="1297b-123">在 編輯 功能表上，指向 SSL 憑證，然後按一下匯入憑證。</span><span class="sxs-lookup"><span data-stu-id="1297b-123">On the **Edit** menu, point to **SSL Certificates**, and then click **Import Certificates**.</span></span> <span data-ttu-id="1297b-124">使用檔案選擇器對話方塊來尋找和開啟您在上一個步驟中瀏覽的憑證。</span><span class="sxs-lookup"><span data-stu-id="1297b-124">Use the file picker dialog box to find and open the certificate that you exported in the previous step.</span></span>

    <span data-ttu-id="1297b-125">匯入之後，系統會提示您重新啟動儲存體總管。</span><span class="sxs-lookup"><span data-stu-id="1297b-125">After importing, you are prompted to restart Storage Explorer.</span></span>

    ![將憑證匯入儲存體總管 (預覽) 中][27]

<span data-ttu-id="1297b-127">現在已經準備就緒，可以將儲存體總管連線到 Azure Stack 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="1297b-127">Now you are ready to connect Storage Explorer to an Azure Stack subscription.</span></span>

### <a name="to-connect-an-azure-stack-subscription"></a><span data-ttu-id="1297b-128">連線到 Azure Stack 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="1297b-128">To connect an Azure Stack subscription</span></span>


1. <span data-ttu-id="1297b-129">儲存體總管 (預覽) 重新啟動後，請選取 [編輯] 功能表，然後確保已選取 [目標 Azure Stack]。</span><span class="sxs-lookup"><span data-stu-id="1297b-129">After Storage Explorer (Preview) restarts, select the **Edit** menu, and then ensure that **Target Azure Stack** is selected.</span></span> <span data-ttu-id="1297b-130">若未選取，請加以選取，然後重新啟動儲存體總管，變更才會生效。</span><span class="sxs-lookup"><span data-stu-id="1297b-130">If it is not selected, select it, and then restart Storage Explorer for the change to take effect.</span></span> <span data-ttu-id="1297b-131">不需要進行此設定，即可相容於 Azure Stack 環境。</span><span class="sxs-lookup"><span data-stu-id="1297b-131">This configuration is required for compatibility with your Azure Stack environment.</span></span>

    ![確保已選取目標 Azure Stack][28]

7. <span data-ttu-id="1297b-133">在左側窗格中，選取 [管理帳戶]。</span><span class="sxs-lookup"><span data-stu-id="1297b-133">In the left pane, select **Manage Accounts**.</span></span>  
    <span data-ttu-id="1297b-134">隨即顯示您已登入的所有 Microsoft 帳戶。</span><span class="sxs-lookup"><span data-stu-id="1297b-134">All the Microsoft accounts that you are signed in to are displayed.</span></span>

8. <span data-ttu-id="1297b-135">若要連線到 Azure Stack 帳戶，請選取 [新增帳戶]。</span><span class="sxs-lookup"><span data-stu-id="1297b-135">To connect to the Azure Stack account, select **Add an account**.</span></span>

    ![新增 Azure Stack 帳戶][29]

9. <span data-ttu-id="1297b-137">在 連線至 Azure 儲存體 對話方塊的 Azure 環境 底下，選取 使用 Azure Stack 環境，然後按一下下一步。</span><span class="sxs-lookup"><span data-stu-id="1297b-137">In the **Connect to Azure Storage** dialog box, under **Azure environment**, select **Use Azure Stack Environment**, and then click **Next**.</span></span>

10. <span data-ttu-id="1297b-138">若要使用至少與一個作用中 Azure Stack 訂用帳戶相關聯的 Azure Stack 帳戶登入，請填寫 [登入 Azure Stack 環境] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="1297b-138">To sign in with the Azure Stack account that's associated with at least one active Azure Stack subscription, fill in the **Sign in to Azure Stack Environment** dialog box.</span></span>  

    <span data-ttu-id="1297b-139">每個欄位的詳細資料如下所示︰</span><span class="sxs-lookup"><span data-stu-id="1297b-139">The details for each field are as follows:</span></span>

    * <span data-ttu-id="1297b-140">**環境名稱**：使用者可以自訂此欄位。</span><span class="sxs-lookup"><span data-stu-id="1297b-140">**Environment name**: The field can be customized by user.</span></span>
    * <span data-ttu-id="1297b-141">**ARM 資源端點**：Azure Resource Manager 資源端點的範例︰</span><span class="sxs-lookup"><span data-stu-id="1297b-141">**ARM resource endpoint**: The samples of Azure Resource Manager resource endpoints:</span></span>

        * <span data-ttu-id="1297b-142">若是雲端操作員：</span><span class="sxs-lookup"><span data-stu-id="1297b-142">For cloud operator:</span></span><br> <span data-ttu-id="1297b-143">https://adminmanagement.local.azurestack.external</span><span class="sxs-lookup"><span data-stu-id="1297b-143">https://adminmanagement.local.azurestack.external</span></span>   
        * <span data-ttu-id="1297b-144">若是租用戶：</span><span class="sxs-lookup"><span data-stu-id="1297b-144">For tenant:</span></span><br> <span data-ttu-id="1297b-145">https://management.local.azurestack.external</span><span class="sxs-lookup"><span data-stu-id="1297b-145">https://management.local.azurestack.external</span></span>
 
    * <span data-ttu-id="1297b-146">**租用戶識別碼**：選擇性。</span><span class="sxs-lookup"><span data-stu-id="1297b-146">**Tenant Id**: Optional.</span></span> <span data-ttu-id="1297b-147">只有在必須指定目錄時，才會提供此值。</span><span class="sxs-lookup"><span data-stu-id="1297b-147">The value is given only when the directory must be specified.</span></span>

12. <span data-ttu-id="1297b-148">成功使用 Azure Stack 帳戶登入後，左窗格會填入與該帳戶相關聯的 Azure Stack 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="1297b-148">After you successfully sign in with an Azure Stack account, the left pane is populated with the Azure Stack subscriptions associated with that account.</span></span> <span data-ttu-id="1297b-149">選取您想要使用的 Azure Stack 訂用帳戶，然後選取 [套用]。</span><span class="sxs-lookup"><span data-stu-id="1297b-149">Select the Azure Stack subscriptions that you want to work with, and then select **Apply**.</span></span> <span data-ttu-id="1297b-150">(選取或清除 [所有訂用帳戶] 核取方塊切換開關，可選取全部或不選取任何列出的 Azure Stack 訂用帳戶。)</span><span class="sxs-lookup"><span data-stu-id="1297b-150">(Selecting or clearing the **All subscriptions** check box toggles selecting all or none of the listed Azure Stack subscriptions.)</span></span>

    ![在填妥 [自訂雲端環境] 對話方塊後選取 Azure Stack 訂用帳戶][30]  
    <span data-ttu-id="1297b-152">左窗格會顯示與所選 Azure Stack 訂用帳戶相關聯的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="1297b-152">The left pane displays the storage accounts associated with the selected Azure Stack subscriptions.</span></span>

    ![包含 Azure Stack 訂用帳戶的儲存體帳戶清單][31]

## <a name="next-steps"></a><span data-ttu-id="1297b-154">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1297b-154">Next steps</span></span>
* [<span data-ttu-id="1297b-155">開始使用儲存體總管 (預覽)</span><span class="sxs-lookup"><span data-stu-id="1297b-155">Get started with Storage Explorer (Preview)</span></span>](../../vs-azure-tools-storage-manage-with-storage-explorer.md)
* [<span data-ttu-id="1297b-156">Azure Stack 儲存體：差異與注意事項</span><span class="sxs-lookup"><span data-stu-id="1297b-156">Azure Stack Storage: differences and considerations</span></span>](azure-stack-acs-differences.md)


* <span data-ttu-id="1297b-157">若要深入了解 Azure 儲存體，請參閱 [Microsoft Azure 儲存體簡介](../../storage/common/storage-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="1297b-157">To learn more about Azure Storage, see [Introduction to Microsoft Azure Storage](../../storage/common/storage-introduction.md)</span></span>

[25]: ./media/azure-stack-storage-connect-se/add-certificate-azure-stack.png
[26]: ./media/azure-stack-storage-connect-se/export-root-cert-azure-stack.png
[27]: ./media/azure-stack-storage-connect-se/import-azure-stack-cert-storage-explorer.png
[28]: ./media/azure-stack-storage-connect-se/select-target-azure-stack.png
[29]: ./media/azure-stack-storage-connect-se/add-azure-stack-account.png
[30]: ./media/azure-stack-storage-connect-se/select-accounts-azure-stack.png
[31]: ./media/azure-stack-storage-connect-se/azure-stack-storage-account-list.png
