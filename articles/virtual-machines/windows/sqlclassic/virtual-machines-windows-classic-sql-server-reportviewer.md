---
title: "aaaUse 網站中的 ReportViewer |Microsoft 文件"
description: "本主題描述如何 toobuild Microsoft Azure Web 網站會顯示報表的 hello Visual Studio ReportViewer 控制項一起儲存在 Microsoft Azure 虛擬機器。"
services: virtual-machines-windows
documentationcenter: na
author: guyinacube
manager: erikre
editor: monicar
tags: azure-service-management
ms.assetid: 78b76318-d9bf-48ef-9d9e-d1b7d8cf3042
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/11/2017
ms.author: asaxton
ms.openlocfilehash: 8e0729d6657f96c32a9ac7dffdff7745ff92b48d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-reportviewer-in-a-web-site-hosted-in-azure"></a><span data-ttu-id="99bc5-103">在裝載於 Azure 上的網站中使用 ReportViewer</span><span class="sxs-lookup"><span data-stu-id="99bc5-103">Use ReportViewer in a Web Site Hosted in Azure</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="99bc5-104">Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../../azure-resource-manager/resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="99bc5-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="99bc5-105">本文件涵蓋使用 hello 傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="99bc5-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="99bc5-106">Microsoft 建議最新的部署使用 hello 資源管理員的模型。</span><span class="sxs-lookup"><span data-stu-id="99bc5-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="99bc5-107">您可以建立 Microsoft Azure 網站以 hello Visual Studio ReportViewer 控制項，會顯示報表，儲存在 Microsoft Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="99bc5-107">You can build a Microsoft Azure Web site with hello Visual Studio ReportViewer control that displays a report stored on an Microsoft Azure Virtual Machine.</span></span> <span data-ttu-id="99bc5-108">hello ReportViewer 控制項是 Web 應用程式中，建立使用 hello ASP.NET Web 應用程式範本。</span><span class="sxs-lookup"><span data-stu-id="99bc5-108">hello ReportViewer control is in a Web application that you build using hello ASP.NET Web application template.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="99bc5-109">hello ASP.NET MVC Web 應用程式範本不支援 hello ReportViewer 控制項。</span><span class="sxs-lookup"><span data-stu-id="99bc5-109">hello ASP.NET MVC Web Application templates do not support hello ReportViewer control.</span></span>

<span data-ttu-id="99bc5-110">tooincorporate ReportViewer 您 Microsoft Azure 網站中的，您需要 toocomplete hello 下列工作。</span><span class="sxs-lookup"><span data-stu-id="99bc5-110">tooincorporate ReportViewer into your Microsoft Azure Web site, you need toocomplete hello following tasks.</span></span>

* <span data-ttu-id="99bc5-111">**新增**組件 toohello 部署套件</span><span class="sxs-lookup"><span data-stu-id="99bc5-111">**Add** Assemblies toohello Deployment Package</span></span>
* <span data-ttu-id="99bc5-112">**設定** 驗證和授權</span><span class="sxs-lookup"><span data-stu-id="99bc5-112">**Configure** Authentication and Authorization</span></span>
* <span data-ttu-id="99bc5-113">**發行**hello ASP.NET Web 應用程式 tooAzure</span><span class="sxs-lookup"><span data-stu-id="99bc5-113">**Publish** hello ASP.NET Web application tooAzure</span></span>

## <a name="prerequisites"></a><span data-ttu-id="99bc5-114">必要條件</span><span class="sxs-lookup"><span data-stu-id="99bc5-114">Prerequisites</span></span>
<span data-ttu-id="99bc5-115">檢閱中的 hello 「 一般建議和最佳作法 」 一節[Azure 虛擬機器中 SQL Server Business Intelligence](../classic/ps-sql-bi.md)。</span><span class="sxs-lookup"><span data-stu-id="99bc5-115">Review hello “General recommendation and best practices” section in [SQL Server Business Intelligence in Azure Virtual Machines](../classic/ps-sql-bi.md).</span></span>

