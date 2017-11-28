---
title: "aaaConnect tooon 內部部署 SQL Server，從使用混合式連線的 Azure App Service 中的 web 應用程式"
description: "Microsoft Azure 上建立 web 應用程式並將它連接 tooan 在內部部署 SQL Server 資料庫"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: mollybos
ms.assetid: 2b4e0539-1a0b-4aa1-8a69-b4b053c3b2e5
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/09/2016
ms.author: cephalin
ms.openlocfilehash: 2e8f8f7e0b9733cfb0433697615faba4358c6023
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooon-premises-sql-server-from-a-web-app-in-azure-app-service-using-hybrid-connections"></a><span data-ttu-id="486f7-103">從使用混合式連線的 Azure App Service 中的 web 應用程式連接 tooon 內部部署 SQL Server</span><span class="sxs-lookup"><span data-stu-id="486f7-103">Connect tooon-premises SQL Server from a web app in Azure App Service using Hybrid Connections</span></span>
<span data-ttu-id="486f7-104">混合式連線可以連接[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web 應用程式使用靜態 TCP 連接埠的 tooon 內部部署資源。</span><span class="sxs-lookup"><span data-stu-id="486f7-104">Hybrid Connections can connect [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web Apps tooon-premises resources that use a static TCP port.</span></span> <span data-ttu-id="486f7-105">支援的資源包括 Microsoft SQL Server、MySQL、HTTP Web API、App Service 和大部分的自訂 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="486f7-105">Supported resources include Microsoft SQL Server, MySQL, HTTP Web APIs, App Service, and most custom Web Services.</span></span>

<span data-ttu-id="486f7-106">在本教學課程中，您將學習如何 toocreate App Service web 應用程式在 hello [Azure 入口網站](http://go.microsoft.com/fwlink/?LinkId=529715)連接 hello web 應用程式 tooyour 本機內部部署 SQL Server 資料庫使用 hello 新混合式連線功能，建立簡單的 ASP.NET將會使用 hello 混合式連接，並部署 hello 應用程式 toohello App Service web 應用程式的應用程式。</span><span class="sxs-lookup"><span data-stu-id="486f7-106">In this tutorial, you will learn how toocreate an App Service web app in hello [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715), connect hello web app tooyour local on-premises SQL Server database using hello new Hybrid Connection feature, create a simple ASP.NET application that will use hello hybrid connection, and deploy hello application toohello App Service web app.</span></span> <span data-ttu-id="486f7-107">在 Azure 上的 hello 完成 web 應用程式是在內部部署的成員資格資料庫中儲存使用者認證。</span><span class="sxs-lookup"><span data-stu-id="486f7-107">hello completed web app on Azure stores user credentials in a membership database that is on-premises.</span></span> <span data-ttu-id="486f7-108">hello 教學課程會假設沒有使用經驗，使用 Azure 或 ASP.NET。</span><span class="sxs-lookup"><span data-stu-id="486f7-108">hello tutorial assumes no prior experience using Azure or ASP.NET.</span></span>

> [!NOTE]
> <span data-ttu-id="486f7-109">如果您想 tooget 之前註冊 Azure 帳戶與 Azure 應用程式服務啟動時，請移至太[再試一次應用程式服務](https://azure.microsoft.com/try/app-service/)，可以立即存留較短的入門的 web 應用程式中建立應用程式服務。</span><span class="sxs-lookup"><span data-stu-id="486f7-109">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="486f7-110">不需要信用卡；沒有承諾。</span><span class="sxs-lookup"><span data-stu-id="486f7-110">No credit cards required; no commitments.</span></span>
> 
> <span data-ttu-id="486f7-111">hello 混合式連線功能 hello Web 應用程式部分是只用於 hello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="486f7-111">hello Web Apps portion of hello Hybrid Connections feature is available only in hello [Azure Portal](https://portal.azure.com).</span></span> <span data-ttu-id="486f7-112">請參閱 toocreate BizTalk 服務中的連接[混合式連線](http://go.microsoft.com/fwlink/p/?LinkID=397274)。</span><span class="sxs-lookup"><span data-stu-id="486f7-112">toocreate a connection in BizTalk Services, see [Hybrid Connections](http://go.microsoft.com/fwlink/p/?LinkID=397274).</span></span>  
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="486f7-113">必要條件</span><span class="sxs-lookup"><span data-stu-id="486f7-113">Prerequisites</span></span>
<span data-ttu-id="486f7-114">toocomplete 本教學課程中，您將需要下列產品的 hello。</span><span class="sxs-lookup"><span data-stu-id="486f7-114">toocomplete this tutorial, you'll need hello following products.</span></span> <span data-ttu-id="486f7-115">所有產品都有免費版本可使用，因此您可以免費進行 Azure 相關開發。</span><span class="sxs-lookup"><span data-stu-id="486f7-115">All are available in free versions, so you can start developing for Azure entirely for free.</span></span>

* <span data-ttu-id="486f7-116">**Azure 訂閱** - 如需免費訂閱，請參閱 [Azure 免費試用](/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="486f7-116">**Azure subscription** - For a free subscription, see [Azure Free Trial](/pricing/free-trial/).</span></span>
* <span data-ttu-id="486f7-117">**Visual Studio 2013** -toodownload 免費試用版的 Visual Studio 2013，請參閱[Visual Studio 下載](http://www.visualstudio.com/downloads/download-visual-studio-vs)。</span><span class="sxs-lookup"><span data-stu-id="486f7-117">**Visual Studio 2013** - toodownload a free trial version of Visual Studio 2013, see [Visual Studio Downloads](http://www.visualstudio.com/downloads/download-visual-studio-vs).</span></span> <span data-ttu-id="486f7-118">請先安裝此項目再繼續作業。</span><span class="sxs-lookup"><span data-stu-id="486f7-118">Install this before continuing.</span></span>
* <span data-ttu-id="486f7-119">**Microsoft .NET Framework 3.5 Service Pack 1** - 如果您的作業系統是 Windows 8.1、Windows Server 2012 R2、Windows 8、Windows Server 2012、Windows 7 或 Windows Server 2008 R2，您可以在 [控制台] > [程式和功能] > [開啟或關閉 Windows 功能] 中啟用此項目。</span><span class="sxs-lookup"><span data-stu-id="486f7-119">**Microsoft .NET Framework 3.5 Service Pack 1** - If your operating system is Windows 8.1, Windows Server 2012 R2, Windows 8, Windows Server 2012, Windows 7, or Windows Server 2008 R2, you can enable this in Control Panel > Programs and Features > Turn Windows features on or off.</span></span> <span data-ttu-id="486f7-120">否則，您可以從下載 hello [Microsoft Download Center](http://www.microsoft.com/download/en/details.aspx?displaylang=en&id=22)。</span><span class="sxs-lookup"><span data-stu-id="486f7-120">Otherwise, you can download it from hello [Microsoft Download Center](http://www.microsoft.com/download/en/details.aspx?displaylang=en&id=22).</span></span>
* <span data-ttu-id="486f7-121">**SQL Server 2014 Express with Tools** -Microsoft SQL Server Express 免費下載在 hello [Microsoft Web 平台的資料庫頁面](http://www.microsoft.com/web/platform/database.aspx)。</span><span class="sxs-lookup"><span data-stu-id="486f7-121">**SQL Server 2014 Express with Tools** - download Microsoft SQL Server Express for free at hello [Microsoft Web Platform Database page](http://www.microsoft.com/web/platform/database.aspx).</span></span> <span data-ttu-id="486f7-122">選擇 hello **Express** (不是 LocalDB) 版本。</span><span class="sxs-lookup"><span data-stu-id="486f7-122">Choose hello **Express** (not LocalDB) version.</span></span> <span data-ttu-id="486f7-123">hello **Express with Tools**版本包含 SQL Server Management Studio，您將在本教學課程中使用。</span><span class="sxs-lookup"><span data-stu-id="486f7-123">hello **Express with Tools** version includes SQL Server Management Studio, which you will use in this tutorial.</span></span>
* <span data-ttu-id="486f7-124">**SQL Server Management Studio Express** -這是使用上面所提下載工具隨附於 SQL Server 2014 Express hello 但如果您需要 tooinstall 它分開，您可以下載並安裝從 hello [SQL Server Express下載頁面](http://www.microsoft.com/web/platform/database.aspx)。</span><span class="sxs-lookup"><span data-stu-id="486f7-124">**SQL Server Management Studio Express** - This is included with hello SQL Server 2014 Express with Tools download mentioned above, but if you need tooinstall it separately, you can download and install it from hello [SQL Server Express download page](http://www.microsoft.com/web/platform/database.aspx).</span></span>

<span data-ttu-id="486f7-125">hello 教學課程假設您有 Azure 訂閱，您已安裝 Visual Studio 2013，以及您已安裝或啟用.NET Framework 3.5。</span><span class="sxs-lookup"><span data-stu-id="486f7-125">hello tutorial assumes that you have an Azure subscription, that you have installed Visual Studio 2013, and that you have installed or enabled .NET Framework 3.5.</span></span> <span data-ttu-id="486f7-126">hello 教學課程會示範 tooinstall SQL Server 2014 Express 中的設定，適用於 hello Azure 混合式連線功能 （使用靜態 TCP 連接埠的預設執行個體） 的方式。</span><span class="sxs-lookup"><span data-stu-id="486f7-126">hello tutorial shows you how tooinstall SQL Server 2014 Express in a configuration that works well with hello Azure Hybrid Connections feature (a default instance with a static TCP port).</span></span> <span data-ttu-id="486f7-127">開始之前 hello 教學課程，請從上面所述，如果您沒有安裝 SQL Server 的 hello 位置下載 SQL Server 2014 Express with Tools。</span><span class="sxs-lookup"><span data-stu-id="486f7-127">Before starting hello tutorial, download SQL Server 2014 Express with Tools from hello location mentioned above if you do not have SQL Server installed.</span></span>

### <a name="notes"></a><span data-ttu-id="486f7-128">注意事項</span><span class="sxs-lookup"><span data-stu-id="486f7-128">Notes</span></span>
<span data-ttu-id="486f7-129">toouse 在內部部署 SQL Server 或 SQL Server Express 的混合式連接的資料庫，TCP/IP 需要 toobe 靜態連接埠上啟用。</span><span class="sxs-lookup"><span data-stu-id="486f7-129">toouse an on-premises SQL Server or SQL Server Express database with a hybrid connection, TCP/IP needs toobe enabled on a static port.</span></span> <span data-ttu-id="486f7-130">SQL Server 上的預設執行個體會使用靜態連接埠 1433，但指定的執行個體則否。</span><span class="sxs-lookup"><span data-stu-id="486f7-130">Default instances on SQL Server use static port 1433, whereas named instances do not.</span></span>

<span data-ttu-id="486f7-131">您安裝代理程式 」 在內部部署混合式連線管理員 hello hello 電腦：</span><span class="sxs-lookup"><span data-stu-id="486f7-131">hello computer on which you install hello on-premises Hybrid Connection Manager agent:</span></span>

* <span data-ttu-id="486f7-132">必須在有傳出連線 tooAzure:</span><span class="sxs-lookup"><span data-stu-id="486f7-132">Must have outbound connectivity tooAzure over:</span></span>

| <span data-ttu-id="486f7-133">Port</span><span class="sxs-lookup"><span data-stu-id="486f7-133">Port</span></span> | <span data-ttu-id="486f7-134">理由</span><span class="sxs-lookup"><span data-stu-id="486f7-134">Why</span></span> |
| --- | --- |
| <span data-ttu-id="486f7-135">80</span><span class="sxs-lookup"><span data-stu-id="486f7-135">80</span></span> |<span data-ttu-id="486f7-136">**必要** 可供 HTTP 連接埠進行憑證驗證以及可供進行資料連線 (選用)。</span><span class="sxs-lookup"><span data-stu-id="486f7-136">**Required** for HTTP port for certificate validation and optionally for data connectivity.</span></span> |
| <span data-ttu-id="486f7-137">443</span><span class="sxs-lookup"><span data-stu-id="486f7-137">443</span></span> |<span data-ttu-id="486f7-138">**選用** 可供進行資料連線。</span><span class="sxs-lookup"><span data-stu-id="486f7-138">**Optional** for data connectivity.</span></span> <span data-ttu-id="486f7-139">如果無法使用輸出連線 too443 時，會使用 TCP 連接埠 80。</span><span class="sxs-lookup"><span data-stu-id="486f7-139">If outbound connectivity too443 is unavailable, TCP port 80 is used.</span></span> |
| <span data-ttu-id="486f7-140">5671 和 9352</span><span class="sxs-lookup"><span data-stu-id="486f7-140">5671 and 9352</span></span> |<span data-ttu-id="486f7-141">**建議** 但可供進行資料連線 (選用)。</span><span class="sxs-lookup"><span data-stu-id="486f7-141">**Recommended** but Optional for data connectivity.</span></span> <span data-ttu-id="486f7-142">請注意，此模式通常會產生較高的輸送量。</span><span class="sxs-lookup"><span data-stu-id="486f7-142">Note this mode usually yields higher throughput.</span></span> <span data-ttu-id="486f7-143">如果無法使用輸出連線 toothese 連接埠，則會使用 TCP 連接埠 443。</span><span class="sxs-lookup"><span data-stu-id="486f7-143">If outbound connectivity toothese ports is unavailable, TCP port 443 is used.</span></span> |

* <span data-ttu-id="486f7-144">必須是能夠 tooreach hello *hostname*:*portnumber*的內部部署資源。</span><span class="sxs-lookup"><span data-stu-id="486f7-144">Must be able tooreach hello *hostname*:*portnumber* of your on-premises resource.</span></span>

<span data-ttu-id="486f7-145">本文章中的 hello 步驟假設您使用 hello 瀏覽器從 hello 主控 hello 在內部部署混合式連接的代理程式的電腦。</span><span class="sxs-lookup"><span data-stu-id="486f7-145">hello steps in this article assume that you are using hello browser from hello computer that will host hello on-premises hybrid connection agent.</span></span>

<span data-ttu-id="486f7-146">如果您已符合上面所述的 hello 條件的環境和組態中安裝 SQL Server，您可以三級跳，而且開頭[建立 SQL Server 資料庫內部](#CreateSQLDB)。</span><span class="sxs-lookup"><span data-stu-id="486f7-146">If you already have SQL Server installed in a configuration and in an environment that meets hello conditions described above, you can skip ahead and start with [Create a SQL Server database on-premises](#CreateSQLDB).</span></span>

<a name="InstallSQL"></a>

## <a name="a-install-sql-server-express-enable-tcpip-and-create-a-sql-server-database-on-premises"></a><span data-ttu-id="486f7-147">A.</span><span class="sxs-lookup"><span data-stu-id="486f7-147">A.</span></span> <span data-ttu-id="486f7-148">在內部部署中安裝 SQL Server Express、啟用 TCP/IP 及建立 SQL Server 資料庫</span><span class="sxs-lookup"><span data-stu-id="486f7-148">Install SQL Server Express, enable TCP/IP, and create a SQL Server database on-premises</span></span>
<span data-ttu-id="486f7-149">這個區段會顯示 SQL Server Express，tooinstall 如何啟用 TCP/IP，和建立資料庫，以便您的 web 應用程式會處理 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="486f7-149">This section shows you how tooinstall SQL Server Express, enable TCP/IP, and create a database so that your web application will work with hello Azure Portal.</span></span>

### <a name="install-sql-server-express"></a><span data-ttu-id="486f7-150">安裝 SQL Server Express</span><span class="sxs-lookup"><span data-stu-id="486f7-150">Install SQL Server Express</span></span>
1. <span data-ttu-id="486f7-151">tooinstall SQL Server Express，執行 hello **SQLEXPRWT_x64_ENU.exe**或**SQLEXPR_x86_ENU.exe**您下載的檔案。</span><span class="sxs-lookup"><span data-stu-id="486f7-151">tooinstall SQL Server Express, run hello **SQLEXPRWT_x64_ENU.exe** or **SQLEXPR_x86_ENU.exe** file that you downloaded.</span></span> <span data-ttu-id="486f7-152">hello SQL Server 安裝中心精靈 隨即出現。</span><span class="sxs-lookup"><span data-stu-id="486f7-152">hello SQL Server Installation Center wizard appears.</span></span>
   
    ![SQL Server Install][SQLServerInstall]
2. <span data-ttu-id="486f7-154">選擇**新的 SQL Server 獨立安裝或加入現有安裝的功能 tooan**。</span><span class="sxs-lookup"><span data-stu-id="486f7-154">Choose **New SQL Server stand-alone installation or add features tooan existing installation**.</span></span> <span data-ttu-id="486f7-155">Hello 的指示，直到取得 toohello 接受 hello 預設選項及設定，請依照下列**執行個體組態**頁面。</span><span class="sxs-lookup"><span data-stu-id="486f7-155">Follow hello instructions, accepting hello default choices and settings, until you get toohello **Instance Configuration** page.</span></span>
3. <span data-ttu-id="486f7-156">在 hello**執行個體組態**頁面上，選擇**預設執行個體**。</span><span class="sxs-lookup"><span data-stu-id="486f7-156">On hello **Instance Configuration** page, choose **Default instance**.</span></span>
   
    ![Choose Default Instance][ChooseDefaultInstance]
   
    <span data-ttu-id="486f7-158">根據預設，SQL Server hello 預設執行個體會靜態通訊埠 1433，SQL Server 用戶端要求是混合式連線功能需要什麼 hello。</span><span class="sxs-lookup"><span data-stu-id="486f7-158">By default, hello default instance of SQL Server listens for requests from SQL Server clients on static port 1433, which is what hello Hybrid Connections feature requires.</span></span> <span data-ttu-id="486f7-159">指定的執行個體會使用動態連接埠和 UDP，而混合式連線並不加以支援。</span><span class="sxs-lookup"><span data-stu-id="486f7-159">Named instances use dynamic ports and UDP, which are not supported by Hybrid Connections.</span></span>
4. <span data-ttu-id="486f7-160">接受 hello 預設值在 hello**伺服器組態**頁面。</span><span class="sxs-lookup"><span data-stu-id="486f7-160">Accept hello defaults on hello **Server Configuration** page.</span></span>
5. <span data-ttu-id="486f7-161">在 hello**資料庫引擎組態**頁面的 **驗證模式**，選擇**混合模式 （SQL Server 驗證和 Windows 驗證）**，並提供密碼。</span><span class="sxs-lookup"><span data-stu-id="486f7-161">On hello **Database Engine Configuration** page, under **Authentication Mode**, choose **Mixed Mode (SQL Server authentication and Windows authentication)**, and provide a password.</span></span>
   
    ![Choose Mixed Mode][ChooseMixedMode]
   
    <span data-ttu-id="486f7-163">在本教學課程中，您將使用 SQL Server 驗證。</span><span class="sxs-lookup"><span data-stu-id="486f7-163">In this tutorial, you will be using SQL Server authentication.</span></span> <span data-ttu-id="486f7-164">是您所提供，確定 tooremember hello 密碼，因為您稍後會需要。</span><span class="sxs-lookup"><span data-stu-id="486f7-164">Be sure tooremember hello password that you provide, because you will need it later.</span></span>
6. <span data-ttu-id="486f7-165">逐步執行 hello 精靈 toocomplete hello 安裝 hello 其餘部分。</span><span class="sxs-lookup"><span data-stu-id="486f7-165">Step through hello rest of hello wizard toocomplete hello installation.</span></span>

### <a name="enable-tcpip"></a><span data-ttu-id="486f7-166">啟用 TCP/IP</span><span class="sxs-lookup"><span data-stu-id="486f7-166">Enable TCP/IP</span></span>
<span data-ttu-id="486f7-167">tooenable TCP/IP，您將使用 SQL Server 組態管理員，當您安裝 SQL Server Express 安裝。</span><span class="sxs-lookup"><span data-stu-id="486f7-167">tooenable TCP/IP, you will use SQL Server Configuration Manager, which was installed when you installed SQL Server Express.</span></span> <span data-ttu-id="486f7-168">中的 hello 步驟[啟用 TCP/IP 網路通訊協定的 SQL Server](http://technet.microsoft.com/library/hh231672%28v=sql.110%29.aspx)才能繼續。</span><span class="sxs-lookup"><span data-stu-id="486f7-168">Follow hello steps in [Enable TCP/IP Network Protocol for SQL Server](http://technet.microsoft.com/library/hh231672%28v=sql.110%29.aspx) before continuing.</span></span>

<a name="CreateSQLDB"></a>

### <a name="create-a-sql-server-database-on-premises"></a><span data-ttu-id="486f7-169">在內部部署中建立 SQL Server 資料庫</span><span class="sxs-lookup"><span data-stu-id="486f7-169">Create a SQL Server database on-premises</span></span>
<span data-ttu-id="486f7-170">您的 Visual Studio Web 應用程式需要可由 Azure 存取的成員資格資料庫。</span><span class="sxs-lookup"><span data-stu-id="486f7-170">Your Visual Studio web application requires a membership database that can be accessed by Azure.</span></span> <span data-ttu-id="486f7-171">這需要 SQL Server 或 SQL Server Express 資料庫 （不 hello LocalDB 資料庫 hello MVC 範本會依預設），讓您將接著建立 hello 成員資格資料庫。</span><span class="sxs-lookup"><span data-stu-id="486f7-171">This requires a SQL Server or SQL Server Express database (not hello LocalDB database that hello MVC template uses by default), so you'll create hello membership database next.</span></span>

1. <span data-ttu-id="486f7-172">在 SQL Server Management Studio 中，連接 toohello 您剛才安裝的 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="486f7-172">In SQL Server Management Studio, connect toohello SQL Server you just installed.</span></span> <span data-ttu-id="486f7-173">(如果 hello**連接 tooServer**對話方塊不會不會自動出現，瀏覽過**物件總管] 中**hello 左窗格中，按一下 [**連接**，然後按一下 **Database Engine**。)![連接 tooServer][SSMSConnectToServer]</span><span class="sxs-lookup"><span data-stu-id="486f7-173">(If hello **Connect tooServer** dialog does not appear automatically, navigate too**Object Explorer** in hello left pane, click **Connect**, and then click **Database Engine**.) ![Connect tooServer][SSMSConnectToServer]</span></span>
   
    <span data-ttu-id="486f7-174">針對 [伺服器類型]，選擇 [資料庫引擎]。</span><span class="sxs-lookup"><span data-stu-id="486f7-174">For **Server type**, choose **Database Engine**.</span></span> <span data-ttu-id="486f7-175">如**伺服器名稱**，您可以使用**localhost**或 hello 您所使用的 hello 電腦名稱。</span><span class="sxs-lookup"><span data-stu-id="486f7-175">For **Server name**, you can use **localhost** or hello name of hello computer that you are using.</span></span> <span data-ttu-id="486f7-176">選擇**SQL Server 驗證**，然後 hello sa 使用者名稱和密碼登入 hello 您稍早建立的。</span><span class="sxs-lookup"><span data-stu-id="486f7-176">Choose **SQL Server authentication**, and then log in with hello sa user name and hello password that you created earlier.</span></span>
2. <span data-ttu-id="486f7-177">toocreate 新的資料庫使用 SQL Server Management Studio，以滑鼠右鍵按一下**資料庫**在物件總管 中，，然後按一下**新資料庫**。</span><span class="sxs-lookup"><span data-stu-id="486f7-177">toocreate a new database by using SQL Server Management Studio, right-click **Databases** in Object Explorer, and then click **New Database**.</span></span>
   
    ![Create new database][SSMScreateNewDB]
3. <span data-ttu-id="486f7-179">在 hello**新資料庫** 對話方塊中，輸入 MembershipDB hello 資料庫名稱，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="486f7-179">In hello **New Database** dialog, enter MembershipDB for hello database name, and then click **OK**.</span></span>
   
    ![Provide database name][SSMSprovideDBname]
   
    <span data-ttu-id="486f7-181">請注意，您不做任何變更 toohello 資料庫此時。</span><span class="sxs-lookup"><span data-stu-id="486f7-181">Note that you do not make any changes toohello database at this point.</span></span> <span data-ttu-id="486f7-182">在執行時，則將 web 應用程式所自動更新版本加入 hello 成員資格資訊。</span><span class="sxs-lookup"><span data-stu-id="486f7-182">hello membership information will be added automatically later by your web application when you run it.</span></span>
4. <span data-ttu-id="486f7-183">在 [物件總管] 中，如果您展開**資料庫**，您會看到已建立該 hello 成員資格資料庫。</span><span class="sxs-lookup"><span data-stu-id="486f7-183">In Object Explorer, if you expand **Databases**, you will see that hello membership database has been created.</span></span>
   
    ![MembershipDB created][SSMSMembershipDBCreated]

<a name="CreateSite"></a>

## <a name="b-create-a-web-app-in-hello-azure-portal"></a><span data-ttu-id="486f7-185">B.</span><span class="sxs-lookup"><span data-stu-id="486f7-185">B.</span></span> <span data-ttu-id="486f7-186">在 hello Azure 入口網站中建立 web 應用程式</span><span class="sxs-lookup"><span data-stu-id="486f7-186">Create a web app in hello Azure Portal</span></span>
> [!NOTE]
> <span data-ttu-id="486f7-187">如果您已經在 hello 的 toouse 本教學課程中的 Azure 入口網站中建立 web 應用程式，您可以向前跳過[建立混合式連接和 BizTalk 服務](#CreateHC)並從該處繼續。</span><span class="sxs-lookup"><span data-stu-id="486f7-187">If you have already created a web app in hello Azure Portal that you want toouse for this tutorial, you can skip ahead too[Create a Hybrid Connection and a BizTalk Service](#CreateHC) and continue from there.</span></span>
> 
> 

1. <span data-ttu-id="486f7-188">在 hello [Azure 入口網站](https://portal.azure.com)，按一下 **新增** > **Web + 行動** > **Web 應用程式**。</span><span class="sxs-lookup"><span data-stu-id="486f7-188">In hello [Azure Portal](https://portal.azure.com), click **New** > **Web + Mobile** > **Web app**.</span></span>
   
    ![New button][New]
2. <span data-ttu-id="486f7-190">設定您的 Web 應用程式，然後按一下建立 。</span><span class="sxs-lookup"><span data-stu-id="486f7-190">Configure your web app, and then click **Create**.</span></span>
   
    ![Website name][WebsiteCreationBlade]
3. <span data-ttu-id="486f7-192">在幾分鐘之後, 建立 hello web 應用程式和其 web 應用程式 刀鋒視窗隨即出現。</span><span class="sxs-lookup"><span data-stu-id="486f7-192">After a few moments, hello web app is created and its web app blade appears.</span></span> <span data-ttu-id="486f7-193">hello 刀鋒視窗中是可垂直捲動的儀表板可讓您管理您的 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="486f7-193">hello blade is a vertically scrollable dashboard that lets you manage your web app.</span></span>
   
    ![Website running][WebSiteRunningBlade]
   
    <span data-ttu-id="486f7-195">是即時的 tooverify hello web 應用程式，您可以按一下 hello**瀏覽**圖示 toodisplay hello 預設頁面。</span><span class="sxs-lookup"><span data-stu-id="486f7-195">tooverify hello web app is live, you can click hello **Browse** icon toodisplay hello default page.</span></span>

<span data-ttu-id="486f7-196">接下來，您將建立混合式連接和 hello web 應用程式的 BizTalk 服務。</span><span class="sxs-lookup"><span data-stu-id="486f7-196">Next, you will create a hybrid connection and a BizTalk service for hello web app.</span></span>

<a name="CreateHC"></a>

## <a name="c-create-a-hybrid-connection-and-a-biztalk-service"></a><span data-ttu-id="486f7-197">C.</span><span class="sxs-lookup"><span data-stu-id="486f7-197">C.</span></span> <span data-ttu-id="486f7-198">建立混合式連線和 BizTalk 服務</span><span class="sxs-lookup"><span data-stu-id="486f7-198">Create a Hybrid Connection and a BizTalk Service</span></span>
1. <span data-ttu-id="486f7-199">傳回在 hello 入口網站，請移 toosettings，然後按一下**網路** > **設定您的混合式連接端點**。</span><span class="sxs-lookup"><span data-stu-id="486f7-199">Back in hello Portal, go toosettings and click **Networking** > **Configure your hybrid connection endpoints**.</span></span>
   
    ![混合式連線][CreateHCHCIcon]
2. <span data-ttu-id="486f7-201">在 hello 混合式連線刀鋒視窗中，按一下 **新增** > **新混合式連接**。</span><span class="sxs-lookup"><span data-stu-id="486f7-201">On hello Hybrid connections blade, click **Add** > **New hybrid connection**.</span></span>
3. <span data-ttu-id="486f7-202">在 hello**建立混合式連接**刀鋒視窗中：</span><span class="sxs-lookup"><span data-stu-id="486f7-202">On hello **Create hybrid connection** blade:</span></span>
   
   * <span data-ttu-id="486f7-203">如**名稱**，提供 hello 連接的名稱。</span><span class="sxs-lookup"><span data-stu-id="486f7-203">For **Name**, provide a name for hello connection.</span></span>
   * <span data-ttu-id="486f7-204">如**Hostname**，輸入您的 SQL Server 主機電腦 hello 電腦名稱。</span><span class="sxs-lookup"><span data-stu-id="486f7-204">For **Hostname**, enter hello computer name of your SQL Server host computer.</span></span>
   * <span data-ttu-id="486f7-205">如**連接埠**，輸入 1433 (hello 預設 SQL Server 連接埠）。</span><span class="sxs-lookup"><span data-stu-id="486f7-205">For **Port**, enter 1433 (hello default port for SQL Server).</span></span>
   * <span data-ttu-id="486f7-206">按一下**BizTalk 服務** > **新的 BizTalk 服務**，然後輸入 hello BizTalk 服務的名稱。</span><span class="sxs-lookup"><span data-stu-id="486f7-206">Click **BizTalk Service** > **New BizTalk Service** and enter a name for hello BizTalk service.</span></span>
     
     ![Create a hybrid connection][TwinCreateHCBlades]
4. <span data-ttu-id="486f7-208">按兩次 [確定]  。</span><span class="sxs-lookup"><span data-stu-id="486f7-208">Click **OK** twice.</span></span>
   
    <span data-ttu-id="486f7-209">Hello 程序完成時，hello**通知**區域將會閃爍綠色**成功**和 hello**混合式連接**刀鋒視窗會顯示以 hello 新混合式連接hello 狀態為**未連接**。</span><span class="sxs-lookup"><span data-stu-id="486f7-209">When hello process completes, hello **Notifications** area will flash a green **SUCCESS** and hello **Hybrid connection** blade will show hello new hybrid connection with hello status as **Not connected**.</span></span>
   
    ![One hybrid connection created][CreateHCOneConnectionCreated]

<span data-ttu-id="486f7-211">此時，您已完成 hello 雲端混合式連接的基礎結構的重要部分。</span><span class="sxs-lookup"><span data-stu-id="486f7-211">At this point, you have completed an important part of hello cloud hybrid connection infrastructure.</span></span> <span data-ttu-id="486f7-212">接下來，您將建立對應的內部部署部分。</span><span class="sxs-lookup"><span data-stu-id="486f7-212">Next, you will create a corresponding on-premises piece.</span></span>

<a name="InstallHCM"></a>

## <a name="d-install-hello-on-premises-hybrid-connection-manager-toocomplete-hello-connection"></a><span data-ttu-id="486f7-213">D.</span><span class="sxs-lookup"><span data-stu-id="486f7-213">D.</span></span> <span data-ttu-id="486f7-214">安裝 hello 在內部部署混合式連線管理員 toocomplete hello 連線</span><span class="sxs-lookup"><span data-stu-id="486f7-214">Install hello on-premises Hybrid Connection Manager toocomplete hello connection</span></span>
[!INCLUDE [app-service-hybrid-connections-manager-install](../../includes/app-service-hybrid-connections-manager-install.md)]

<span data-ttu-id="486f7-215">現在該 hello 混合式連接基礎結構已完成，您將建立 web 應用程式使用它。</span><span class="sxs-lookup"><span data-stu-id="486f7-215">Now that hello hybrid connection infrastructure is complete, you will create a web application that uses it.</span></span>

<a name="CreateASPNET"></a>

## <a name="e-create-a-basic-aspnet-web-project-edit-hello-database-connection-string-and-run-hello-project-locally"></a><span data-ttu-id="486f7-216">E.</span><span class="sxs-lookup"><span data-stu-id="486f7-216">E.</span></span> <span data-ttu-id="486f7-217">建立基本的 ASP.NET web 專案、 編輯 hello 資料庫連接字串，並在本機執行 hello 專案</span><span class="sxs-lookup"><span data-stu-id="486f7-217">Create a basic ASP.NET web project, edit hello database connection string, and run hello project locally</span></span>
### <a name="create-a-basic-aspnet-project"></a><span data-ttu-id="486f7-218">建立基本 ASP.NET 專案</span><span class="sxs-lookup"><span data-stu-id="486f7-218">Create a basic ASP.NET project</span></span>
1. <span data-ttu-id="486f7-219">在 Visual Studio 中的 hello**檔案**功能表上，建立新的專案：</span><span class="sxs-lookup"><span data-stu-id="486f7-219">In Visual Studio, on hello **File** menu, create a new Project:</span></span>
   
    ![New Visual Studio project][HCVSNewProject]
2. <span data-ttu-id="486f7-221">在 hello**範本**hello 區段**新專案**對話方塊中，選取**Web**選擇**ASP.NET Web 應用程式**，然後按一下 **確定**。</span><span class="sxs-lookup"><span data-stu-id="486f7-221">In hello **Templates** section of hello **New Project** dialog, select **Web** and choose **ASP.NET Web Application**, and then click **OK**.</span></span>
   
    ![Choose ASP.NET Web Application][HCVSChooseASPNET]
3. <span data-ttu-id="486f7-223">在 hello**新增 ASP.NET 專案** 對話方塊中，選擇**MVC**，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="486f7-223">In hello **New ASP.NET Project** dialog, choose **MVC**, and then click **OK**.</span></span>
   
    ![Choose MVC][HCVSChooseMVC]
4. <span data-ttu-id="486f7-225">Hello 專案建立後，會顯示 hello 應用程式讀我檔案頁面。</span><span class="sxs-lookup"><span data-stu-id="486f7-225">When hello project has been created, hello application readme page appears.</span></span> <span data-ttu-id="486f7-226">請勿執行 hello web 專案。</span><span class="sxs-lookup"><span data-stu-id="486f7-226">Do not run hello web project yet.</span></span>
   
    ![Readme page][HCVSReadmePage]

### <a name="edit-hello-database-connection-string-for-hello-application"></a><span data-ttu-id="486f7-228">編輯 hello hello 應用程式的資料庫連接字串</span><span class="sxs-lookup"><span data-stu-id="486f7-228">Edit hello database connection string for hello application</span></span>
<span data-ttu-id="486f7-229">在此步驟中，您可以編輯 hello 會告訴您的應用程式的連接字串其中 toofind 本機的 SQL Server Express 資料庫。</span><span class="sxs-lookup"><span data-stu-id="486f7-229">In this step, you edit hello connection string that tells your application where toofind your local SQL Server Express database.</span></span> <span data-ttu-id="486f7-230">hello 連接字串是 hello 應用程式的 Web.config 檔案，其中包含 hello 應用程式的組態資訊。</span><span class="sxs-lookup"><span data-stu-id="486f7-230">hello connection string is in hello application's Web.config file, which contains configuration information for hello application.</span></span>

> [!NOTE]
> <span data-ttu-id="486f7-231">應用程式使用您在 SQL Server Express，並不在 Visual Studio 的預設 LocalDB 一個 hello hello 資料庫的 tooensure，請務必執行您的專案之前完成此步驟。</span><span class="sxs-lookup"><span data-stu-id="486f7-231">tooensure that your application uses hello database that you created in SQL Server Express, and not hello one in Visual Studio's default LocalDB, it is important that you complete this step before running your project.</span></span>
> 
> 

1. <span data-ttu-id="486f7-232">在方案總管 中，按兩下 hello Web.config 檔案。</span><span class="sxs-lookup"><span data-stu-id="486f7-232">In Solution Explorer, double-click hello Web.config file.</span></span>
   
    ![Web.config][HCVSChooseWebConfig]
2. <span data-ttu-id="486f7-234">編輯 hello **connectionStrings**區段 toopoint toohello SQL Server 資料庫在本機電腦，在下列範例中的 hello hello 語法如下：</span><span class="sxs-lookup"><span data-stu-id="486f7-234">Edit hello **connectionStrings** section toopoint toohello SQL Server database on your local machine, following hello syntax in hello following example:</span></span>
   
    ![連接字串][HCVSConnectionString]
   
    <span data-ttu-id="486f7-236">當您在撰寫 hello 連接字串，請注意 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="486f7-236">When composing hello connection string, keep in mind hello following:</span></span>
   
   * <span data-ttu-id="486f7-237">如果您要連接 tooa 具名執行個體，而不是預設執行個體 (例如，YourServer\SQLEXPRESS)，您必須設定您 SQL Server toouse 靜態連接埠。</span><span class="sxs-lookup"><span data-stu-id="486f7-237">If you are connecting tooa named instance instead of a default instance (for example, YourServer\SQLEXPRESS), you must configure your SQL Server toouse static ports.</span></span> <span data-ttu-id="486f7-238">如需設定靜態通訊埠資訊，請參閱[如何 tooconfigure 特定通訊埠上的 SQL Server toolisten](http://support.microsoft.com/kb/823938)。</span><span class="sxs-lookup"><span data-stu-id="486f7-238">For information on configuring static ports, see [How tooconfigure SQL Server toolisten on a specific port](http://support.microsoft.com/kb/823938).</span></span> <span data-ttu-id="486f7-239">根據預設，指定的執行個體會使用 UDP 和動態連接埠，而混合式連線並不加以支援。</span><span class="sxs-lookup"><span data-stu-id="486f7-239">By default, named instances use UDP and dynamic ports, which are not supported by Hybrid Connections.</span></span>
   * <span data-ttu-id="486f7-240">建議您指定 hello hello 連接字串上連接埠 (1433 根據預設，在 hello 範例所示)，使您可以確定您的本機 SQL Server 具有 TCP 已啟用，並且正在使用 hello 正確連接埠。</span><span class="sxs-lookup"><span data-stu-id="486f7-240">It is recommended that you specify hello port (1433 by default, as shown in hello example) on hello connection string so that you can be sure that your local SQL Server has TCP enabled and is using hello correct port.</span></span>
   * <span data-ttu-id="486f7-241">請記住 toouse SQL Server 驗證 tooconnect，指定連接字串中的 hello 使用者識別碼和密碼。</span><span class="sxs-lookup"><span data-stu-id="486f7-241">Remember toouse SQL Server Authentication tooconnect, specifying hello user ID and password in your connection string.</span></span>
3. <span data-ttu-id="486f7-242">按一下**儲存**Visual Studio toosave hello Web.config 檔案中。</span><span class="sxs-lookup"><span data-stu-id="486f7-242">Click **Save** in Visual Studio toosave hello Web.config file.</span></span>

### <a name="run-hello-project-locally-and-register-a-new-user"></a><span data-ttu-id="486f7-243">在本機執行 hello 專案，並註冊新的使用者</span><span class="sxs-lookup"><span data-stu-id="486f7-243">Run hello project locally and register a new user</span></span>
1. <span data-ttu-id="486f7-244">現在，按一下 hello 瀏覽 按鈕，在偵錯在本機執行新的 web 專案。</span><span class="sxs-lookup"><span data-stu-id="486f7-244">Now, run your new web project locally by clicking hello browse button under Debug.</span></span> <span data-ttu-id="486f7-245">此範例使用 Internet Explorer。</span><span class="sxs-lookup"><span data-stu-id="486f7-245">This example uses Internet Explorer.</span></span>
   
    ![Run project][HCVSRunProject]
2. <span data-ttu-id="486f7-247">在 hello 右上方的 hello 預設網頁，選擇 **註冊**tooregister 新的帳戶：</span><span class="sxs-lookup"><span data-stu-id="486f7-247">On hello upper right of hello default web page, choose **Register** tooregister a new account:</span></span>
   
    ![Register a new account][HCVSRegisterLocally]
3. <span data-ttu-id="486f7-249">輸入使用者名稱和密碼：</span><span class="sxs-lookup"><span data-stu-id="486f7-249">Enter a user name and password:</span></span>
   
    ![Enter user name and password][HCVSCreateNewAccount]
   
    <span data-ttu-id="486f7-251">這樣會自動建立資料庫，您會保留您的應用程式的 hello 成員資格資訊的本機 SQL Server 上。</span><span class="sxs-lookup"><span data-stu-id="486f7-251">This automatically creates a database on your local SQL Server that holds hello membership information for your application.</span></span> <span data-ttu-id="486f7-252">其中一個 hello 資料表 (**dbo。AspNetUsers**) 保留 web 應用程式像是 hello 您剛才輸入的使用者認證。</span><span class="sxs-lookup"><span data-stu-id="486f7-252">One of hello tables (**dbo.AspNetUsers**) holds web app user credentials like hello ones that you just entered.</span></span> <span data-ttu-id="486f7-253">您會看到此資料表在 hello 教學課程後面。</span><span class="sxs-lookup"><span data-stu-id="486f7-253">You will see this table later in hello tutorial.</span></span>
4. <span data-ttu-id="486f7-254">關閉 hello 的 hello 預設網頁瀏覽器視窗。</span><span class="sxs-lookup"><span data-stu-id="486f7-254">Close hello browser window of hello default web page.</span></span> <span data-ttu-id="486f7-255">這樣會阻止 Visual Studio 中的 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="486f7-255">This stops hello application in Visual Studio.</span></span>

<span data-ttu-id="486f7-256">您現在準備好進行 hello 下一個步驟，也就是 toopublish hello 應用程式 tooAzure 並進行測試。</span><span class="sxs-lookup"><span data-stu-id="486f7-256">You are now ready for hello next step, which is toopublish hello application tooAzure and test it.</span></span>

<a name="PubNTest"></a>

## <a name="f-publish-hello-web-application-tooazure-and-test-it"></a><span data-ttu-id="486f7-257">F.</span><span class="sxs-lookup"><span data-stu-id="486f7-257">F.</span></span> <span data-ttu-id="486f7-258">發行 hello web 應用程式 tooAzure 並進行測試</span><span class="sxs-lookup"><span data-stu-id="486f7-258">Publish hello web application tooAzure and test it</span></span>
<span data-ttu-id="486f7-259">現在，您將會發行您的應用程式 tooyour App Service web 應用程式，然後 toosee hello 混合式連接您先前設定的方式在本機電腦上的 web 應用程式 toohello 資料庫正在使用的 tooconnect。</span><span class="sxs-lookup"><span data-stu-id="486f7-259">Now, you'll publish your application tooyour App Service web app and then test it toosee how hello hybrid connection you configured earlier is being used tooconnect your web app toohello database on your local machine.</span></span>

### <a name="publish-hello-web-application"></a><span data-ttu-id="486f7-260">發行 hello web 應用程式</span><span class="sxs-lookup"><span data-stu-id="486f7-260">Publish hello web application</span></span>
1. <span data-ttu-id="486f7-261">您可以下載您的 hello hello Azure 入口網站中的 App Service web 應用程式的發行設定檔。</span><span class="sxs-lookup"><span data-stu-id="486f7-261">You can download your publishing profile for hello App Service web app in hello Azure Portal.</span></span> <span data-ttu-id="486f7-262">在 web 應用程式的 hello 刀鋒視窗，按一下 **取得發行設定檔**，然後儲存 hello 檔案 tooyour 電腦。</span><span class="sxs-lookup"><span data-stu-id="486f7-262">On hello blade for your web app, click **Get publish profile**, and then save hello file tooyour computer.</span></span>
   
    ![Download publish profile][PortalDownloadPublishProfile]
   
    <span data-ttu-id="486f7-264">接著，您會將此檔案匯入 Visual Studio Web 應用程式中。</span><span class="sxs-lookup"><span data-stu-id="486f7-264">Next, you will import this file into your Visual Studio web application.</span></span>
2. <span data-ttu-id="486f7-265">在 Visual Studio 中，以滑鼠右鍵按一下方案總管 中的 hello 專案名稱，然後選取**發行**。</span><span class="sxs-lookup"><span data-stu-id="486f7-265">In Visual Studio, right-click hello project name in Solution Explorer and select **Publish**.</span></span>
   
    ![Select publish][HCVSRightClickProjectSelectPublish]
3. <span data-ttu-id="486f7-267">在 [hello**發行 Web** hello] 對話方塊，**設定檔**索引標籤上，選擇**匯入**。</span><span class="sxs-lookup"><span data-stu-id="486f7-267">In hello **Publish Web** dialog, on hello **Profile** tab, choose **Import**.</span></span>
   
    ![Import][HCVSPublishWebDialogImport]
4. <span data-ttu-id="486f7-269">瀏覽 tooyour 下載發行設定檔，加以選取，然後按**確定**。</span><span class="sxs-lookup"><span data-stu-id="486f7-269">Browse tooyour downloaded publishing profile, select it, and then click **OK**.</span></span>
   
    ![瀏覽 tooprofile][HCVSBrowseToImportPubProfile]
5. <span data-ttu-id="486f7-271">您發行的資訊匯入，並顯示 hello 上**連接**hello 對話方塊 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="486f7-271">Your publishing information is imported and displays on hello **Connection** tab of hello dialog.</span></span>
   
    ![Click Publish][HCVSClickPublish]
   
    <span data-ttu-id="486f7-273">按一下 [發行] 。</span><span class="sxs-lookup"><span data-stu-id="486f7-273">Click **Publish**.</span></span>
   
    <span data-ttu-id="486f7-274">當發行完成時，您的瀏覽器將會啟動，並顯示現在熟悉的 ASP.NET 應用程式--，不同之處在於現在是即時 hello Azure 雲端中 ！</span><span class="sxs-lookup"><span data-stu-id="486f7-274">When publishing completes, your browser will launch and show your now familiar ASP.NET application -- except that now it is live in hello Azure cloud!</span></span>

<span data-ttu-id="486f7-275">接下來，您將使用您的即時 web 應用程式 toosee 混合式連線作用中。</span><span class="sxs-lookup"><span data-stu-id="486f7-275">Next, you will use your live web application toosee its Hybrid Connection in action.</span></span>

### <a name="test-hello-completed-web-application-on-azure"></a><span data-ttu-id="486f7-276">測試 hello 完成 Azure 上的 web 應用程式</span><span class="sxs-lookup"><span data-stu-id="486f7-276">Test hello completed web application on Azure</span></span>
1. <span data-ttu-id="486f7-277">Hello 最上層顯示權限的 Azure 上您網頁上，選擇 **登入**。</span><span class="sxs-lookup"><span data-stu-id="486f7-277">On hello top right of your web page on Azure, choose **Log in**.</span></span>
   
    ![Test log in][HCTestLogIn]
2. <span data-ttu-id="486f7-279">Web 應用程式現在正在您的應用程式服務連接 tooyour web 應用程式的成員資格資料庫，在本機電腦上。</span><span class="sxs-lookup"><span data-stu-id="486f7-279">Your App Service web app is now connected tooyour web application's membership database on your local machine.</span></span> <span data-ttu-id="486f7-280">tooverify，登入相同的認證，您輸入 hello 本機資料庫先前的 hello。</span><span class="sxs-lookup"><span data-stu-id="486f7-280">tooverify this, log in with hello same credentials that you entered in hello local database earlier.</span></span>
   
    ![Hello greeting][HCTestHelloContoso]
3. <span data-ttu-id="486f7-282">toofurther 測試新的混合式連線，登出您的 Azure web 應用程式並註冊為另一位使用者。</span><span class="sxs-lookup"><span data-stu-id="486f7-282">toofurther test your new hybrid connection, log off of your Azure web application and register as another user.</span></span> <span data-ttu-id="486f7-283">提供新的使用者名稱和密碼，然後按一下註冊 。</span><span class="sxs-lookup"><span data-stu-id="486f7-283">Provide a new user name and password, and then click **Register**.</span></span>
   
    ![Test register another user][HCTestRegisterRelecloud]
4. <span data-ttu-id="486f7-285">tooverify hello 新使用者的認證，透過您的混合式連線，本機資料庫中已儲存在本機電腦上開啟 SQL Management Studio。</span><span class="sxs-lookup"><span data-stu-id="486f7-285">tooverify that hello new user's credentials have been stored in your local database through your hybrid connection, open SQL Management Studio on your local computer.</span></span> <span data-ttu-id="486f7-286">在 物件總管 中，展開 hello **MembershipDB**資料庫，然後再展開**資料表**。</span><span class="sxs-lookup"><span data-stu-id="486f7-286">In Object Explorer, expand hello **MembershipDB** database, and then expand **Tables**.</span></span> <span data-ttu-id="486f7-287">以滑鼠右鍵按一下 hello **dbo。AspNetUsers**成員資格資料表，並選擇**選取前 1000 個資料列**tooview hello 結果。</span><span class="sxs-lookup"><span data-stu-id="486f7-287">Right-click hello **dbo.AspNetUsers** membership table and choose **Select Top 1000 Rows** tooview hello results.</span></span>
   
    ![檢視 hello 結果][HCTestSSMSTree]
5. <span data-ttu-id="486f7-289">本機成員資格資料表現在會顯示這兩個帳戶-您在本機建立的其中一個 hello 與 hello hello Azure 雲端中建立的其中一個。</span><span class="sxs-lookup"><span data-stu-id="486f7-289">Your local membership table now shows both accounts - hello one that you created locally, and hello one that you created in hello Azure cloud.</span></span> <span data-ttu-id="486f7-290">您建立 hello 雲端中的 hello 已儲存 tooyour 在內部部署資料庫，透過 Azure 的混合式連接功能。</span><span class="sxs-lookup"><span data-stu-id="486f7-290">hello one that you created in hello cloud has been saved tooyour on-premises database through Azure's Hybrid Connection feature.</span></span>
   
    ![Registered users in on-premises database][HCTestShowMemberDb]

<span data-ttu-id="486f7-292">您現在已建立並部署 ASP.NET web 應用程式使用 hello Azure 雲端中的 web 應用程式與內部部署 SQL Server 資料庫之間的混合式連接。</span><span class="sxs-lookup"><span data-stu-id="486f7-292">You have now created and deployed an ASP.NET web application that uses a hybrid connection between a web app in hello Azure cloud and an on-premises SQL Server database.</span></span> <span data-ttu-id="486f7-293">恭喜！</span><span class="sxs-lookup"><span data-stu-id="486f7-293">Congratulations!</span></span>

## <a name="see-also"></a><span data-ttu-id="486f7-294">另請參閱</span><span class="sxs-lookup"><span data-stu-id="486f7-294">See Also</span></span>
[<span data-ttu-id="486f7-295">混合式連線概觀</span><span class="sxs-lookup"><span data-stu-id="486f7-295">Hybrid Connections overview</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=397274)

[<span data-ttu-id="486f7-296">Josh Twist 介紹混合式連線 (第 9 頻道視訊)</span><span class="sxs-lookup"><span data-stu-id="486f7-296">Josh Twist introduces hybrid connections (Channel 9 video)</span></span>](http://channel9.msdn.com/Shows/Azure-Friday/Josh-Twist-introduces-hybrid-connections)

[<span data-ttu-id="486f7-297">混合式連線概觀</span><span class="sxs-lookup"><span data-stu-id="486f7-297">Hybrid Connections overview</span></span>](/services/biztalk-services/)

[<span data-ttu-id="486f7-298">BizTalk 服務：儀表板、監視器、調整、設定和混合式連線索引標籤</span><span class="sxs-lookup"><span data-stu-id="486f7-298">BizTalk Services: Dashboard, Monitor, Scale, Configure, and Hybrid Connection tabs</span></span>](../biztalk-services/biztalk-dashboard-monitor-scale-tabs.md)

[<span data-ttu-id="486f7-299">透過絕佳的應用程式可攜性建置真實的混合式雲端 (第 9 頻道視訊)</span><span class="sxs-lookup"><span data-stu-id="486f7-299">Building a Real-World Hybrid Cloud with Seamless Application Portability (Channel 9 video)</span></span>](http://channel9.msdn.com/events/TechEd/NorthAmerica/2014/DCIM-B323#fbid=)

[<span data-ttu-id="486f7-300">在 Azure App Service 中使用混合式連線存取內部部署資源</span><span class="sxs-lookup"><span data-stu-id="486f7-300">Access on-premises resources using hybrid connections in Azure App Service</span></span>](web-sites-hybrid-connection-get-started.md)

[<span data-ttu-id="486f7-301">ASP.NET 身分識別概觀</span><span class="sxs-lookup"><span data-stu-id="486f7-301">ASP.NET Identity Overview</span></span>](http://www.asp.net/identity)

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

<!-- IMAGES -->
[SQLServerInstall]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A01SQLServerInstall.png
[ChooseDefaultInstance]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A02ChooseDefaultInstance.png
[ChooseMixedMode]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A03ChooseMixedMode.png
[SSMSConnectToServer]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A04SSMSConnectToServer.png
[SSMScreateNewDB]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A05SSMScreateNewDBlh.png
[SSMSprovideDBname]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A06SSMSprovideDBname.png
[SSMSMembershipDBCreated]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A07SSMSMembershipDBCreated.png
[New]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/B01New.png
[NewWebsite]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/B02NewWebsite.png
[WebsiteCreationBlade]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/B03WebsiteCreationBlade.png
[WebSiteRunningBlade]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/B04WebSiteRunningBlade.png
[Browse]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/B05Browse.png
[DefaultWebSitePage]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/B06DefaultWebSitePage.png
[CreateHCHCIcon]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C01CreateHCHCIcon.png
[CreateHCAddHC]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C02CreateHCAddHC.png
[TwinCreateHCBlades]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C03TwinCreateHCBlades.png
[CreateHCCreateBTS]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C04CreateHCCreateBTS.png
[CreateBTScomplete]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C05CreateBTScomplete.png
[CreateHCSuccessNotification]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C06CreateHCSuccessNotification.png
[CreateHCOneConnectionCreated]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C07CreateHCOneConnectionCreated.png
[HCIcon]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D01HCIcon.png
[NotConnected]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D02NotConnected.png
[NotConnectedBlade]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D03NotConnectedBlade.png
[ClickListenerSetup]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D04ClickListenerSetup.png
[ClickToInstallHCM]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D05ClickToInstallHCM.png
[ApplicationRunWarning]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D06ApplicationRunWarning.png
[UAC]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D07UAC.png
[HCMInstalling]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D08HCMInstalling.png
[HCMInstallComplete]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D09HCMInstallComplete.png
[HCStatusConnected]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D10HCStatusConnected.png
[HCVSNewProject]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E01HCVSNewProject.png
[HCVSChooseASPNET]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E02HCVSChooseASPNET.png
[HCVSChooseMVC]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E03HCVSChooseMVC.png
[HCVSReadmePage]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E04HCVSReadmePage.png
[HCVSChooseWebConfig]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E05HCVSChooseWebConfig.png
[HCVSConnectionString]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E06HCVSConnectionString.png
[HCVSRunProject]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E06HCVSRunProject.png
[HCVSRegisterLocally]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E07HCVSRegisterLocally.png
[HCVSCreateNewAccount]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E08HCVSCreateNewAccount.png
[PortalDownloadPublishProfile]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F01PortalDownloadPublishProfile.png
[HCVSPublishProfileInDownloadsFolder]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F02HCVSPublishProfileInDownloadsFolder.png
[HCVSRightClickProjectSelectPublish]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F03HCVSRightClickProjectSelectPublish.png
[HCVSPublishWebDialogImport]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F04HCVSPublishWebDialogImport.png
[HCVSBrowseToImportPubProfile]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F05HCVSBrowseToImportPubProfile.png
[HCVSClickPublish]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F06HCVSClickPublish.png
[HCTestLogIn]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F07HCTestLogIn.png
[HCTestHelloContoso]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F08HCTestHelloContoso.png
[HCTestRegisterRelecloud]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F09HCTestRegisterRelecloud.png
[HCTestSSMSTree]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F10HCTestSSMSTree.png
[HCTestShowMemberDb]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F11HCTestShowMemberDb.png
