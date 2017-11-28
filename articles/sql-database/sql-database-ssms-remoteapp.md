---
title: "在 Azure RemoteApp 中使用 SQL Server Management Studio 連接到 SQL Database | Microsoft 文件"
description: "使用本教學課程來了解如何在連線到 SQL Database 時，在 Azure RemoteApp 中使用 SQL Server Management Studio 以維護安全性和效能"
services: sql-database
documentationcenter: 
author: adhurwit
manager: jhubbard
ms.assetid: 1052c83c-e7f5-4736-922f-216194d8874b
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/01/2016
ms.author: adhurwit
ms.openlocfilehash: ae1f2fa38d38fe6c10bc7960fddb07ae330d1eeb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="use-sql-server-management-studio-in-azure-remoteapp-to-connect-to-sql-database"></a><span data-ttu-id="a3dc2-103">在 Azure RemoteApp 中使用 SQL Server Management Studio 來連接到 SQL Database</span><span class="sxs-lookup"><span data-stu-id="a3dc2-103">Use SQL Server Management Studio in Azure RemoteApp to connect to SQL Database</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a3dc2-104">Azure RemoteApp 即將中止。</span><span class="sxs-lookup"><span data-stu-id="a3dc2-104">Azure RemoteApp is being discontinued.</span></span> <span data-ttu-id="a3dc2-105">如需詳細資訊，請參閱 [公告](https://go.microsoft.com/fwlink/?linkid=821148) 。</span><span class="sxs-lookup"><span data-stu-id="a3dc2-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
>

## <a name="introduction"></a><span data-ttu-id="a3dc2-106">簡介</span><span class="sxs-lookup"><span data-stu-id="a3dc2-106">Introduction</span></span>
<span data-ttu-id="a3dc2-107">本教學課程會示範如何在 Azure RemoteApp 中使用 SQL Server Management Studio (SSMS) 連接到 SQL Database。</span><span class="sxs-lookup"><span data-stu-id="a3dc2-107">This tutorial shows you how to use SQL Server Management Studio (SSMS) in Azure RemoteApp to connect to SQL Database.</span></span> <span data-ttu-id="a3dc2-108">它將逐步說明在 Azure RemoteApp 中設定 SQL Server Management Studio 的程序、說明優點，並示範您可以在 Azure Active Directory 中使用的安全性功能。</span><span class="sxs-lookup"><span data-stu-id="a3dc2-108">It walks you through the process of setting up SQL Server Management Studio in Azure RemoteApp, explains the benefits, and shows security features that you can use in Azure Active Directory.</span></span>

<span data-ttu-id="a3dc2-109">**預估完成時間：** 45 分鐘</span><span class="sxs-lookup"><span data-stu-id="a3dc2-109">**Estimated time to complete:** 45 minutes</span></span>

