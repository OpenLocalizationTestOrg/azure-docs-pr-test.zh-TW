---
title: "aaaConnect tooSQL Azure RemoteApp 中使用 SQL Server Management Studio 的資料庫 |Microsoft 文件"
description: "如何使用這個教學課程 toolearn toouse Azure RemoteApp 中的 SQL Server Management Studio 的安全性和連接 tooSQL 資料庫時的效能"
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
ms.openlocfilehash: 73994f9a1eb3e48efa5d7c4f976b00cfcbc88d75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-sql-server-management-studio-in-azure-remoteapp-tooconnect-toosql-database"></a><span data-ttu-id="f0b29-103">在 Azure RemoteApp tooconnect tooSQL 資料庫中使用 SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="f0b29-103">Use SQL Server Management Studio in Azure RemoteApp tooconnect tooSQL Database</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f0b29-104">Azure RemoteApp 即將中止。</span><span class="sxs-lookup"><span data-stu-id="f0b29-104">Azure RemoteApp is being discontinued.</span></span> <span data-ttu-id="f0b29-105">讀取 hello[公告](https://go.microsoft.com/fwlink/?linkid=821148)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="f0b29-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
>

## <a name="introduction"></a><span data-ttu-id="f0b29-106">簡介</span><span class="sxs-lookup"><span data-stu-id="f0b29-106">Introduction</span></span>
<span data-ttu-id="f0b29-107">本教學課程示範如何在 Azure RemoteApp tooconnect tooSQL 資料庫 toouse SQL Server Management Studio (SSMS)。</span><span class="sxs-lookup"><span data-stu-id="f0b29-107">This tutorial shows you how toouse SQL Server Management Studio (SSMS) in Azure RemoteApp tooconnect tooSQL Database.</span></span> <span data-ttu-id="f0b29-108">它會引導您設定 SQL Server Management Studio，在 Azure RemoteApp 中的 hello 程序、 說明 hello 優點，並顯示安全性功能，您可以使用 Azure Active Directory 中。</span><span class="sxs-lookup"><span data-stu-id="f0b29-108">It walks you through hello process of setting up SQL Server Management Studio in Azure RemoteApp, explains hello benefits, and shows security features that you can use in Azure Active Directory.</span></span>

<span data-ttu-id="f0b29-109">**估計時間 toocomplete:** 45 分鐘的時間</span><span class="sxs-lookup"><span data-stu-id="f0b29-109">**Estimated time toocomplete:** 45 minutes</span></span>

## <a name="ssms-in-azure-remoteapp"></a><span data-ttu-id="f0b29-110">Azure RemoteApp 中的 SSMS</span><span class="sxs-lookup"><span data-stu-id="f0b29-110">SSMS in Azure RemoteApp</span></span>
<span data-ttu-id="f0b29-111">Azure RemoteApp 是在 Azure 中的一項 RDS 服務，可提供應用程式。</span><span class="sxs-lookup"><span data-stu-id="f0b29-111">Azure RemoteApp is an RDS service in Azure that delivers applications.</span></span> <span data-ttu-id="f0b29-112">您可以在此處深入了解： [什麼是 RemoteApp？](../remoteapp/remoteapp-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="f0b29-112">You can learn more about it here: [What is RemoteApp?](../remoteapp/remoteapp-whatis.md)</span></span>

<span data-ttu-id="f0b29-113">SSMS 執行在 Azure RemoteApp 可讓您 hello 與在本機執行 SSMS 相同的體驗。</span><span class="sxs-lookup"><span data-stu-id="f0b29-113">SSMS running in Azure RemoteApp gives you hello same experience as running SSMS locally.</span></span>

![螢幕擷取畫面顯示正在 Azure RemoteApp 中執行的 SSMS][1]

## <a name="benefits"></a><span data-ttu-id="f0b29-115">優點</span><span class="sxs-lookup"><span data-stu-id="f0b29-115">Benefits</span></span>
<span data-ttu-id="f0b29-116">有許多優點 toousing Azure RemoteApp 中的 SSMS 包括：</span><span class="sxs-lookup"><span data-stu-id="f0b29-116">There are many benefits toousing SSMS in Azure RemoteApp, including:</span></span>

* <span data-ttu-id="f0b29-117">Azure SQL server 上的通訊埠 1433年沒有 toobe 公開外部 （Azure) 外部。</span><span class="sxs-lookup"><span data-stu-id="f0b29-117">Port 1433 on Azure SQL server does not have toobe exposed externally (outside of Azure).</span></span>
* <span data-ttu-id="f0b29-118">不是需要 tookeep 新增和移除 hello Azure SQL server 防火牆中的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="f0b29-118">No need tookeep adding and removing IP addresses in hello Azure SQL server firewall.</span></span>
* <span data-ttu-id="f0b29-119">所有 Azure RemoteApp 連線都會使用加密的遠端桌面通訊協定，透過 HTTPS 在連接埠 443 上進行</span><span class="sxs-lookup"><span data-stu-id="f0b29-119">All Azure RemoteApp connections occur over HTTPS on port 443 using encrypted Remote Desktop protocol</span></span>
* <span data-ttu-id="f0b29-120">這是多使用者功能，且可以調整。</span><span class="sxs-lookup"><span data-stu-id="f0b29-120">It is multi-user and can scale.</span></span>
* <span data-ttu-id="f0b29-121">不必 SSMS hello 效能提升 hello SQL 資料庫與相同的區域。</span><span class="sxs-lookup"><span data-stu-id="f0b29-121">There is a performance gain from having SSMS in hello same region as hello SQL Database.</span></span>
* <span data-ttu-id="f0b29-122">您可以稽核 hello Premium edition，其具有使用者活動報告的 Azure Active directory 與 Azure remoteapp 使用。</span><span class="sxs-lookup"><span data-stu-id="f0b29-122">You can audit use of Azure RemoteApp with hello Premium edition of Azure Active Directory which has user activity reports.</span></span>
* <span data-ttu-id="f0b29-123">您可以啟用 Multi-Factor Authentication (MFA)。</span><span class="sxs-lookup"><span data-stu-id="f0b29-123">You can enable multi-factor authentication (MFA).</span></span>
* <span data-ttu-id="f0b29-124">存取任何地方時使用任何 hello SSMS 支援的 Azure RemoteApp 用戶端，包括 iOS、 Android、 Mac、 Windows Phone 和 Windows 電腦。</span><span class="sxs-lookup"><span data-stu-id="f0b29-124">Access SSMS anywhere when using any of hello supported Azure RemoteApp clients which includes iOS, Android, Mac, Windows Phone, and Windows PC’s.</span></span>

## <a name="create-hello-azure-remoteapp-collection"></a><span data-ttu-id="f0b29-125">建立 hello Azure RemoteApp 集合</span><span class="sxs-lookup"><span data-stu-id="f0b29-125">Create hello Azure RemoteApp collection</span></span>
<span data-ttu-id="f0b29-126">以下是您的 Azure RemoteApp 集合，使用 SSMS hello 步驟 toocreate:</span><span class="sxs-lookup"><span data-stu-id="f0b29-126">Here are hello steps toocreate your Azure RemoteApp collection with SSMS:</span></span>

### <a name="1-create-a-new-windows-vm-from-image"></a><span data-ttu-id="f0b29-127">1.從映像建立新的 Windows VM</span><span class="sxs-lookup"><span data-stu-id="f0b29-127">1. Create a new Windows VM from Image</span></span>
<span data-ttu-id="f0b29-128">新的 VM 使用 hello hello 圖庫 toomake 從 「 Windows Server 遠端桌面工作階段主機 Windows Server 2012 R2 」 映像。</span><span class="sxs-lookup"><span data-stu-id="f0b29-128">Use hello "Windows Server Remote Desktop Session Host Windows Server 2012 R2" Image from hello Gallery toomake your new VM.</span></span>

### <a name="2-install-ssms-from-sql-express"></a><span data-ttu-id="f0b29-129">2.從 SQL Express 安裝 SSMS</span><span class="sxs-lookup"><span data-stu-id="f0b29-129">2. Install SSMS from SQL Express</span></span>
<span data-ttu-id="f0b29-130">移至 hello 新的 VM，並瀏覽 toothis 下載頁面： [Microsoft® SQL Server® 2014 Express](https://www.microsoft.com/download/details.aspx?id=42299)</span><span class="sxs-lookup"><span data-stu-id="f0b29-130">Go onto hello new VM and navigate toothis download page: [Microsoft® SQL Server® 2014 Express](https://www.microsoft.com/download/details.aspx?id=42299)</span></span>

<span data-ttu-id="f0b29-131">沒有選項 tooonly 下載 SSMS。</span><span class="sxs-lookup"><span data-stu-id="f0b29-131">There is an option tooonly download SSMS.</span></span> <span data-ttu-id="f0b29-132">下載之後, 進入 hello 安裝目錄並執行安裝程式 tooinstall SSMS。</span><span class="sxs-lookup"><span data-stu-id="f0b29-132">After download, go into hello install directory and run Setup tooinstall SSMS.</span></span>

<span data-ttu-id="f0b29-133">您也需要 tooinstall SQL Server 2014 Service Pack 1。</span><span class="sxs-lookup"><span data-stu-id="f0b29-133">You also need tooinstall SQL Server 2014 Service Pack 1.</span></span> <span data-ttu-id="f0b29-134">您可以在這裡下載：[Microsoft SQL Server 2014 Service Pack 1 (SP1)](https://www.microsoft.com/download/details.aspx?id=46694)</span><span class="sxs-lookup"><span data-stu-id="f0b29-134">You can download it here: [Microsoft SQL Server 2014 Service Pack 1 (SP1)](https://www.microsoft.com/download/details.aspx?id=46694)</span></span>

<span data-ttu-id="f0b29-135">SQL Server 2014 Service Pack 1 包含和 Azure SQL Database 搭配使用的基本功能。</span><span class="sxs-lookup"><span data-stu-id="f0b29-135">SQL Server 2014 Service Pack 1 includes essential functionality for working with Azure SQL Database.</span></span>

### <a name="3-run-validate-script-and-sysprep"></a><span data-ttu-id="f0b29-136">3.執行「驗證」指令碼和 SysPrep</span><span class="sxs-lookup"><span data-stu-id="f0b29-136">3. Run Validate script and Sysprep</span></span>
<span data-ttu-id="f0b29-137">Hello VM 桌面上是 hello 的稱為驗證的 PowerShell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="f0b29-137">On hello desktop of hello VM is a PowerShell script called Validate.</span></span> <span data-ttu-id="f0b29-138">按兩下以執行此指令碼。</span><span class="sxs-lookup"><span data-stu-id="f0b29-138">Run this by double-clicking.</span></span> <span data-ttu-id="f0b29-139">它將會驗證該 hello VM 準備好 toobe 用於遠端裝載的應用程式。</span><span class="sxs-lookup"><span data-stu-id="f0b29-139">It will verify that hello VM is ready toobe used for remote hosting of applications.</span></span> <span data-ttu-id="f0b29-140">驗證完成時，它會要求 toorun sysprep-選擇 toorun 它。</span><span class="sxs-lookup"><span data-stu-id="f0b29-140">When verification is complete, it will ask toorun sysprep - choose toorun it.</span></span>

<span data-ttu-id="f0b29-141">Sysprep 完成時，它會關閉 hello VM。</span><span class="sxs-lookup"><span data-stu-id="f0b29-141">When sysprep completes, it will shut down hello VM.</span></span>

<span data-ttu-id="f0b29-142">toolearn 進一步了解建立 Azure RemoteApp 映像，請參閱： [toocreate RemoteApp 範本映像在 Azure 中的方式](http://blogs.msdn.com/b/rds/archive/2015/03/17/how-to-create-a-remoteapp-template-image-in-azure.aspx)</span><span class="sxs-lookup"><span data-stu-id="f0b29-142">toolearn more about creating a Azure RemoteApp image, see: [How toocreate a RemoteApp template image in Azure](http://blogs.msdn.com/b/rds/archive/2015/03/17/how-to-create-a-remoteapp-template-image-in-azure.aspx)</span></span>

### <a name="4-capture-image"></a><span data-ttu-id="f0b29-143">4.擷取映像</span><span class="sxs-lookup"><span data-stu-id="f0b29-143">4. Capture image</span></span>
<span data-ttu-id="f0b29-144">當 VM 已停止執行，hello hello 目前入口網站中找到它和擷取它。</span><span class="sxs-lookup"><span data-stu-id="f0b29-144">When hello VM has stopped running, find it in hello current portal and capture it.</span></span>

<span data-ttu-id="f0b29-145">toolearn 深入了解擷取映像，請參閱[擷取與 hello 傳統部署模型所建立的 Azure Windows 虛擬機器的映像](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="f0b29-145">toolearn more about capturing an image, see [Capture an image of an Azure Windows virtual machine created with hello classic deployment model](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span></span>

### <a name="5-add-tooazure-remoteapp-template-images"></a><span data-ttu-id="f0b29-146">5.新增 tooAzure RemoteApp 範本映像</span><span class="sxs-lookup"><span data-stu-id="f0b29-146">5. Add tooAzure RemoteApp Template images</span></span>
<span data-ttu-id="f0b29-147">在 hello hello 目前入口網站的 Azure RemoteApp 區段中，移 toohello 範本映像 索引標籤並按一下 新增。</span><span class="sxs-lookup"><span data-stu-id="f0b29-147">In hello Azure RemoteApp section of hello current portal, go toohello Template Images tab and click Add.</span></span> <span data-ttu-id="f0b29-148">在 hello 快顯方塊中，選取 [從虛擬機器程式庫匯入映像]，然後選擇 hello 您剛才建立的映像。</span><span class="sxs-lookup"><span data-stu-id="f0b29-148">In hello pop-up box, select "Import an image from your Virtual Machines library" and then choose hello Image that you just created.</span></span>

### <a name="6-create-cloud-collection"></a><span data-ttu-id="f0b29-149">6.建立雲端集合</span><span class="sxs-lookup"><span data-stu-id="f0b29-149">6. Create cloud collection</span></span>
<span data-ttu-id="f0b29-150">Hello 目前入口網站中建立新的 Azure RemoteApp 雲端集合。</span><span class="sxs-lookup"><span data-stu-id="f0b29-150">In hello current portal, create a new Azure RemoteApp Cloud Collection.</span></span> <span data-ttu-id="f0b29-151">選擇您剛才匯入使用 SSMS 在其上安裝的範本影像 hello。</span><span class="sxs-lookup"><span data-stu-id="f0b29-151">Choose hello Template Image that you just imported with SSMS installed on it.</span></span>

![建立新的雲端集合][2]

### <a name="7-publish-ssms"></a><span data-ttu-id="f0b29-153">7.發佈 SSMS</span><span class="sxs-lookup"><span data-stu-id="f0b29-153">7. Publish SSMS</span></span>
<span data-ttu-id="f0b29-154">Hello hello 從應用程式發行新的雲端集合，選取發行] 索引標籤上的 [開始] 功能表，然後從 hello 清單中選擇 [SSMS。</span><span class="sxs-lookup"><span data-stu-id="f0b29-154">On hello Publishing tab of your new cloud collection, select Publish an application from hello Start Menu and then choose SSMS from hello list.</span></span>

![發佈應用程式][5]

### <a name="8-add-users"></a><span data-ttu-id="f0b29-156">8.新增使用者</span><span class="sxs-lookup"><span data-stu-id="f0b29-156">8. Add users</span></span>
<span data-ttu-id="f0b29-157">Hello 使用者存取 索引標籤中，您可以選取 hello 使用者必須存取其中只包含 SSMS toothis Azure RemoteApp 集合。</span><span class="sxs-lookup"><span data-stu-id="f0b29-157">On hello User Access tab you can select hello users that will have access toothis Azure RemoteApp collection which only includes SSMS.</span></span>

![新增使用者][6]

### <a name="9-install-hello-azure-remoteapp-client-application"></a><span data-ttu-id="f0b29-159">9.安裝 hello Azure RemoteApp 用戶端應用程式</span><span class="sxs-lookup"><span data-stu-id="f0b29-159">9. Install hello Azure RemoteApp client application</span></span>
<span data-ttu-id="f0b29-160">您可以在這裡下載並安裝 Azure RemoteApp 用戶端： [下載 | Azure RemoteApp](https://www.remoteapp.windowsazure.com/en/clients.aspx)</span><span class="sxs-lookup"><span data-stu-id="f0b29-160">You can download and install a Azure RemoteApp client here: [Download | Azure RemoteApp](https://www.remoteapp.windowsazure.com/en/clients.aspx)</span></span>

## <a name="configure-azure-sql-server"></a><span data-ttu-id="f0b29-161">設定 Azure SQL Server</span><span class="sxs-lookup"><span data-stu-id="f0b29-161">Configure Azure SQL server</span></span>
<span data-ttu-id="f0b29-162">hello 只需要設定了 Azure 服務的 tooensure 啟用 hello 防火牆。</span><span class="sxs-lookup"><span data-stu-id="f0b29-162">hello only configuration needed is tooensure that Azure Services is enabled for hello firewall.</span></span> <span data-ttu-id="f0b29-163">如果您使用此方案，然後您不需要 tooadd 任何 IP 位址 tooopen hello 防火牆。</span><span class="sxs-lookup"><span data-stu-id="f0b29-163">If you use this solution, then you do not need tooadd any IP addresses tooopen hello firewall.</span></span> <span data-ttu-id="f0b29-164">允許 toohello SQL Server 的 hello 網路流量會從其他 Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="f0b29-164">hello network traffic that is allowed toohello SQL Server is from other Azure services.</span></span>

![Azure 允許][4]

## <a name="multi-factor-authentication-mfa"></a><span data-ttu-id="f0b29-166">Multi-Factor Authentication (MFA)</span><span class="sxs-lookup"><span data-stu-id="f0b29-166">Multi-Factor Authentication (MFA)</span></span>
<span data-ttu-id="f0b29-167">可特別為此應用程式啟用 MFA。</span><span class="sxs-lookup"><span data-stu-id="f0b29-167">MFA can be enabled for this application specifically.</span></span> <span data-ttu-id="f0b29-168">移 toohello 的 Azure Active Directory 的應用程式 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="f0b29-168">Go toohello Applications tab of your Azure Active Directory.</span></span> <span data-ttu-id="f0b29-169">您會發現 Microsoft Azure RemoteApp 的項目。</span><span class="sxs-lookup"><span data-stu-id="f0b29-169">You will find an entry for Microsoft Azure RemoteApp.</span></span> <span data-ttu-id="f0b29-170">如果您按一下該應用程式，然後設定時，您會看到 hello 頁面下方，您可以啟用 MFA，此應用程式。</span><span class="sxs-lookup"><span data-stu-id="f0b29-170">If you click that application and then configure, you will see hello page below where you can enable MFA for this application.</span></span>

![啟用 MFA][3]

## <a name="audit-user-activity-with-azure-active-directory-premium"></a><span data-ttu-id="f0b29-172">使用 Azure Active Directory Premium 稽核使用者活動</span><span class="sxs-lookup"><span data-stu-id="f0b29-172">Audit user activity with Azure Active Directory Premium</span></span>
<span data-ttu-id="f0b29-173">如果您沒有 Azure AD Premium，則必須 tooturn 它在 hello 授權您的目錄區段。</span><span class="sxs-lookup"><span data-stu-id="f0b29-173">If you do not have Azure AD Premium, then you have tooturn it on in hello Licenses section of your directory.</span></span> <span data-ttu-id="f0b29-174">已啟用 Premium，您可以將使用者指派給 toohello Premium 層級。</span><span class="sxs-lookup"><span data-stu-id="f0b29-174">With Premium enabled, you can assign users toohello Premium level.</span></span>

<span data-ttu-id="f0b29-175">當您移 tooa 使用者在 Azure Active Directory 中時，您可以前往 toohello 活動索引標籤 toosee 登入資訊 tooAzure RemoteApp。</span><span class="sxs-lookup"><span data-stu-id="f0b29-175">When you go tooa user in your Azure Active Directory, you can then go toohello Activity tab toosee login information tooAzure RemoteApp.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f0b29-176">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f0b29-176">Next steps</span></span>
<span data-ttu-id="f0b29-177">完成上述步驟的所有 hello 之後, 您將無法 toorun hello Azure RemoteApp 的用戶端與登入與指派的使用者。</span><span class="sxs-lookup"><span data-stu-id="f0b29-177">After completing all hello above steps, you will be able toorun hello Azure RemoteApp client and log-in with an assigned user.</span></span> <span data-ttu-id="f0b29-178">您會做為其中一個應用程式提供使用 SSMS，而且它存取 tooAzure SQL server 電腦上安裝時執行它。</span><span class="sxs-lookup"><span data-stu-id="f0b29-178">You will be presented with SSMS as one of your applications, and you can run it as you would if it were installed on your computer with access tooAzure SQL server.</span></span>

<span data-ttu-id="f0b29-179">如需有關如何 toomake hello 連接 tooSQL 資料庫的詳細資訊，請參閱[連接 SQL Server Management Studio tooSQL 資料庫及執行範例 T-SQL 查詢](sql-database-connect-query-ssms.md)。</span><span class="sxs-lookup"><span data-stu-id="f0b29-179">For more information on how toomake hello connection tooSQL Database, see [Connect tooSQL Database with SQL Server Management Studio and perform a sample T-SQL query](sql-database-connect-query-ssms.md).</span></span>

<span data-ttu-id="f0b29-180">以上為目前的所有內容。</span><span class="sxs-lookup"><span data-stu-id="f0b29-180">That's everything for now.</span></span> <span data-ttu-id="f0b29-181">盡情享受！</span><span class="sxs-lookup"><span data-stu-id="f0b29-181">Enjoy!</span></span>

<!--Image references-->
[1]: ./media/sql-database-ssms-remoteapp/ssms.png
[2]: ./media/sql-database-ssms-remoteapp/newcloudcollection.png
[3]: ./media/sql-database-ssms-remoteapp/mfa.png
[4]: ./media/sql-database-ssms-remoteapp/allowazure.png
[5]: ./media/sql-database-ssms-remoteapp/publish.png
[6]: ./media/sql-database-ssms-remoteapp/user.png