> [!NOTE]
> <span data-ttu-id="99bc5-116">ReportViewer 控制項隨附於 Visual Studio (Standard Edition 以上版本) 中。</span><span class="sxs-lookup"><span data-stu-id="99bc5-116">ReportViewer controls are shipped with Visual Studio, Standard Edition or above.</span></span> <span data-ttu-id="99bc5-117">如果您使用 hello Web Developer Express 版，您必須安裝 hello [MICROSOFT REPORT VIEWER 2012 RUNTIME](https://www.microsoft.com/download/details.aspx?id=35747) toouse hello ReportViewer 執行階段功能。</span><span class="sxs-lookup"><span data-stu-id="99bc5-117">If you are using hello Web Developer Express Edition, you must install hello [MICROSOFT REPORT VIEWER 2012 RUNTIME](https://www.microsoft.com/download/details.aspx?id=35747) toouse hello ReportViewer runtime features.</span></span>
> 
> <span data-ttu-id="99bc5-118">Microsoft Azure 不支援在本機處理模式中設定的 ReportViewer。</span><span class="sxs-lookup"><span data-stu-id="99bc5-118">ReportViewer configured in local processing mode is not supported in Microsoft Azure.</span></span>

## <a name="adding-assemblies-toohello-deployment-package"></a><span data-ttu-id="99bc5-119">加入組件 toohello 部署套件</span><span class="sxs-lookup"><span data-stu-id="99bc5-119">Adding Assemblies toohello Deployment Package</span></span>
<span data-ttu-id="99bc5-120">當您裝載 ASP.NET 應用程式在內部時，hello ReportViewer 組件通常會直接在 hello IIS 伺服器的 hello 全域組件快取 (GAC) 中安裝 Visual Studio 安裝期間，並且 hello 應用程式可以直接存取。</span><span class="sxs-lookup"><span data-stu-id="99bc5-120">When you host your ASP.NET application on-premises, hello ReportViewer assemblies are usually installed directly in hello global assembly cache (GAC) of hello IIS server during Visual Studio installation, and can be accessed directly by hello application.</span></span> <span data-ttu-id="99bc5-121">不過，當您的主機在 hello 雲端中，Microsoft Azure ASP.NET 應用程式不允許任何項目 toobe 安裝到 hello GAC，因此您必須確定 hello ReportViewer 組件可在本機上提供您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="99bc5-121">However, when you host your ASP.NET application in hello cloud, Microsoft Azure does not allow anything toobe installed into hello GAC, so you must make sure hello ReportViewer assemblies are available locally for your application.</span></span> <span data-ttu-id="99bc5-122">您可以將您的專案中參考 toothem 達到此目的，及設定這些 toobe 在本機複製。</span><span class="sxs-lookup"><span data-stu-id="99bc5-122">You can do this by adding references toothem in your project and configure them toobe copied locally.</span></span>

<span data-ttu-id="99bc5-123">在遠端處理模式中，hello ReportViewer 控制項，請使用下列組件的 hello:</span><span class="sxs-lookup"><span data-stu-id="99bc5-123">In remote processing mode, hello ReportViewer control uses hello following assemblies:</span></span>

* <span data-ttu-id="99bc5-124">**Microsoft.ReportViewer.WebForms.dll**： 包含 hello ReportViewer 程式碼，您必須在頁面中 toouse ReportViewer。</span><span class="sxs-lookup"><span data-stu-id="99bc5-124">**Microsoft.ReportViewer.WebForms.dll**: Contains hello ReportViewer code, which you need toouse ReportViewer in your page.</span></span> <span data-ttu-id="99bc5-125">當您將 ReportViewer 控制項拖曳到 ASP.NET 頁面放入您的專案時，這個組件的參考會加入 tooyour 專案。</span><span class="sxs-lookup"><span data-stu-id="99bc5-125">A reference for this assembly is added tooyour project when you drop a ReportViewer control onto an ASP.NET page in your project.</span></span>
* <span data-ttu-id="99bc5-126">**Microsoft.ReportViewer.Common.dll**： 包含在執行階段 hello ReportViewer 控制項所使用的類別。</span><span class="sxs-lookup"><span data-stu-id="99bc5-126">**Microsoft.ReportViewer.Common.dll**: Contains classes used by hello ReportViewer control at run time.</span></span> <span data-ttu-id="99bc5-127">它不會自動加入 tooyour 專案。</span><span class="sxs-lookup"><span data-stu-id="99bc5-127">It is not automatically added tooyour project.</span></span>

### <a name="tooadd-a-reference-toomicrosoftreportviewercommon"></a><span data-ttu-id="99bc5-128">tooadd 參考 tooMicrosoft.ReportViewer.Common</span><span class="sxs-lookup"><span data-stu-id="99bc5-128">tooadd a reference tooMicrosoft.ReportViewer.Common</span></span>
* <span data-ttu-id="99bc5-129">以滑鼠右鍵按一下您的專案**參考**節點，然後選取**加入參考**，選取 hello 組件以 hello.NET 索引標籤，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="99bc5-129">Right-click your project’s **References** node and select **Add Reference**, select hello assembly in hello .NET tab, and click **OK**.</span></span>

### <a name="toomake-hello-assemblies-locally-accessible-by-your-aspnet-application"></a><span data-ttu-id="99bc5-130">在本機上存取您的 ASP.NET 應用程式的 toomake hello 組件</span><span class="sxs-lookup"><span data-stu-id="99bc5-130">toomake hello assemblies locally accessible by your ASP.NET application</span></span>
1. <span data-ttu-id="99bc5-131">在 [hello**參考**資料夾中，按一下 hello Microsoft.ReportViewer.Common 組件，如此其屬性會顯示 hello 屬性] 窗格中。</span><span class="sxs-lookup"><span data-stu-id="99bc5-131">In hello **References** folder, click hello Microsoft.ReportViewer.Common assembly so that its properties appear in hello Properties pane.</span></span>
2. <span data-ttu-id="99bc5-132">在 [hello] 內容窗格中，設定**複製到本機**tooTrue。</span><span class="sxs-lookup"><span data-stu-id="99bc5-132">In hello Properties pane, set **Copy Local** tooTrue.</span></span>
3. <span data-ttu-id="99bc5-133">對 Microsoft.ReportViewer.WebForms 重複步驟 1 和 2。</span><span class="sxs-lookup"><span data-stu-id="99bc5-133">Repeat steps 1 and 2 for Microsoft.ReportViewer.WebForms.</span></span>

### <a name="tooget-reportviewer-language-pack"></a><span data-ttu-id="99bc5-134">tooget ReportViewer 語言套件</span><span class="sxs-lookup"><span data-stu-id="99bc5-134">tooget ReportViewer Language Pack</span></span>
1. <span data-ttu-id="99bc5-135">安裝 hello 適當 Microsoft Report Viewer 2012 Runtime 可轉散發套件從[Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=317386)。</span><span class="sxs-lookup"><span data-stu-id="99bc5-135">Install hello appropriate Microsoft Report Viewer 2012 Runtime redistributable package from [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=317386).</span></span>
2. <span data-ttu-id="99bc5-136">從下拉式清單中 hello 和 hello 頁面選取 hello 語言取得重新導向的 toohello 對應的下載中心頁面。</span><span class="sxs-lookup"><span data-stu-id="99bc5-136">Select hello language from hello dropdown list and hello page gets redirected toohello corresponding download center page.</span></span>
3. <span data-ttu-id="99bc5-137">按一下**下載**toostart hello 下載 ReportViewerLP.exe。</span><span class="sxs-lookup"><span data-stu-id="99bc5-137">Click **Download** toostart hello download of ReportViewerLP.exe.</span></span>
4. <span data-ttu-id="99bc5-138">下載 ReportViewerLP.exe 之後，請按一下**執行**tooinstall 立即，或按一下**儲存**toosave 它 tooyour 電腦。</span><span class="sxs-lookup"><span data-stu-id="99bc5-138">After you download ReportViewerLP.exe, click **Run** tooinstall immediately, or click **Save** toosave it tooyour computer.</span></span> <span data-ttu-id="99bc5-139">如果您按一下**儲存**，請記住 hello hello 儲存 hello 檔案的資料夾名稱。</span><span class="sxs-lookup"><span data-stu-id="99bc5-139">If you click **Save**, remember hello name of hello folder where you save hello file.</span></span>
5. <span data-ttu-id="99bc5-140">找出 hello 資料夾儲存 hello 檔案的位置。</span><span class="sxs-lookup"><span data-stu-id="99bc5-140">Locate hello folder where you saved hello file.</span></span> <span data-ttu-id="99bc5-141">在 ReportViewerLP.exe 上按一下滑鼠右鍵，按一下 以系統管理員身分執行，然後按一下是。</span><span class="sxs-lookup"><span data-stu-id="99bc5-141">Right-click ReportViewerLP.exe, click **Run as administrator**, and then click **Yes**.</span></span>
6. <span data-ttu-id="99bc5-142">執行 ReportViewerLP.exe 之後，您會看到 hello c:\windows\assembly 具有 hello 資源檔**Microsoft.ReportViewer.Webforms.Resources**和**Microsoft.ReportViewer.Common.Resources**.</span><span class="sxs-lookup"><span data-stu-id="99bc5-142">After running ReportViewerLP.exe, you will see hello c:\windows\assembly has hello resource files **Microsoft.ReportViewer.Webforms.Resources** and **Microsoft.ReportViewer.Common.Resources**.</span></span>

### <a name="tooconfigure-for-localized-reportviewer-control"></a><span data-ttu-id="99bc5-143">tooconfigure 當地語系化的 ReportViewer 控制項</span><span class="sxs-lookup"><span data-stu-id="99bc5-143">tooconfigure for localized ReportViewer control</span></span>
1. <span data-ttu-id="99bc5-144">下載並安裝下列 hello 上面指定的指示由 hello Microsoft Report Viewer 2012 Runtime 可轉散發套件。</span><span class="sxs-lookup"><span data-stu-id="99bc5-144">Download and install hello Microsoft Report Viewer 2012 Runtime redistributable package by following hello above specified instructions.</span></span>
2. <span data-ttu-id="99bc5-145">建立<language>hello 專案和複製 hello 資料夾相關聯的資源組件檔案。</span><span class="sxs-lookup"><span data-stu-id="99bc5-145">Create <language> folder in hello project and copy hello associated resource assembly files there.</span></span> <span data-ttu-id="99bc5-146">hello 複製的資源組件檔案 toobe 是： **Microsoft.ReportViewer.Webforms.Resources.dll**和**Microsoft.ReportViewer.Common.Resources.dll**。選取 hello 資源組件檔案，然後在 [hello] 內容窗格中，設定**複製 tooOutput 目錄**太"**永遠複製**"。</span><span class="sxs-lookup"><span data-stu-id="99bc5-146">hello resource assembly files toobe copied are: **Microsoft.ReportViewer.Webforms.Resources.dll** and **Microsoft.ReportViewer.Common.Resources.dll**.Select hello resource assembly files, and in hello Properties pane, set **Copy tooOutput Directory** too“**Copy always**”.</span></span>
3. <span data-ttu-id="99bc5-147">設定 hello hello web 專案的 Culture 和 UICulture。</span><span class="sxs-lookup"><span data-stu-id="99bc5-147">Set hello Culture & UICulture for hello web project.</span></span> <span data-ttu-id="99bc5-148">如需有關如何 tooset hello 文化特性和 UI 文化特性的 ASP.NET Web 網頁，請參閱[How to： 設定 ASP.NET Web 網頁全球化 hello 文化特性和 UI 文化特性](http://go.microsoft.com/fwlink/?LinkId=237461)。</span><span class="sxs-lookup"><span data-stu-id="99bc5-148">For more information about how tooset hello Culture and UI Culture for an ASP.NET Web page, see [How to: Set hello Culture and UI Culture for ASP.NET Web Page Globalization](http://go.microsoft.com/fwlink/?LinkId=237461).</span></span>

## <a name="configuring-authentication-and-authorization"></a><span data-ttu-id="99bc5-149">設定驗證和授權</span><span class="sxs-lookup"><span data-stu-id="99bc5-149">Configuring Authentication and Authorization</span></span>
<span data-ttu-id="99bc5-150">hello ReportViewer 需要 toouse 適當的認證 tooauthenticate 與 hello 報表伺服器，並 hello 認證必須經過 hello report server tooaccess hello 報表您想要授權。</span><span class="sxs-lookup"><span data-stu-id="99bc5-150">hello ReportViewer needs toouse proper credentials tooauthenticate with hello report server, and hello credentials must be authorized by hello report server tooaccess hello reports you want.</span></span> <span data-ttu-id="99bc5-151">如需驗證資訊，請參閱 hello 白皮書[Reporting Services 報表檢視器控制項和 Microsoft Azure 虛擬機器為基礎的報表伺服器](https://msdn.microsoft.com/library/azure/dn753698.aspx)。</span><span class="sxs-lookup"><span data-stu-id="99bc5-151">For information on authentication, see hello white paper [Reporting Services report viewer control and Microsoft Azure virtual machine based report servers](https://msdn.microsoft.com/library/azure/dn753698.aspx).</span></span>

## <a name="publish-hello-aspnet-web-application-tooazure"></a><span data-ttu-id="99bc5-152">發佈 ASP.NET Web 應用程式 tooAzure hello</span><span class="sxs-lookup"><span data-stu-id="99bc5-152">Publish hello ASP.NET Web application tooAzure</span></span>
<span data-ttu-id="99bc5-153">如需發佈 ASP.NET Web 應用程式 tooAzure 指示，請參閱[How to： 移轉並發行從 Visual Studio Web 應用程式 tooAzure](../../../vs-azure-tools-migrate-publish-web-app-to-cloud-service.md)和[開始使用 Web 應用程式和 ASP.NET](../../../app-service-web/app-service-web-get-started-dotnet.md)。</span><span class="sxs-lookup"><span data-stu-id="99bc5-153">For instructions on publishing an ASP.NET Web application tooAzure, see [How to: Migrate and Publish a Web Application tooAzure from Visual Studio](../../../vs-azure-tools-migrate-publish-web-app-to-cloud-service.md) and [Get started with Web Apps and ASP.NET](../../../app-service-web/app-service-web-get-started-dotnet.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="99bc5-154">如果 hello 加入 Azure 部署專案或加入 Azure 雲端服務專案命令沒有出現在方案總管 中的 hello 快顯功能表中，您可能需要 toochange hello 目標 framework 的 hello 專案 too.NET Framework 4。</span><span class="sxs-lookup"><span data-stu-id="99bc5-154">If hello Add Azure Deployment Project or Add Azure Cloud Service Project command does not appear in hello shortcut menu in Solution Explorer, you may need toochange hello Target framework for hello project too.NET Framework 4.</span></span>
> 
> <span data-ttu-id="99bc5-155">hello 兩個命令提供本質上 hello 相同的功能。</span><span class="sxs-lookup"><span data-stu-id="99bc5-155">hello two commands provide essentially hello same functionality.</span></span> <span data-ttu-id="99bc5-156">一或 hello 其他命令會出現在 hello 快顯功能表中的 hello Microsoft Azure SDK 版本而定，您已安裝。</span><span class="sxs-lookup"><span data-stu-id="99bc5-156">One or hello other command will appear in hello shortcut menu depending on which version of hello Microsoft Azure SDK you have installed.</span></span>
> 
> 

## <a name="resources"></a><span data-ttu-id="99bc5-157">資源</span><span class="sxs-lookup"><span data-stu-id="99bc5-157">Resources</span></span>
[<span data-ttu-id="99bc5-158">Microsoft 報告</span><span class="sxs-lookup"><span data-stu-id="99bc5-158">Microsoft Reports</span></span>](http://go.microsoft.com/fwlink/?LinkId=205399)

[<span data-ttu-id="99bc5-159">Azure 虛擬機器中的 SQL Server Business Intelligence</span><span class="sxs-lookup"><span data-stu-id="99bc5-159">SQL Server Business Intelligence in Azure Virtual Machines</span></span>](../classic/ps-sql-bi.md)

[<span data-ttu-id="99bc5-160">使用 PowerShell tooCreate Azure VM 具有原生模式報表伺服器</span><span class="sxs-lookup"><span data-stu-id="99bc5-160">Use PowerShell tooCreate an Azure VM With a Native Mode Report Server</span></span>](../classic/ps-sql-report.md)

