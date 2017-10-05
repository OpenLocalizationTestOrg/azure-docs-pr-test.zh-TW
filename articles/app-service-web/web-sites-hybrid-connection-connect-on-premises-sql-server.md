---
title: "使用混合式連線從 Azure App Service 內的 Web 應用程式連線至內部部署 SQL Server"
description: "在 Microsoft Azure 上建立 Web 應用程式，並將它連接到內部部署 SQL Server 資料庫"
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
ms.openlocfilehash: 12456ef3e2aecfa7a03cca97de2ff6ffd9602357
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="connect-to-on-premises-sql-server-from-a-web-app-in-azure-app-service-using-hybrid-connections"></a><span data-ttu-id="7a378-103">使用混合式連線從 Azure App Service 內的 Web 應用程式連線至內部部署 SQL Server</span><span class="sxs-lookup"><span data-stu-id="7a378-103">Connect to on-premises SQL Server from a web app in Azure App Service using Hybrid Connections</span></span>
<span data-ttu-id="7a378-104">「混合式連線」可將 [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web Apps 連接到使用靜態 TCP 連接埠的內部部署資源。</span><span class="sxs-lookup"><span data-stu-id="7a378-104">Hybrid Connections can connect [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web Apps to on-premises resources that use a static TCP port.</span></span> <span data-ttu-id="7a378-105">支援的資源包括 Microsoft SQL Server、MySQL、HTTP Web API、App Service 和大部分的自訂 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="7a378-105">Supported resources include Microsoft SQL Server, MySQL, HTTP Web APIs, App Service, and most custom Web Services.</span></span>

<span data-ttu-id="7a378-106">在本教學課程中，您將了解如何在 [Azure 入口網站](http://go.microsoft.com/fwlink/?LinkId=529715)中建立 App Service Web 應用程式、使用新的「混合式連線」功能將 Web 應用程式連接到您的本機內部部署 SQL Server 資料庫、建立將使用混合式連線的簡易 ASP.NET 應用程式，以及將應用程式部署至 App Service Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="7a378-106">In this tutorial, you will learn how to create an App Service web app in the [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715), connect the web app to your local on-premises SQL Server database using the new Hybrid Connection feature, create a simple ASP.NET application that will use the hybrid connection, and deploy the application to the App Service web app.</span></span> <span data-ttu-id="7a378-107">Azure 上已完成的 Web 應用程式會將使用者認證儲存在內部部署的成員資格資料庫中。</span><span class="sxs-lookup"><span data-stu-id="7a378-107">The completed web app on Azure stores user credentials in a membership database that is on-premises.</span></span> <span data-ttu-id="7a378-108">本教學課程假設您沒有使用 Azure 或 ASP.NET 的經驗。</span><span class="sxs-lookup"><span data-stu-id="7a378-108">The tutorial assumes no prior experience using Azure or ASP.NET.</span></span>

> [!NOTE]
> <span data-ttu-id="7a378-109">如果您想在註冊 Azure 帳戶前開始使用 Azure App Service，請移至 [試用 App Service](https://azure.microsoft.com/try/app-service/)，即可在 App Service 中立即建立短期入門 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="7a378-109">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="7a378-110">不需要信用卡；無需承諾。</span><span class="sxs-lookup"><span data-stu-id="7a378-110">No credit cards required; no commitments.</span></span>
> 
> <span data-ttu-id="7a378-111">「混合式連線」功能的 Web Apps 部分僅適用於 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="7a378-111">The Web Apps portion of the Hybrid Connections feature is available only in the [Azure Portal](https://portal.azure.com).</span></span> <span data-ttu-id="7a378-112">若要在 BizTalk 服務中建立連線，請參閱 [混合式連線](http://go.microsoft.com/fwlink/p/?LinkID=397274)。</span><span class="sxs-lookup"><span data-stu-id="7a378-112">To create a connection in BizTalk Services, see [Hybrid Connections](http://go.microsoft.com/fwlink/p/?LinkID=397274).</span></span>  
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="7a378-113">必要條件</span><span class="sxs-lookup"><span data-stu-id="7a378-113">Prerequisites</span></span>
<span data-ttu-id="7a378-114">若要完成本教學課程，您將需要下列產品。</span><span class="sxs-lookup"><span data-stu-id="7a378-114">To complete this tutorial, you'll need the following products.</span></span> <span data-ttu-id="7a378-115">所有產品都有免費版本可使用，因此您可以免費進行 Azure 相關開發。</span><span class="sxs-lookup"><span data-stu-id="7a378-115">All are available in free versions, so you can start developing for Azure entirely for free.</span></span>

* <span data-ttu-id="7a378-116">**Azure 訂閱** - 如需免費訂閱，請參閱 [Azure 免費試用](/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="7a378-116">**Azure subscription** - For a free subscription, see [Azure Free Trial](/pricing/free-trial/).</span></span>
* <span data-ttu-id="7a378-117">**Visual Studio 2013** - 若要下載 Visual Studio 2013 的免費試用版，請參閱 [Visual Studio 下載](http://www.visualstudio.com/downloads/download-visual-studio-vs)。</span><span class="sxs-lookup"><span data-stu-id="7a378-117">**Visual Studio 2013** - To download a free trial version of Visual Studio 2013, see [Visual Studio Downloads](http://www.visualstudio.com/downloads/download-visual-studio-vs).</span></span> <span data-ttu-id="7a378-118">請先安裝此項目再繼續作業。</span><span class="sxs-lookup"><span data-stu-id="7a378-118">Install this before continuing.</span></span>
* <span data-ttu-id="7a378-119">**Microsoft .NET Framework 3.5 Service Pack 1** - 如果您的作業系統是 Windows 8.1、Windows Server 2012 R2、Windows 8、Windows Server 2012、Windows 7 或 Windows Server 2008 R2，您可以在 [控制台] > [程式和功能] > [開啟或關閉 Windows 功能] 中啟用此項目。</span><span class="sxs-lookup"><span data-stu-id="7a378-119">**Microsoft .NET Framework 3.5 Service Pack 1** - If your operating system is Windows 8.1, Windows Server 2012 R2, Windows 8, Windows Server 2012, Windows 7, or Windows Server 2008 R2, you can enable this in Control Panel > Programs and Features > Turn Windows features on or off.</span></span> <span data-ttu-id="7a378-120">否則，您可以從 [Microsoft 下載中心](http://www.microsoft.com/download/en/details.aspx?displaylang=en&id=22)下載。</span><span class="sxs-lookup"><span data-stu-id="7a378-120">Otherwise, you can download it from the [Microsoft Download Center](http://www.microsoft.com/download/en/details.aspx?displaylang=en&id=22).</span></span>
* <span data-ttu-id="7a378-121">**SQL Server 2014 Express with Tools** - 請在 [Microsoft Web Platform Database 頁面](http://www.microsoft.com/web/platform/database.aspx)下載免費的 Microsoft SQL Server Express。</span><span class="sxs-lookup"><span data-stu-id="7a378-121">**SQL Server 2014 Express with Tools** - download Microsoft SQL Server Express for free at the [Microsoft Web Platform Database page](http://www.microsoft.com/web/platform/database.aspx).</span></span> <span data-ttu-id="7a378-122">選擇 [Express]  \(非 LocalDB) 版本。</span><span class="sxs-lookup"><span data-stu-id="7a378-122">Choose the **Express** (not LocalDB) version.</span></span> <span data-ttu-id="7a378-123">[Express with Tools]  版本包含您將在此教學課程中使用的 SQL Server Management Studio。</span><span class="sxs-lookup"><span data-stu-id="7a378-123">The **Express with Tools** version includes SQL Server Management Studio, which you will use in this tutorial.</span></span>
* <span data-ttu-id="7a378-124">**SQL Server Management Studio Express** - 此項目隨附於前述的 SQL Server 2014 Express with Tools 下載中，但您必須個別加以安裝，您可以從 [SQL Server Express 下載頁面](http://www.microsoft.com/web/platform/database.aspx)加以下載並安裝。</span><span class="sxs-lookup"><span data-stu-id="7a378-124">**SQL Server Management Studio Express** - This is included with the SQL Server 2014 Express with Tools download mentioned above, but if you need to install it separately, you can download and install it from the [SQL Server Express download page](http://www.microsoft.com/web/platform/database.aspx).</span></span>

<span data-ttu-id="7a378-125">本教學課程假設您具有 Azure 訂閱、您已安裝 Visual Studio 2013，並且已安裝或啟用 .NET Framework 3.5。</span><span class="sxs-lookup"><span data-stu-id="7a378-125">The tutorial assumes that you have an Azure subscription, that you have installed Visual Studio 2013, and that you have installed or enabled .NET Framework 3.5.</span></span> <span data-ttu-id="7a378-126">本教學課程將說明如何在可與 Azure 混合式連線功能妥善搭配運作的組態中安裝 SQL Server 2014 Express (使用靜態 TCP 連接埠的預設執行個體)。</span><span class="sxs-lookup"><span data-stu-id="7a378-126">The tutorial shows you how to install SQL Server 2014 Express in a configuration that works well with the Azure Hybrid Connections feature (a default instance with a static TCP port).</span></span> <span data-ttu-id="7a378-127">在開始本教學課程之前，如果您尚未安裝 SQL Server，請先從前述位置下載 SQL Server 2014 Express with Tools。</span><span class="sxs-lookup"><span data-stu-id="7a378-127">Before starting the tutorial, download SQL Server 2014 Express with Tools from the location mentioned above if you do not have SQL Server installed.</span></span>

### <a name="notes"></a><span data-ttu-id="7a378-128">注意事項</span><span class="sxs-lookup"><span data-stu-id="7a378-128">Notes</span></span>
<span data-ttu-id="7a378-129">若要透過混合式連線使用內部部署 SQL Server 或 SQL Server Express 資料庫，必須在靜態連接埠上啟用 TCP/IP。</span><span class="sxs-lookup"><span data-stu-id="7a378-129">To use an on-premises SQL Server or SQL Server Express database with a hybrid connection, TCP/IP needs to be enabled on a static port.</span></span> <span data-ttu-id="7a378-130">SQL Server 上的預設執行個體會使用靜態連接埠 1433，但指定的執行個體則否。</span><span class="sxs-lookup"><span data-stu-id="7a378-130">Default instances on SQL Server use static port 1433, whereas named instances do not.</span></span>

<span data-ttu-id="7a378-131">安裝內部部署混合式連線管理員代理程式的電腦：</span><span class="sxs-lookup"><span data-stu-id="7a378-131">The computer on which you install the on-premises Hybrid Connection Manager agent:</span></span>

* <span data-ttu-id="7a378-132">必須有透過下列連接埠的 Azure 輸出連線：</span><span class="sxs-lookup"><span data-stu-id="7a378-132">Must have outbound connectivity to Azure over:</span></span>

| <span data-ttu-id="7a378-133">連接埠</span><span class="sxs-lookup"><span data-stu-id="7a378-133">Port</span></span> | <span data-ttu-id="7a378-134">理由</span><span class="sxs-lookup"><span data-stu-id="7a378-134">Why</span></span> |
| --- | --- |
| <span data-ttu-id="7a378-135">80</span><span class="sxs-lookup"><span data-stu-id="7a378-135">80</span></span> |<span data-ttu-id="7a378-136">**必要** 可供 HTTP 連接埠進行憑證驗證以及可供進行資料連線 (選用)。</span><span class="sxs-lookup"><span data-stu-id="7a378-136">**Required** for HTTP port for certificate validation and optionally for data connectivity.</span></span> |
| <span data-ttu-id="7a378-137">443</span><span class="sxs-lookup"><span data-stu-id="7a378-137">443</span></span> |<span data-ttu-id="7a378-138">**選用** 可供進行資料連線。</span><span class="sxs-lookup"><span data-stu-id="7a378-138">**Optional** for data connectivity.</span></span> <span data-ttu-id="7a378-139">如果無法使用 443 的輸出連線，則使用 TCP 連接埠 80。</span><span class="sxs-lookup"><span data-stu-id="7a378-139">If outbound connectivity to 443 is unavailable, TCP port 80 is used.</span></span> |
| <span data-ttu-id="7a378-140">5671 和 9352</span><span class="sxs-lookup"><span data-stu-id="7a378-140">5671 and 9352</span></span> |<span data-ttu-id="7a378-141">**建議** 但可供進行資料連線 (選用)。</span><span class="sxs-lookup"><span data-stu-id="7a378-141">**Recommended** but Optional for data connectivity.</span></span> <span data-ttu-id="7a378-142">請注意，此模式通常會產生較高的輸送量。</span><span class="sxs-lookup"><span data-stu-id="7a378-142">Note this mode usually yields higher throughput.</span></span> <span data-ttu-id="7a378-143">如果無法使用這些連接埠的輸出連線，則使用 TCP 連接埠 443。</span><span class="sxs-lookup"><span data-stu-id="7a378-143">If outbound connectivity to these ports is unavailable, TCP port 443 is used.</span></span> |

* <span data-ttu-id="7a378-144">必須能夠連繫內部部署資源的 *hostname*上：*portnumber* 。</span><span class="sxs-lookup"><span data-stu-id="7a378-144">Must be able to reach the *hostname*:*portnumber* of your on-premises resource.</span></span>

<span data-ttu-id="7a378-145">本文中的步驟假設您使用將主控內部部署混合式連線代理程式之電腦中的瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="7a378-145">The steps in this article assume that you are using the browser from the computer that will host the on-premises hybrid connection agent.</span></span>

<span data-ttu-id="7a378-146">如果您已在組態和符合前述條件的環境中安裝 SQL Server，您可以直接開始 [在內部部署中建立 SQL Server 資料庫](#CreateSQLDB)。</span><span class="sxs-lookup"><span data-stu-id="7a378-146">If you already have SQL Server installed in a configuration and in an environment that meets the conditions described above, you can skip ahead and start with [Create a SQL Server database on-premises](#CreateSQLDB).</span></span>

<a name="InstallSQL"></a>

## <a name="a-install-sql-server-express-enable-tcpip-and-create-a-sql-server-database-on-premises"></a><span data-ttu-id="7a378-147">A.</span><span class="sxs-lookup"><span data-stu-id="7a378-147">A.</span></span> <span data-ttu-id="7a378-148">在內部部署中安裝 SQL Server Express、啟用 TCP/IP 及建立 SQL Server 資料庫</span><span class="sxs-lookup"><span data-stu-id="7a378-148">Install SQL Server Express, enable TCP/IP, and create a SQL Server database on-premises</span></span>
<span data-ttu-id="7a378-149">本節說明如何安裝 SQL Server Express、啟用 TCP/IP 及建立資料庫，讓您的 Web 應用程式可在 Azure 入口網站中運作。</span><span class="sxs-lookup"><span data-stu-id="7a378-149">This section shows you how to install SQL Server Express, enable TCP/IP, and create a database so that your web application will work with the Azure Portal.</span></span>

### <a name="install-sql-server-express"></a><span data-ttu-id="7a378-150">安裝 SQL Server Express</span><span class="sxs-lookup"><span data-stu-id="7a378-150">Install SQL Server Express</span></span>
1. <span data-ttu-id="7a378-151">若要安裝 SQL Server Express，請執行您已下載的 **SQLEXPRWT_x64_ENU.exe** 或 **SQLEXPR_x86_ENU.exe** 檔案。</span><span class="sxs-lookup"><span data-stu-id="7a378-151">To install SQL Server Express, run the **SQLEXPRWT_x64_ENU.exe** or **SQLEXPR_x86_ENU.exe** file that you downloaded.</span></span> <span data-ttu-id="7a378-152">[SQL Server 安裝中心] 精靈會隨即出現。</span><span class="sxs-lookup"><span data-stu-id="7a378-152">The SQL Server Installation Center wizard appears.</span></span>
   
    ![SQL Server Install][SQLServerInstall]
2. <span data-ttu-id="7a378-154">選擇 [新的 SQL Server 獨立安裝或將功能加入到現有安裝] 。</span><span class="sxs-lookup"><span data-stu-id="7a378-154">Choose **New SQL Server stand-alone installation or add features to an existing installation**.</span></span> <span data-ttu-id="7a378-155">遵循指示接受預設選項和設定，直到您進入 [執行個體組態]  頁面。</span><span class="sxs-lookup"><span data-stu-id="7a378-155">Follow the instructions, accepting the default choices and settings, until you get to the **Instance Configuration** page.</span></span>
3. <span data-ttu-id="7a378-156">在 [執行個體組態] 頁面上，選擇 [預設執行個體]。</span><span class="sxs-lookup"><span data-stu-id="7a378-156">On the **Instance Configuration** page, choose **Default instance**.</span></span>
   
    ![Choose Default Instance][ChooseDefaultInstance]
   
    <span data-ttu-id="7a378-158">根據預設，SQL Server 的預設執行個體會在靜態連接埠 1433 上接聽來自 SQL Server 用戶端的要求，而這正是混合式連線功能的需求。</span><span class="sxs-lookup"><span data-stu-id="7a378-158">By default, the default instance of SQL Server listens for requests from SQL Server clients on static port 1433, which is what the Hybrid Connections feature requires.</span></span> <span data-ttu-id="7a378-159">指定的執行個體會使用動態連接埠和 UDP，而混合式連線並不加以支援。</span><span class="sxs-lookup"><span data-stu-id="7a378-159">Named instances use dynamic ports and UDP, which are not supported by Hybrid Connections.</span></span>
4. <span data-ttu-id="7a378-160">接受 [伺服器組態]  頁面上的預設值。</span><span class="sxs-lookup"><span data-stu-id="7a378-160">Accept the defaults on the **Server Configuration** page.</span></span>
5. <span data-ttu-id="7a378-161">在 [資料庫引擎組態] 頁面上的 [驗證模式] 下，選擇 [混合模式 (SQL Server 驗證和 Windows 驗證)]，並提供密碼。</span><span class="sxs-lookup"><span data-stu-id="7a378-161">On the **Database Engine Configuration** page, under **Authentication Mode**, choose **Mixed Mode (SQL Server authentication and Windows authentication)**, and provide a password.</span></span>
   
    ![Choose Mixed Mode][ChooseMixedMode]
   
    <span data-ttu-id="7a378-163">在本教學課程中，您將使用 SQL Server 驗證。</span><span class="sxs-lookup"><span data-stu-id="7a378-163">In this tutorial, you will be using SQL Server authentication.</span></span> <span data-ttu-id="7a378-164">請務必記住您提供的密碼，因為後續將會用到。</span><span class="sxs-lookup"><span data-stu-id="7a378-164">Be sure to remember the password that you provide, because you will need it later.</span></span>
6. <span data-ttu-id="7a378-165">逐步完成精靈的其餘步驟，以完成安裝。</span><span class="sxs-lookup"><span data-stu-id="7a378-165">Step through the rest of the wizard to complete the installation.</span></span>

### <a name="enable-tcpip"></a><span data-ttu-id="7a378-166">啟用 TCP/IP</span><span class="sxs-lookup"><span data-stu-id="7a378-166">Enable TCP/IP</span></span>
<span data-ttu-id="7a378-167">若要啟用 TCP/IP，您必須使用您在安裝 SQL Server Express 時所安裝的 SQL Server 組態管理員。</span><span class="sxs-lookup"><span data-stu-id="7a378-167">To enable TCP/IP, you will use SQL Server Configuration Manager, which was installed when you installed SQL Server Express.</span></span> <span data-ttu-id="7a378-168">請先執行 [為 SQL Server 啟用 TCP/IP 網路通訊協定](http://technet.microsoft.com/library/hh231672%28v=sql.110%29.aspx) 中的步驟，再繼續作業。</span><span class="sxs-lookup"><span data-stu-id="7a378-168">Follow the steps in [Enable TCP/IP Network Protocol for SQL Server](http://technet.microsoft.com/library/hh231672%28v=sql.110%29.aspx) before continuing.</span></span>

<a name="CreateSQLDB"></a>

### <a name="create-a-sql-server-database-on-premises"></a><span data-ttu-id="7a378-169">在內部部署中建立 SQL Server 資料庫</span><span class="sxs-lookup"><span data-stu-id="7a378-169">Create a SQL Server database on-premises</span></span>
<span data-ttu-id="7a378-170">您的 Visual Studio Web 應用程式需要可由 Azure 存取的成員資格資料庫。</span><span class="sxs-lookup"><span data-stu-id="7a378-170">Your Visual Studio web application requires a membership database that can be accessed by Azure.</span></span> <span data-ttu-id="7a378-171">這必須要有 SQL Server 或 SQL Server Express 資料庫 (不是 MVC 範本依預設使用的 LocalDB 資料庫)，因此您接下來將會建立成員資格資料庫。</span><span class="sxs-lookup"><span data-stu-id="7a378-171">This requires a SQL Server or SQL Server Express database (not the LocalDB database that the MVC template uses by default), so you'll create the membership database next.</span></span>

1. <span data-ttu-id="7a378-172">在 SQL Server Management Studio 中，連接到您剛剛安裝的 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="7a378-172">In SQL Server Management Studio, connect to the SQL Server you just installed.</span></span> <span data-ttu-id="7a378-173">(如果 [連線到伺服器] 對話方塊未自動出現，請導覽至左窗格中的 [物件總管]，依序按一下 [連接] 和 [資料庫引擎]。)![連接到伺服器][SSMSConnectToServer]</span><span class="sxs-lookup"><span data-stu-id="7a378-173">(If the **Connect to Server** dialog does not appear automatically, navigate to **Object Explorer** in the left pane, click **Connect**, and then click **Database Engine**.) ![Connect to Server][SSMSConnectToServer]</span></span>
   
    <span data-ttu-id="7a378-174">針對 [伺服器類型]，選擇 [資料庫引擎]。</span><span class="sxs-lookup"><span data-stu-id="7a378-174">For **Server type**, choose **Database Engine**.</span></span> <span data-ttu-id="7a378-175">對於 [伺服器名稱]，您可以使用 **localhost** 或您要使用之電腦的名稱。</span><span class="sxs-lookup"><span data-stu-id="7a378-175">For **Server name**, you can use **localhost** or the name of the computer that you are using.</span></span> <span data-ttu-id="7a378-176">選擇 [SQL Server 驗證]，然後以您先前建立的 sa 使用者名稱和密碼登入。</span><span class="sxs-lookup"><span data-stu-id="7a378-176">Choose **SQL Server authentication**, and then log in with the sa user name and the password that you created earlier.</span></span>
2. <span data-ttu-id="7a378-177">若要使用 SQL Server Management Studio 建立新資料庫，請在 [物件總管] 中以滑鼠右鍵按一下 [資料庫]，然後按一下 [新增資料庫]。</span><span class="sxs-lookup"><span data-stu-id="7a378-177">To create a new database by using SQL Server Management Studio, right-click **Databases** in Object Explorer, and then click **New Database**.</span></span>
   
    ![Create new database][SSMScreateNewDB]
3. <span data-ttu-id="7a378-179">在 [新增資料庫] 對話方塊中，輸入 MembershipDB 做為資料庫名稱，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="7a378-179">In the **New Database** dialog, enter MembershipDB for the database name, and then click **OK**.</span></span>
   
    ![Provide database name][SSMSprovideDBname]
   
    <span data-ttu-id="7a378-181">請注意，到目前為止您並未對資料庫做任何變更。</span><span class="sxs-lookup"><span data-stu-id="7a378-181">Note that you do not make any changes to the database at this point.</span></span> <span data-ttu-id="7a378-182">成員資格資訊後續會在您執行 Web 應用程式時由該應用程式自動新增。</span><span class="sxs-lookup"><span data-stu-id="7a378-182">The membership information will be added automatically later by your web application when you run it.</span></span>
4. <span data-ttu-id="7a378-183">在 [物件總管] 中，如果您展開 [資料庫] ，您會發現成員資格資料庫已建立。</span><span class="sxs-lookup"><span data-stu-id="7a378-183">In Object Explorer, if you expand **Databases**, you will see that the membership database has been created.</span></span>
   
    ![MembershipDB created][SSMSMembershipDBCreated]

<a name="CreateSite"></a>

## <a name="b-create-a-web-app-in-the-azure-portal"></a><span data-ttu-id="7a378-185">B.</span><span class="sxs-lookup"><span data-stu-id="7a378-185">B.</span></span> <span data-ttu-id="7a378-186">在 Azure 入口網站中建立 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="7a378-186">Create a web app in the Azure Portal</span></span>
> [!NOTE]
> <span data-ttu-id="7a378-187">如果您已在 Azure 入口網站中建立要用於此教學課程的 Web 應用程式，您可以直接跳到 [建立混合式連線和 BizTalk 服務](#CreateHC) 繼續作業。</span><span class="sxs-lookup"><span data-stu-id="7a378-187">If you have already created a web app in the Azure Portal that you want to use for this tutorial, you can skip ahead to [Create a Hybrid Connection and a BizTalk Service](#CreateHC) and continue from there.</span></span>
> 
> 

1. <span data-ttu-id="7a378-188">在 [Azure 入口網站](https://portal.azure.com)中，按一下 [新增]  >  [Web + 行動]  >  [Web 應用程式]。</span><span class="sxs-lookup"><span data-stu-id="7a378-188">In the [Azure Portal](https://portal.azure.com), click **New** > **Web + Mobile** > **Web app**.</span></span>
   
    ![New button][New]
2. <span data-ttu-id="7a378-190">設定您的 Web 應用程式，然後按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="7a378-190">Configure your web app, and then click **Create**.</span></span>
   
    ![Website name][WebsiteCreationBlade]
3. <span data-ttu-id="7a378-192">經過一段時間之後，Web 應用程式會建立，並顯示它的 Web 應用程式分頁。</span><span class="sxs-lookup"><span data-stu-id="7a378-192">After a few moments, the web app is created and its web app blade appears.</span></span> <span data-ttu-id="7a378-193">此分頁是垂直捲動的儀表板，可供您管理 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="7a378-193">The blade is a vertically scrollable dashboard that lets you manage your web app.</span></span>
   
    ![Website running][WebSiteRunningBlade]
   
    <span data-ttu-id="7a378-195">若要確認 Web 應用程式是否已上線啟用，您可以按一下 [瀏覽]  圖示以顯示預設頁面。</span><span class="sxs-lookup"><span data-stu-id="7a378-195">To verify the web app is live, you can click the **Browse** icon to display the default page.</span></span>

<span data-ttu-id="7a378-196">接著，您將為 Web 應用程式建立混合式連線和 BizTalk 服務。</span><span class="sxs-lookup"><span data-stu-id="7a378-196">Next, you will create a hybrid connection and a BizTalk service for the web app.</span></span>

<a name="CreateHC"></a>

## <a name="c-create-a-hybrid-connection-and-a-biztalk-service"></a><span data-ttu-id="7a378-197">C.</span><span class="sxs-lookup"><span data-stu-id="7a378-197">C.</span></span> <span data-ttu-id="7a378-198">建立混合式連線和 BizTalk 服務</span><span class="sxs-lookup"><span data-stu-id="7a378-198">Create a Hybrid Connection and a BizTalk Service</span></span>
1. <span data-ttu-id="7a378-199">返回入口網站，移至設定並按一下 [網路]  >  [設定混合式連接端點]。</span><span class="sxs-lookup"><span data-stu-id="7a378-199">Back in the Portal, go to settings and click **Networking** > **Configure your hybrid connection endpoints**.</span></span>
   
    ![混合式連線][CreateHCHCIcon]
2. <span data-ttu-id="7a378-201">在 [混合式連線] 分頁上，按一下 [新增]  >  [建立混合式連線]。</span><span class="sxs-lookup"><span data-stu-id="7a378-201">On the Hybrid connections blade, click **Add** > **New hybrid connection**.</span></span>
3. <span data-ttu-id="7a378-202">在 [建立混合式連線]  刀鋒視窗上：</span><span class="sxs-lookup"><span data-stu-id="7a378-202">On the **Create hybrid connection** blade:</span></span>
   
   * <span data-ttu-id="7a378-203">在 [名稱] 中，提供連線的名稱。</span><span class="sxs-lookup"><span data-stu-id="7a378-203">For **Name**, provide a name for the connection.</span></span>
   * <span data-ttu-id="7a378-204">針對 [主機名稱] ，輸入您的 SQL Server 主機電腦的電腦名稱。</span><span class="sxs-lookup"><span data-stu-id="7a378-204">For **Hostname**, enter the computer name of your SQL Server host computer.</span></span>
   * <span data-ttu-id="7a378-205">針對 [連接埠] ，輸入 1433 (SQL Server 的預設連接埠)。</span><span class="sxs-lookup"><span data-stu-id="7a378-205">For **Port**, enter 1433 (the default port for SQL Server).</span></span>
   * <span data-ttu-id="7a378-206">按一下 [BizTalk 服務]  >  [新增 BizTalk 服務]，然後輸入 BizTalk 服務的名稱。</span><span class="sxs-lookup"><span data-stu-id="7a378-206">Click **BizTalk Service** > **New BizTalk Service** and enter a name for the BizTalk service.</span></span>
     
     ![Create a hybrid connection][TwinCreateHCBlades]
4. <span data-ttu-id="7a378-208">按兩次 [確定]  。</span><span class="sxs-lookup"><span data-stu-id="7a378-208">Click **OK** twice.</span></span>
   
    <span data-ttu-id="7a378-209">程序完成時，[通知] 區域會閃爍綠色 [成功]，而且 [混合式連線] 刀鋒視窗會顯示新的混合式連線，且狀態為 [未連線]。</span><span class="sxs-lookup"><span data-stu-id="7a378-209">When the process completes, the **Notifications** area will flash a green **SUCCESS** and the **Hybrid connection** blade will show the new hybrid connection with the status as **Not connected**.</span></span>
   
    ![One hybrid connection created][CreateHCOneConnectionCreated]

<span data-ttu-id="7a378-211">至此，您已完成雲端混合式連線基礎結構的重要部分。</span><span class="sxs-lookup"><span data-stu-id="7a378-211">At this point, you have completed an important part of the cloud hybrid connection infrastructure.</span></span> <span data-ttu-id="7a378-212">接下來，您將建立對應的內部部署部分。</span><span class="sxs-lookup"><span data-stu-id="7a378-212">Next, you will create a corresponding on-premises piece.</span></span>

<a name="InstallHCM"></a>

## <a name="d-install-the-on-premises-hybrid-connection-manager-to-complete-the-connection"></a><span data-ttu-id="7a378-213">D.</span><span class="sxs-lookup"><span data-stu-id="7a378-213">D.</span></span> <span data-ttu-id="7a378-214">安裝內部部署混合式連線管理員以完成連線</span><span class="sxs-lookup"><span data-stu-id="7a378-214">Install the on-premises Hybrid Connection Manager to complete the connection</span></span>
[!INCLUDE [app-service-hybrid-connections-manager-install](../../includes/app-service-hybrid-connections-manager-install.md)]

<span data-ttu-id="7a378-215">現在，混合式連線基礎結構已完成，您將建立使用此基礎結構的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="7a378-215">Now that the hybrid connection infrastructure is complete, you will create a web application that uses it.</span></span>

<a name="CreateASPNET"></a>

## <a name="e-create-a-basic-aspnet-web-project-edit-the-database-connection-string-and-run-the-project-locally"></a><span data-ttu-id="7a378-216">E.</span><span class="sxs-lookup"><span data-stu-id="7a378-216">E.</span></span> <span data-ttu-id="7a378-217">建立基本 ASP.NET Web 專案、編輯資料庫連接字串，和在本機執行專案</span><span class="sxs-lookup"><span data-stu-id="7a378-217">Create a basic ASP.NET web project, edit the database connection string, and run the project locally</span></span>
### <a name="create-a-basic-aspnet-project"></a><span data-ttu-id="7a378-218">建立基本 ASP.NET 專案</span><span class="sxs-lookup"><span data-stu-id="7a378-218">Create a basic ASP.NET project</span></span>
1. <span data-ttu-id="7a378-219">在 Visual Studio 的 [檔案]  功能表上，建立新的專案：</span><span class="sxs-lookup"><span data-stu-id="7a378-219">In Visual Studio, on the **File** menu, create a new Project:</span></span>
   
    ![New Visual Studio project][HCVSNewProject]
2. <span data-ttu-id="7a378-221">在 [新增專案] 對話方塊的 [範本] 區段中選取 [Web]，再選擇 [ASP.NET Web 應用程式]，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="7a378-221">In the **Templates** section of the **New Project** dialog, select **Web** and choose **ASP.NET Web Application**, and then click **OK**.</span></span>
   
    ![Choose ASP.NET Web Application][HCVSChooseASPNET]
3. <span data-ttu-id="7a378-223">在 [新增 ASP.NET 專案] 對話方塊中，選擇 [MVC]，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="7a378-223">In the **New ASP.NET Project** dialog, choose **MVC**, and then click **OK**.</span></span>
   
    ![Choose MVC][HCVSChooseMVC]
4. <span data-ttu-id="7a378-225">建立專案之後，會出現應用程式 Readme 頁面。</span><span class="sxs-lookup"><span data-stu-id="7a378-225">When the project has been created, the application readme page appears.</span></span> <span data-ttu-id="7a378-226">請還不要執行 Web 專案。</span><span class="sxs-lookup"><span data-stu-id="7a378-226">Do not run the web project yet.</span></span>
   
    ![Readme page][HCVSReadmePage]

### <a name="edit-the-database-connection-string-for-the-application"></a><span data-ttu-id="7a378-228">編輯應用程式的資料庫連接字串</span><span class="sxs-lookup"><span data-stu-id="7a378-228">Edit the database connection string for the application</span></span>
<span data-ttu-id="7a378-229">在此步驟中您會編輯連接字串，以指示應用程式應至何處尋找您的本機 SQL Server Express 資料庫。</span><span class="sxs-lookup"><span data-stu-id="7a378-229">In this step, you edit the connection string that tells your application where to find your local SQL Server Express database.</span></span> <span data-ttu-id="7a378-230">連接字串位於應用程式的 Web.config 檔案中，其中包含應用程式的組態資訊。</span><span class="sxs-lookup"><span data-stu-id="7a378-230">The connection string is in the application's Web.config file, which contains configuration information for the application.</span></span>

> [!NOTE]
> <span data-ttu-id="7a378-231">為確保您的應用程式使用的是您在 SQL Server Express 中建立的資料庫，而不是 Visual Studio 的預設 LocalDB 中的資料庫，請務必先完成此步驟，再執行您的專案。</span><span class="sxs-lookup"><span data-stu-id="7a378-231">To ensure that your application uses the database that you created in SQL Server Express, and not the one in Visual Studio's default LocalDB, it is important that you complete this step before running your project.</span></span>
> 
> 

1. <span data-ttu-id="7a378-232">在 [方案總管] 中，按兩下 Web.config 檔案。</span><span class="sxs-lookup"><span data-stu-id="7a378-232">In Solution Explorer, double-click the Web.config file.</span></span>
   
    ![Web.config][HCVSChooseWebConfig]
2. <span data-ttu-id="7a378-234">依照下列範例中的語法編輯 [connectionStrings]  區段，將 SQL Server 資料庫指向您的本機電腦：</span><span class="sxs-lookup"><span data-stu-id="7a378-234">Edit the **connectionStrings** section to point to the SQL Server database on your local machine, following the syntax in the following example:</span></span>
   
    ![Connection string][HCVSConnectionString]
   
    <span data-ttu-id="7a378-236">編譯連接字串時，請留意下列事項：</span><span class="sxs-lookup"><span data-stu-id="7a378-236">When composing the connection string, keep in mind the following:</span></span>
   
   * <span data-ttu-id="7a378-237">如果您要連接到指定的執行個體而非預設執行個體 (例如 YourServer\SQLEXPRESS)，您必須將 SQL Server 設定成使用靜態連接埠。</span><span class="sxs-lookup"><span data-stu-id="7a378-237">If you are connecting to a named instance instead of a default instance (for example, YourServer\SQLEXPRESS), you must configure your SQL Server to use static ports.</span></span> <span data-ttu-id="7a378-238">如需設定靜態連接埠的相關資訊，請參閱 [如何將 SQL Server 設定成在特定連接埠上接聽](http://support.microsoft.com/kb/823938)。</span><span class="sxs-lookup"><span data-stu-id="7a378-238">For information on configuring static ports, see [How to configure SQL Server to listen on a specific port](http://support.microsoft.com/kb/823938).</span></span> <span data-ttu-id="7a378-239">根據預設，指定的執行個體會使用 UDP 和動態連接埠，而混合式連線並不加以支援。</span><span class="sxs-lookup"><span data-stu-id="7a378-239">By default, named instances use UDP and dynamic ports, which are not supported by Hybrid Connections.</span></span>
   * <span data-ttu-id="7a378-240">建議您在連接字串上指定連接埠 (依預設為 1433，如範例所示)，以確定您的本機 SQL Server 會啟用 TCP 並使用正確的連接埠。</span><span class="sxs-lookup"><span data-stu-id="7a378-240">It is recommended that you specify the port (1433 by default, as shown in the example) on the connection string so that you can be sure that your local SQL Server has TCP enabled and is using the correct port.</span></span>
   * <span data-ttu-id="7a378-241">請務必使用 SQL Server 驗證進行連接，以在您的連接字串中指定使用者識別碼和密碼。</span><span class="sxs-lookup"><span data-stu-id="7a378-241">Remember to use SQL Server Authentication to connect, specifying the user ID and password in your connection string.</span></span>
3. <span data-ttu-id="7a378-242">在 Visual Studio 中按一下 [儲存]  ，以儲存 Web.config 檔案。</span><span class="sxs-lookup"><span data-stu-id="7a378-242">Click **Save** in Visual Studio to save the Web.config file.</span></span>

### <a name="run-the-project-locally-and-register-a-new-user"></a><span data-ttu-id="7a378-243">在本機執行專案和註冊新使用者</span><span class="sxs-lookup"><span data-stu-id="7a378-243">Run the project locally and register a new user</span></span>
1. <span data-ttu-id="7a378-244">現在，請按一下 [偵錯] 下的瀏覽按鈕，在本機執行您新的 Web 專案。</span><span class="sxs-lookup"><span data-stu-id="7a378-244">Now, run your new web project locally by clicking the browse button under Debug.</span></span> <span data-ttu-id="7a378-245">此範例使用 Internet Explorer。</span><span class="sxs-lookup"><span data-stu-id="7a378-245">This example uses Internet Explorer.</span></span>
   
    ![Run project][HCVSRunProject]
2. <span data-ttu-id="7a378-247">在預設網頁的右上方，選擇 [註冊]  以註冊新帳戶：</span><span class="sxs-lookup"><span data-stu-id="7a378-247">On the upper right of the default web page, choose **Register** to register a new account:</span></span>
   
    ![Register a new account][HCVSRegisterLocally]
3. <span data-ttu-id="7a378-249">輸入使用者名稱和密碼：</span><span class="sxs-lookup"><span data-stu-id="7a378-249">Enter a user name and password:</span></span>
   
    ![Enter user name and password][HCVSCreateNewAccount]
   
    <span data-ttu-id="7a378-251">這會在您的本機 SQL Server 上自動建立一個資料庫，存放您應用程式的成員資格資訊。</span><span class="sxs-lookup"><span data-stu-id="7a378-251">This automatically creates a database on your local SQL Server that holds the membership information for your application.</span></span> <span data-ttu-id="7a378-252">其中一個資料表 (**dbo.AspNetUsers**) 包含如同您剛剛輸入的 Web 應用程式使用者認證。</span><span class="sxs-lookup"><span data-stu-id="7a378-252">One of the tables (**dbo.AspNetUsers**) holds web app user credentials like the ones that you just entered.</span></span> <span data-ttu-id="7a378-253">稍後在教學課程中會看見此資料表。</span><span class="sxs-lookup"><span data-stu-id="7a378-253">You will see this table later in the tutorial.</span></span>
4. <span data-ttu-id="7a378-254">關閉預設網頁的瀏覽器視窗。</span><span class="sxs-lookup"><span data-stu-id="7a378-254">Close the browser window of the default web page.</span></span> <span data-ttu-id="7a378-255">這會停止 Visual Studio 中的應用程式。</span><span class="sxs-lookup"><span data-stu-id="7a378-255">This stops the application in Visual Studio.</span></span>

<span data-ttu-id="7a378-256">現在您已可執行下一個步驟，也就是將應用程式發行至 Azure，並加以測試。</span><span class="sxs-lookup"><span data-stu-id="7a378-256">You are now ready for the next step, which is to publish the application to Azure and test it.</span></span>

<a name="PubNTest"></a>

## <a name="f-publish-the-web-application-to-azure-and-test-it"></a><span data-ttu-id="7a378-257">F.</span><span class="sxs-lookup"><span data-stu-id="7a378-257">F.</span></span> <span data-ttu-id="7a378-258">將 Web 應用程式發行至 Azure 並加以測試</span><span class="sxs-lookup"><span data-stu-id="7a378-258">Publish the web application to Azure and test it</span></span>
<span data-ttu-id="7a378-259">現在，您會將應用程式發行至您的 App Service Web 應用程式並加以測試，以確認您先前設定的混合式連線是否可用來將您的 Web 應用程式連接到本機電腦上的資料庫。</span><span class="sxs-lookup"><span data-stu-id="7a378-259">Now, you'll publish your application to your App Service web app and then test it to see how the hybrid connection you configured earlier is being used to connect your web app to the database on your local machine.</span></span>

### <a name="publish-the-web-application"></a><span data-ttu-id="7a378-260">發行 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="7a378-260">Publish the web application</span></span>
1. <span data-ttu-id="7a378-261">您可以在 Azure 入口網站中下載 App Service Web 應用程式的發行設定檔。</span><span class="sxs-lookup"><span data-stu-id="7a378-261">You can download your publishing profile for the App Service web app in the Azure Portal.</span></span> <span data-ttu-id="7a378-262">在您 Web 應用程式的分頁上，按一下 [取得發行設定檔] ，然後將檔案儲存至您的電腦。</span><span class="sxs-lookup"><span data-stu-id="7a378-262">On the blade for your web app, click **Get publish profile**, and then save the file to your computer.</span></span>
   
    ![Download publish profile][PortalDownloadPublishProfile]
   
    <span data-ttu-id="7a378-264">接著，您會將此檔案匯入 Visual Studio Web 應用程式中。</span><span class="sxs-lookup"><span data-stu-id="7a378-264">Next, you will import this file into your Visual Studio web application.</span></span>
2. <span data-ttu-id="7a378-265">在 Visual Studio 的 [方案總管] 中，以滑鼠右鍵按一下專案名稱，並選取 [發行] 。</span><span class="sxs-lookup"><span data-stu-id="7a378-265">In Visual Studio, right-click the project name in Solution Explorer and select **Publish**.</span></span>
   
    ![Select publish][HCVSRightClickProjectSelectPublish]
3. <span data-ttu-id="7a378-267">在 [發佈 Web] 對話方塊的 [設定檔] 索引標籤上，選擇 [匯入]。</span><span class="sxs-lookup"><span data-stu-id="7a378-267">In the **Publish Web** dialog, on the **Profile** tab, choose **Import**.</span></span>
   
    ![Import][HCVSPublishWebDialogImport]
4. <span data-ttu-id="7a378-269">瀏覽至您已下載的發行設定檔並加以選取，然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="7a378-269">Browse to your downloaded publishing profile, select it, and then click **OK**.</span></span>
   
    ![Browse to profile][HCVSBrowseToImportPubProfile]
5. <span data-ttu-id="7a378-271">您的發行資訊會匯入並顯示在對話方塊的 [連線]  索引標籤上。</span><span class="sxs-lookup"><span data-stu-id="7a378-271">Your publishing information is imported and displays on the **Connection** tab of the dialog.</span></span>
   
    ![Click Publish][HCVSClickPublish]
   
    <span data-ttu-id="7a378-273">按一下 [發行] 。</span><span class="sxs-lookup"><span data-stu-id="7a378-273">Click **Publish**.</span></span>
   
    <span data-ttu-id="7a378-274">發行完成後，瀏覽器將會啟動並顯示您熟悉的 ASP.NET 應用程式，差別在於網站現在已運作於 Azure 雲端中。</span><span class="sxs-lookup"><span data-stu-id="7a378-274">When publishing completes, your browser will launch and show your now familiar ASP.NET application -- except that now it is live in the Azure cloud!</span></span>

<span data-ttu-id="7a378-275">接著，您將使用即時 Web 應用程式來檢視其運作中的混合式連線。</span><span class="sxs-lookup"><span data-stu-id="7a378-275">Next, you will use your live web application to see its Hybrid Connection in action.</span></span>

### <a name="test-the-completed-web-application-on-azure"></a><span data-ttu-id="7a378-276">測試 Azure 上已完成的 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="7a378-276">Test the completed web application on Azure</span></span>
1. <span data-ttu-id="7a378-277">在您位於 Azure 上的網頁中，從右上方選擇 [登入] 。</span><span class="sxs-lookup"><span data-stu-id="7a378-277">On the top right of your web page on Azure, choose **Log in**.</span></span>
   
    ![Test log in][HCTestLogIn]
2. <span data-ttu-id="7a378-279">您的 App Service Web 應用程式現在已連接到您本機電腦上的 Web 應用程式成員資格資料庫。</span><span class="sxs-lookup"><span data-stu-id="7a378-279">Your App Service web app is now connected to your web application's membership database on your local machine.</span></span> <span data-ttu-id="7a378-280">若要驗證這一點，請以您先前在本機資料庫中輸入的相同認證登入。</span><span class="sxs-lookup"><span data-stu-id="7a378-280">To verify this, log in with the same credentials that you entered in the local database earlier.</span></span>
   
    ![Hello greeting][HCTestHelloContoso]
3. <span data-ttu-id="7a378-282">若要進一步測試新的混合式連線，請登出您的 Azure Web 應用程式，再以另一名使用者的身分註冊。</span><span class="sxs-lookup"><span data-stu-id="7a378-282">To further test your new hybrid connection, log off of your Azure web application and register as another user.</span></span> <span data-ttu-id="7a378-283">提供新的使用者名稱和密碼，然後按一下 [註冊] 。</span><span class="sxs-lookup"><span data-stu-id="7a378-283">Provide a new user name and password, and then click **Register**.</span></span>
   
    ![Test register another user][HCTestRegisterRelecloud]
4. <span data-ttu-id="7a378-285">若要驗證新使用者的認證已透過混合式連線儲存在您的本機資料庫中，請在本機電腦上開啟 SQL Management Studio。</span><span class="sxs-lookup"><span data-stu-id="7a378-285">To verify that the new user's credentials have been stored in your local database through your hybrid connection, open SQL Management Studio on your local computer.</span></span> <span data-ttu-id="7a378-286">在 [物件總管] 中展開 **MembershipDB** 資料庫，然後展開 [資料表]。</span><span class="sxs-lookup"><span data-stu-id="7a378-286">In Object Explorer, expand the **MembershipDB** database, and then expand **Tables**.</span></span> <span data-ttu-id="7a378-287">以滑鼠右鍵按一下 **dbo.AspNetUsers** 成員資格資料表，然後選擇 [選取前 1000 個資料列] 以檢視結果。</span><span class="sxs-lookup"><span data-stu-id="7a378-287">Right-click the **dbo.AspNetUsers** membership table and choose **Select Top 1000 Rows** to view the results.</span></span>
   
    ![View the results][HCTestSSMSTree]
5. <span data-ttu-id="7a378-289">您的本機成員資格資料表此時會將兩個帳戶都顯示出來 - 您在本機建立的帳戶，以及您在 Azure 雲端中建立的帳戶。</span><span class="sxs-lookup"><span data-stu-id="7a378-289">Your local membership table now shows both accounts - the one that you created locally, and the one that you created in the Azure cloud.</span></span> <span data-ttu-id="7a378-290">您在雲端中建立的帳戶已透過 Azure 的混合式連線功能儲存到您的內部部署資料庫。</span><span class="sxs-lookup"><span data-stu-id="7a378-290">The one that you created in the cloud has been saved to your on-premises database through Azure's Hybrid Connection feature.</span></span>
   
    ![Registered users in on-premises database][HCTestShowMemberDb]

<span data-ttu-id="7a378-292">現在，您已在 Azure 雲端中的 Web 應用程式與內部部署 SQL Server 資料庫之間，建立並部署使用混合式連線的 ASP.NET Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="7a378-292">You have now created and deployed an ASP.NET web application that uses a hybrid connection between a web app in the Azure cloud and an on-premises SQL Server database.</span></span> <span data-ttu-id="7a378-293">恭喜！</span><span class="sxs-lookup"><span data-stu-id="7a378-293">Congratulations!</span></span>

## <a name="see-also"></a><span data-ttu-id="7a378-294">另請參閱</span><span class="sxs-lookup"><span data-stu-id="7a378-294">See Also</span></span>
[<span data-ttu-id="7a378-295">混合式連線概觀</span><span class="sxs-lookup"><span data-stu-id="7a378-295">Hybrid Connections overview</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=397274)

[<span data-ttu-id="7a378-296">Josh Twist 介紹混合式連線 (第 9 頻道視訊)</span><span class="sxs-lookup"><span data-stu-id="7a378-296">Josh Twist introduces hybrid connections (Channel 9 video)</span></span>](http://channel9.msdn.com/Shows/Azure-Friday/Josh-Twist-introduces-hybrid-connections)

[<span data-ttu-id="7a378-297">混合式連線概觀</span><span class="sxs-lookup"><span data-stu-id="7a378-297">Hybrid Connections overview</span></span>](/services/biztalk-services/)

[<span data-ttu-id="7a378-298">BizTalk 服務：儀表板、監視器、調整、設定和混合式連線索引標籤</span><span class="sxs-lookup"><span data-stu-id="7a378-298">BizTalk Services: Dashboard, Monitor, Scale, Configure, and Hybrid Connection tabs</span></span>](../biztalk-services/biztalk-dashboard-monitor-scale-tabs.md)

[<span data-ttu-id="7a378-299">透過絕佳的應用程式可攜性建置真實的混合式雲端 (第 9 頻道視訊)</span><span class="sxs-lookup"><span data-stu-id="7a378-299">Building a Real-World Hybrid Cloud with Seamless Application Portability (Channel 9 video)</span></span>](http://channel9.msdn.com/events/TechEd/NorthAmerica/2014/DCIM-B323#fbid=)

[<span data-ttu-id="7a378-300">在 Azure App Service 中使用混合式連線存取內部部署資源</span><span class="sxs-lookup"><span data-stu-id="7a378-300">Access on-premises resources using hybrid connections in Azure App Service</span></span>](web-sites-hybrid-connection-get-started.md)

[<span data-ttu-id="7a378-301">ASP.NET 身分識別概觀</span><span class="sxs-lookup"><span data-stu-id="7a378-301">ASP.NET Identity Overview</span></span>](http://www.asp.net/identity)

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