## <a name="ssms-in-azure-remoteapp"></a><span data-ttu-id="a3dc2-110">Azure RemoteApp 中的 SSMS</span><span class="sxs-lookup"><span data-stu-id="a3dc2-110">SSMS in Azure RemoteApp</span></span>
<span data-ttu-id="a3dc2-111">Azure RemoteApp 是在 Azure 中的一項 RDS 服務，可提供應用程式。</span><span class="sxs-lookup"><span data-stu-id="a3dc2-111">Azure RemoteApp is an RDS service in Azure that delivers applications.</span></span> <span data-ttu-id="a3dc2-112">您可以在此處深入了解： [什麼是 RemoteApp？](../remoteapp/remoteapp-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="a3dc2-112">You can learn more about it here: [What is RemoteApp?](../remoteapp/remoteapp-whatis.md)</span></span>

<span data-ttu-id="a3dc2-113">在 Azure RemoteApp 中執行的 SSMS 可提供您與在本機執行 SSMS 相同的體驗。</span><span class="sxs-lookup"><span data-stu-id="a3dc2-113">SSMS running in Azure RemoteApp gives you the same experience as running SSMS locally.</span></span>

![螢幕擷取畫面顯示正在 Azure RemoteApp 中執行的 SSMS][1]

## <a name="benefits"></a><span data-ttu-id="a3dc2-115">優點</span><span class="sxs-lookup"><span data-stu-id="a3dc2-115">Benefits</span></span>
<span data-ttu-id="a3dc2-116">在 Azure RemoteApp 中使用 SSMS 有許多好處，包括：</span><span class="sxs-lookup"><span data-stu-id="a3dc2-116">There are many benefits to using SSMS in Azure RemoteApp, including:</span></span>

* <span data-ttu-id="a3dc2-117">Azure SQL Server 上的連接埠 1433 不需要對外 (Azure 之外) 公開。</span><span class="sxs-lookup"><span data-stu-id="a3dc2-117">Port 1433 on Azure SQL server does not have to be exposed externally (outside of Azure).</span></span>
* <span data-ttu-id="a3dc2-118">不需要在 Azure SQL Server 防火牆中不斷新增和移除 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="a3dc2-118">No need to keep adding and removing IP addresses in the Azure SQL server firewall.</span></span>
* <span data-ttu-id="a3dc2-119">所有 Azure RemoteApp 連線都會使用加密的遠端桌面通訊協定，透過 HTTPS 在連接埠 443 上進行</span><span class="sxs-lookup"><span data-stu-id="a3dc2-119">All Azure RemoteApp connections occur over HTTPS on port 443 using encrypted Remote Desktop protocol</span></span>
* <span data-ttu-id="a3dc2-120">這是多使用者功能，且可以調整。</span><span class="sxs-lookup"><span data-stu-id="a3dc2-120">It is multi-user and can scale.</span></span>
* <span data-ttu-id="a3dc2-121">在與 SQL Database 相同的區域中擁有 SSMS 可增進效能。</span><span class="sxs-lookup"><span data-stu-id="a3dc2-121">There is a performance gain from having SSMS in the same region as the SQL Database.</span></span>
* <span data-ttu-id="a3dc2-122">您可以利用擁有使用者活動報告的 Azure Active Directory Premium Edition 來稽核 Azure RemoteApp 的使用狀況。</span><span class="sxs-lookup"><span data-stu-id="a3dc2-122">You can audit use of Azure RemoteApp with the Premium edition of Azure Active Directory which has user activity reports.</span></span>
* <span data-ttu-id="a3dc2-123">您可以啟用 Multi-Factor Authentication (MFA)。</span><span class="sxs-lookup"><span data-stu-id="a3dc2-123">You can enable multi-factor authentication (MFA).</span></span>
* <span data-ttu-id="a3dc2-124">使用任一種支援的 Azure RemoteApp 用戶端 (包括 iOS、Android、Mac、Windows Phone，和 Windows 電腦) 時，即可隨處存取 SSMS。</span><span class="sxs-lookup"><span data-stu-id="a3dc2-124">Access SSMS anywhere when using any of the supported Azure RemoteApp clients which includes iOS, Android, Mac, Windows Phone, and Windows PC’s.</span></span>

## <a name="create-the-azure-remoteapp-collection"></a><span data-ttu-id="a3dc2-125">建立 Azure RemoteApp 集合</span><span class="sxs-lookup"><span data-stu-id="a3dc2-125">Create the Azure RemoteApp collection</span></span>
<span data-ttu-id="a3dc2-126">以下是使用 SSMS 建立 Azure RemoteApp 集合的步驟：</span><span class="sxs-lookup"><span data-stu-id="a3dc2-126">Here are the steps to create your Azure RemoteApp collection with SSMS:</span></span>

### <a name="1-create-a-new-windows-vm-from-image"></a><span data-ttu-id="a3dc2-127">1.從映像建立新的 Windows VM</span><span class="sxs-lookup"><span data-stu-id="a3dc2-127">1. Create a new Windows VM from Image</span></span>
<span data-ttu-id="a3dc2-128">從資源庫中使用「Windows Server 遠端桌面工作階段主機 Windows Server 2012 R2」映像來建立您的新 VM。</span><span class="sxs-lookup"><span data-stu-id="a3dc2-128">Use the "Windows Server Remote Desktop Session Host Windows Server 2012 R2" Image from the Gallery to make your new VM.</span></span>

### <a name="2-install-ssms-from-sql-express"></a><span data-ttu-id="a3dc2-129">2.從 SQL Express 安裝 SSMS</span><span class="sxs-lookup"><span data-stu-id="a3dc2-129">2. Install SSMS from SQL Express</span></span>
<span data-ttu-id="a3dc2-130">移至新的 VM 並瀏覽到此下載頁面：[Microsoft® SQL Server® 2014 Express](https://www.microsoft.com/download/details.aspx?id=42299)</span><span class="sxs-lookup"><span data-stu-id="a3dc2-130">Go onto the new VM and navigate to this download page: [Microsoft® SQL Server® 2014 Express](https://www.microsoft.com/download/details.aspx?id=42299)</span></span>

<span data-ttu-id="a3dc2-131">有一個僅下載 SSMS 的選項。</span><span class="sxs-lookup"><span data-stu-id="a3dc2-131">There is an option to only download SSMS.</span></span> <span data-ttu-id="a3dc2-132">下載之後，移至安裝目錄，並執行安裝程式以安裝 SSMS。</span><span class="sxs-lookup"><span data-stu-id="a3dc2-132">After download, go into the install directory and run Setup to install SSMS.</span></span>

<span data-ttu-id="a3dc2-133">您同時需要安裝 SQL Server 2014 Service Pack 1。</span><span class="sxs-lookup"><span data-stu-id="a3dc2-133">You also need to install SQL Server 2014 Service Pack 1.</span></span> <span data-ttu-id="a3dc2-134">您可以在這裡下載：[Microsoft SQL Server 2014 Service Pack 1 (SP1)](https://www.microsoft.com/download/details.aspx?id=46694)</span><span class="sxs-lookup"><span data-stu-id="a3dc2-134">You can download it here: [Microsoft SQL Server 2014 Service Pack 1 (SP1)](https://www.microsoft.com/download/details.aspx?id=46694)</span></span>

<span data-ttu-id="a3dc2-135">SQL Server 2014 Service Pack 1 包含和 Azure SQL Database 搭配使用的基本功能。</span><span class="sxs-lookup"><span data-stu-id="a3dc2-135">SQL Server 2014 Service Pack 1 includes essential functionality for working with Azure SQL Database.</span></span>

### <a name="3-run-validate-script-and-sysprep"></a><span data-ttu-id="a3dc2-136">3.執行「驗證」指令碼和 SysPrep</span><span class="sxs-lookup"><span data-stu-id="a3dc2-136">3. Run Validate script and Sysprep</span></span>
<span data-ttu-id="a3dc2-137">VM 桌面上的是稱為「驗證」的 PowerShell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="a3dc2-137">On the desktop of the VM is a PowerShell script called Validate.</span></span> <span data-ttu-id="a3dc2-138">按兩下以執行此指令碼。</span><span class="sxs-lookup"><span data-stu-id="a3dc2-138">Run this by double-clicking.</span></span> <span data-ttu-id="a3dc2-139">它會確認 VM 已準備好用於遠端裝載應用程式。</span><span class="sxs-lookup"><span data-stu-id="a3dc2-139">It will verify that the VM is ready to be used for remote hosting of applications.</span></span> <span data-ttu-id="a3dc2-140">驗證完成時，它會要求執行 Sysprep - 請選擇執行它。</span><span class="sxs-lookup"><span data-stu-id="a3dc2-140">When verification is complete, it will ask to run sysprep - choose to run it.</span></span>

<span data-ttu-id="a3dc2-141">Sysprep 完成時，它會關閉 VM。</span><span class="sxs-lookup"><span data-stu-id="a3dc2-141">When sysprep completes, it will shut down the VM.</span></span>

<span data-ttu-id="a3dc2-142">若要深入了解建立 Azure RemoteApp 映像，請參閱： [How to create a RemoteApp template image in Azure (如何在 Azure 中建立 RemoteApp 範本映像)](http://blogs.msdn.com/b/rds/archive/2015/03/17/how-to-create-a-remoteapp-template-image-in-azure.aspx)</span><span class="sxs-lookup"><span data-stu-id="a3dc2-142">To learn more about creating a Azure RemoteApp image, see: [How to create a RemoteApp template image in Azure](http://blogs.msdn.com/b/rds/archive/2015/03/17/how-to-create-a-remoteapp-template-image-in-azure.aspx)</span></span>

### <a name="4-capture-image"></a><span data-ttu-id="a3dc2-143">4.擷取映像</span><span class="sxs-lookup"><span data-stu-id="a3dc2-143">4. Capture image</span></span>
<span data-ttu-id="a3dc2-144">當 VM 已經停止執行時，請在目前的入口網站尋找並擷取它。</span><span class="sxs-lookup"><span data-stu-id="a3dc2-144">When the VM has stopped running, find it in the current portal and capture it.</span></span>

<span data-ttu-id="a3dc2-145">若要深入了解擷取映像，[請參閱擷取以傳統部署模型建立之 Azure Windows 虛擬機器的映像](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="a3dc2-145">To learn more about capturing an image, see [Capture an image of an Azure Windows virtual machine created with the classic deployment model](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span></span>

### <a name="5-add-to-azure-remoteapp-template-images"></a><span data-ttu-id="a3dc2-146">5.新增至 Azure RemoteApp 範本映像</span><span class="sxs-lookup"><span data-stu-id="a3dc2-146">5. Add to Azure RemoteApp Template images</span></span>
<span data-ttu-id="a3dc2-147">在目前入口網站的 [Azure RemoteApp] 區段中，移至 [範本映像] 索引標籤然後按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="a3dc2-147">In the Azure RemoteApp section of the current portal, go to the Template Images tab and click Add.</span></span> <span data-ttu-id="a3dc2-148">在快顯方塊中，選取 [從您的虛擬機器映像庫匯入映像] 然後選擇您剛才建立的映像。</span><span class="sxs-lookup"><span data-stu-id="a3dc2-148">In the pop-up box, select "Import an image from your Virtual Machines library" and then choose the Image that you just created.</span></span>

### <a name="6-create-cloud-collection"></a><span data-ttu-id="a3dc2-149">6.建立雲端集合</span><span class="sxs-lookup"><span data-stu-id="a3dc2-149">6. Create cloud collection</span></span>
<span data-ttu-id="a3dc2-150">在目前的入口網站中，建立新的 Azure RemoteApp 雲端集合。</span><span class="sxs-lookup"><span data-stu-id="a3dc2-150">In the current portal, create a new Azure RemoteApp Cloud Collection.</span></span> <span data-ttu-id="a3dc2-151">選擇您剛才匯入之已安裝 SSMS 的範本映像。</span><span class="sxs-lookup"><span data-stu-id="a3dc2-151">Choose the Template Image that you just imported with SSMS installed on it.</span></span>

![建立新的雲端集合][2]

### <a name="7-publish-ssms"></a><span data-ttu-id="a3dc2-153">7.發佈 SSMS</span><span class="sxs-lookup"><span data-stu-id="a3dc2-153">7. Publish SSMS</span></span>
<span data-ttu-id="a3dc2-154">在新雲端集合的 [發佈] 索引標籤上，從 [開始] 功能表選取 [發佈應用程式]，然後從清單中選擇 SSMS。</span><span class="sxs-lookup"><span data-stu-id="a3dc2-154">On the Publishing tab of your new cloud collection, select Publish an application from the Start Menu and then choose SSMS from the list.</span></span>

![發佈應用程式][5]

### <a name="8-add-users"></a><span data-ttu-id="a3dc2-156">8.新增使用者</span><span class="sxs-lookup"><span data-stu-id="a3dc2-156">8. Add users</span></span>
<span data-ttu-id="a3dc2-157">您可以在 [使用者存取] 索引標籤上，選取將能存取這個只包含 SSMS 之 Azure RemoteApp 集合的使用者。</span><span class="sxs-lookup"><span data-stu-id="a3dc2-157">On the User Access tab you can select the users that will have access to this Azure RemoteApp collection which only includes SSMS.</span></span>

![新增使用者][6]

### <a name="9-install-the-azure-remoteapp-client-application"></a><span data-ttu-id="a3dc2-159">9.安裝 Azure RemoteApp 用戶端應用程式</span><span class="sxs-lookup"><span data-stu-id="a3dc2-159">9. Install the Azure RemoteApp client application</span></span>
<span data-ttu-id="a3dc2-160">您可以在這裡下載並安裝 Azure RemoteApp 用戶端： [下載 | Azure RemoteApp](https://www.remoteapp.windowsazure.com/en/clients.aspx)</span><span class="sxs-lookup"><span data-stu-id="a3dc2-160">You can download and install a Azure RemoteApp client here: [Download | Azure RemoteApp](https://www.remoteapp.windowsazure.com/en/clients.aspx)</span></span>

## <a name="configure-azure-sql-server"></a><span data-ttu-id="a3dc2-161">設定 Azure SQL Server</span><span class="sxs-lookup"><span data-stu-id="a3dc2-161">Configure Azure SQL server</span></span>
<span data-ttu-id="a3dc2-162">所需的唯一設定是確保已針對防火牆啟用 Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="a3dc2-162">The only configuration needed is to ensure that Azure Services is enabled for the firewall.</span></span> <span data-ttu-id="a3dc2-163">如果您使用此方案，就不需要新增任何的 IP 位址來開啟防火牆。</span><span class="sxs-lookup"><span data-stu-id="a3dc2-163">If you use this solution, then you do not need to add any IP addresses to open the firewall.</span></span> <span data-ttu-id="a3dc2-164">允許進入 SQL Server 的網路流量來自於其他 Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="a3dc2-164">The network traffic that is allowed to the SQL Server is from other Azure services.</span></span>

![Azure 允許][4]

## <a name="multi-factor-authentication-mfa"></a><span data-ttu-id="a3dc2-166">Multi-Factor Authentication (MFA)</span><span class="sxs-lookup"><span data-stu-id="a3dc2-166">Multi-Factor Authentication (MFA)</span></span>
<span data-ttu-id="a3dc2-167">可特別為此應用程式啟用 MFA。</span><span class="sxs-lookup"><span data-stu-id="a3dc2-167">MFA can be enabled for this application specifically.</span></span> <span data-ttu-id="a3dc2-168">移至 Azure Active Directory 的 [應用程式] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="a3dc2-168">Go to the Applications tab of your Azure Active Directory.</span></span> <span data-ttu-id="a3dc2-169">您會發現 Microsoft Azure RemoteApp 的項目。</span><span class="sxs-lookup"><span data-stu-id="a3dc2-169">You will find an entry for Microsoft Azure RemoteApp.</span></span> <span data-ttu-id="a3dc2-170">如果您按一下該應用程式然後設定，您將會看到以下頁面，您可以在頁面中為此應用程式啟用 MFA。</span><span class="sxs-lookup"><span data-stu-id="a3dc2-170">If you click that application and then configure, you will see the page below where you can enable MFA for this application.</span></span>

![啟用 MFA][3]

## <a name="audit-user-activity-with-azure-active-directory-premium"></a><span data-ttu-id="a3dc2-172">使用 Azure Active Directory Premium 稽核使用者活動</span><span class="sxs-lookup"><span data-stu-id="a3dc2-172">Audit user activity with Azure Active Directory Premium</span></span>
<span data-ttu-id="a3dc2-173">如果您沒有 Azure AD Premium，那麼您必須在您目錄的 [授權] 區段中將它開啟。</span><span class="sxs-lookup"><span data-stu-id="a3dc2-173">If you do not have Azure AD Premium, then you have to turn it on in the Licenses section of your directory.</span></span> <span data-ttu-id="a3dc2-174">啟用 Premium 之後，您可以將使用者指派到 Premium 層級。</span><span class="sxs-lookup"><span data-stu-id="a3dc2-174">With Premium enabled, you can assign users to the Premium level.</span></span>

<span data-ttu-id="a3dc2-175">當您移至 Azure Active Directory 中的使用者時，您接著可以移至 [活動] 索引標籤來查看 Azure RemoteApp 的登入資訊。</span><span class="sxs-lookup"><span data-stu-id="a3dc2-175">When you go to a user in your Azure Active Directory, you can then go to the Activity tab to see login information to Azure RemoteApp.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a3dc2-176">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a3dc2-176">Next steps</span></span>
<span data-ttu-id="a3dc2-177">完成上述的所有步驟之後，您將可以執行 Azure RemoteApp 用戶端，並使用已指派的使用者登入。</span><span class="sxs-lookup"><span data-stu-id="a3dc2-177">After completing all the above steps, you will be able to run the Azure RemoteApp client and log-in with an assigned user.</span></span> <span data-ttu-id="a3dc2-178">您將會看到 SSMS 顯示為您的其中一個應用程式，而您可以將它當作就像是安裝在您電腦上而能夠存取 Azure SQL Server 一樣來執行它。</span><span class="sxs-lookup"><span data-stu-id="a3dc2-178">You will be presented with SSMS as one of your applications, and you can run it as you would if it were installed on your computer with access to Azure SQL server.</span></span>

<span data-ttu-id="a3dc2-179">如需有關如何連接到 SQL Database 的詳細資訊，請參閱 [使用 SQL Server Management Studio 連接到 SQL Database 並執行範例 T-SQL 查詢](sql-database-connect-query-ssms.md)。</span><span class="sxs-lookup"><span data-stu-id="a3dc2-179">For more information on how to make the connection to SQL Database, see [Connect to SQL Database with SQL Server Management Studio and perform a sample T-SQL query](sql-database-connect-query-ssms.md).</span></span>

<span data-ttu-id="a3dc2-180">以上為目前的所有內容。</span><span class="sxs-lookup"><span data-stu-id="a3dc2-180">That's everything for now.</span></span> <span data-ttu-id="a3dc2-181">盡情享受！</span><span class="sxs-lookup"><span data-stu-id="a3dc2-181">Enjoy!</span></span>

<!--Image references-->
[1]: ./media/sql-database-ssms-remoteapp/ssms.png
[2]: ./media/sql-database-ssms-remoteapp/newcloudcollection.png
[3]: ./media/sql-database-ssms-remoteapp/mfa.png
[4]: ./media/sql-database-ssms-remoteapp/allowazure.png
[5]: ./media/sql-database-ssms-remoteapp/publish.png
[6]: ./media/sql-database-ssms-remoteapp/user.png