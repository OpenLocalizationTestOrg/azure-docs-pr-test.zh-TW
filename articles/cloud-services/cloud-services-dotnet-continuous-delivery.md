---
title: "在 Azure 中使用 TFS 持續傳遞雲端服務 | Microsoft Docs"
description: "了解如何設定 Azure 雲端應用程式的連續傳遞。 MSBuild 命令列陳述式和 PowerShell 指令碼的程式碼範例。"
services: cloud-services
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 4f3c93c6-5c82-4779-9d19-7404a01e82ca
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/12/2017
ms.author: kraigb
ms.openlocfilehash: 0979722b9ec715e91825c7aba74657451df6e83f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="continuous-delivery-for-cloud-services-in-azure"></a><span data-ttu-id="73ea6-104">Azure 中雲端服務的連續傳遞</span><span class="sxs-lookup"><span data-stu-id="73ea6-104">Continuous Delivery for Cloud Services in Azure</span></span>
<span data-ttu-id="73ea6-105">本文所述的程序顯示如何為 Azure 雲端應用程式設定連續傳遞。</span><span class="sxs-lookup"><span data-stu-id="73ea6-105">The process described in this article shows you how to set up continuous delivery for Azure cloud apps.</span></span> <span data-ttu-id="73ea6-106">此程序可讓您自動建立套件，並在每次程式碼簽入時將套件部署到 Azure。</span><span class="sxs-lookup"><span data-stu-id="73ea6-106">This process enables you to automatically create packages and deploy the package to Azure after every code check-in.</span></span> <span data-ttu-id="73ea6-107">本文所述的套件建置程序等同於 Visual Studio 中的 [封裝]命令，而發佈步驟等同於 Visual Studio 中的 [發佈] 命令。</span><span class="sxs-lookup"><span data-stu-id="73ea6-107">The package build process described in this article is equivalent to the **Package** command in Visual Studio, and the publishing steps are equivalent to the **Publish** command in Visual Studio.</span></span>
<span data-ttu-id="73ea6-108">文中會說明使用 MSBuild 命令列陳述式與指令碼來建置伺服器的方法，同時也會示範如何選擇性設定 Visual StudioTeam Foundation Server - Team Build 定義來使用 MSBuild 命令及 PowerShell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="73ea6-108">The article covers the methods you would use to create a build server with MSBuild command-line statements and Windows PowerShell scripts, and it also demonstrates how to optionally configure Visual Studio Team Foundation Server - Team Build definitions to use the MSBuild commands and PowerShell scripts.</span></span> <span data-ttu-id="73ea6-109">您可根據自己的組建環境及 Azure 目標環境自訂此程序。</span><span class="sxs-lookup"><span data-stu-id="73ea6-109">The process is customizable for your build environment and Azure target environments.</span></span>

<span data-ttu-id="73ea6-110">此動作也可以用 Visual Studio Team Services (託管於 Azure 中的 TFS 版本) 來執行，這樣會變得更容易。</span><span class="sxs-lookup"><span data-stu-id="73ea6-110">You can also use Visual Studio Team Services, a version of TFS that is hosted in Azure, to do this more easily.</span></span> 

<span data-ttu-id="73ea6-111">開始之前，您應該先從 Visual Studio 發佈應用程式。</span><span class="sxs-lookup"><span data-stu-id="73ea6-111">Before you start, you should publish your application from Visual Studio.</span></span>
<span data-ttu-id="73ea6-112">如此可確保當您嘗試將發佈程序自動化時，所有資源皆可用並已初始化。</span><span class="sxs-lookup"><span data-stu-id="73ea6-112">This will ensure that all the resources are available and initialized when you attempt to automate the publication process.</span></span>

## <a name="1-configure-the-build-server"></a><span data-ttu-id="73ea6-113">1：設定組建伺服器</span><span class="sxs-lookup"><span data-stu-id="73ea6-113">1: Configure the Build Server</span></span>
<span data-ttu-id="73ea6-114">您必須先在組建伺服器上安裝必要的軟體與工具，才能使用 MSBuild 建立 Azure 套件。</span><span class="sxs-lookup"><span data-stu-id="73ea6-114">Before you can create an Azure package by using MSBuild, you must install the required software and tools on the build server.</span></span>

<span data-ttu-id="73ea6-115">組建伺服器上不需要安裝 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="73ea6-115">Visual Studio is not required to be installed on the build server.</span></span> <span data-ttu-id="73ea6-116">若要使用 Team Foundation Build Service 來管理組建伺服器，請遵循 [Team Foundation Build Service][Team Foundation Build Service] 文件中的指示。</span><span class="sxs-lookup"><span data-stu-id="73ea6-116">If you want to use Team Foundation Build Service to manage your build server, follow the instructions in the [Team Foundation Build Service][Team Foundation Build Service] documentation.</span></span>

1. <span data-ttu-id="73ea6-117">在組建伺服器上，安裝 [.NET Framework 4.5.2][.NET Framework 4.5.2](其中包含 MSBuild)。</span><span class="sxs-lookup"><span data-stu-id="73ea6-117">On the build server, install the [.NET Framework 4.5.2][.NET Framework 4.5.2], which includes MSBuild.</span></span>
2. <span data-ttu-id="73ea6-118">安裝最新版的 [適用於 .NET 的 Azure 編寫工具](https://azure.microsoft.com/develop/net/)。</span><span class="sxs-lookup"><span data-stu-id="73ea6-118">Install the latest [Azure Authoring Tools for .NET](https://azure.microsoft.com/develop/net/).</span></span>
3. <span data-ttu-id="73ea6-119">安裝 [Azure Libraries for .NET](http://go.microsoft.com/fwlink/?LinkId=623519)。</span><span class="sxs-lookup"><span data-stu-id="73ea6-119">Install the [Azure Libraries for .NET](http://go.microsoft.com/fwlink/?LinkId=623519).</span></span>
4. <span data-ttu-id="73ea6-120">將 Microsoft.WebApplication.targets 檔案從 Visual Studio 安裝複製到組建伺服器上。</span><span class="sxs-lookup"><span data-stu-id="73ea6-120">Copy the Microsoft.WebApplication.targets file from a Visual Studio installation to the build server.</span></span>

   <span data-ttu-id="73ea6-121">在安裝 Visual Studio 的電腦上，此檔案位於目錄 C:\\Program Files(x86)\\MSBuild\\Microsoft\\VisualStudio\\v14.0\\WebApplications。</span><span class="sxs-lookup"><span data-stu-id="73ea6-121">On a computer with Visual Studio installed, this file is located in the directory C:\\Program Files(x86)\\MSBuild\\Microsoft\\VisualStudio\\v14.0\\WebApplications.</span></span> <span data-ttu-id="73ea6-122">您應該將它複製至組建伺服器上的相同目錄。</span><span class="sxs-lookup"><span data-stu-id="73ea6-122">You should copy it to the same directory on the build server.</span></span>
5. <span data-ttu-id="73ea6-123">安裝 [Azure Tools for Visual Studio](https://www.visualstudio.com/features/azure-tools-vs.aspx)。</span><span class="sxs-lookup"><span data-stu-id="73ea6-123">Install the [Azure Tools for Visual Studio](https://www.visualstudio.com/features/azure-tools-vs.aspx).</span></span>

## <a name="2-build-a-package-using-msbuild-commands"></a><span data-ttu-id="73ea6-124">2：使用 MSBuild 命令來建置封裝</span><span class="sxs-lookup"><span data-stu-id="73ea6-124">2: Build a Package using MSBuild Commands</span></span>
<span data-ttu-id="73ea6-125">本節說明如何建構 MSBuild 命令來建置 Azure 套件。</span><span class="sxs-lookup"><span data-stu-id="73ea6-125">This section describes how to construct an MSBuild command that builds an Azure package.</span></span> <span data-ttu-id="73ea6-126">在組建伺服器上執行這個步驟，確認一切都已正確設定，且 MSBuild 命令會執行您要它執行的動作。</span><span class="sxs-lookup"><span data-stu-id="73ea6-126">Run this step on the build server to verify that everything is configured correctly and that the MSBuild command does what you want it to do.</span></span> <span data-ttu-id="73ea6-127">您可以將此命令列新增至組建伺服器上的現有組建指令碼，也可以在 TFS 組建定義中使用此命令列 (說明於下節)。</span><span class="sxs-lookup"><span data-stu-id="73ea6-127">You can either add this command line to existing build scripts on the build server, or you can use the command line in a TFS Build Definition, as described in the next section.</span></span> <span data-ttu-id="73ea6-128">如需命令列參數及 MSBuild 的詳細資訊，請參閱 [MSBuild 命令列參考](https://msdn.microsoft.com/library/ms164311%28v=vs.140%29.aspx)。</span><span class="sxs-lookup"><span data-stu-id="73ea6-128">For more information about command-line parameters and MSBuild, see [MSBuild Command Line Reference](https://msdn.microsoft.com/library/ms164311%28v=vs.140%29.aspx).</span></span>

1. <span data-ttu-id="73ea6-129">如果組建伺服器上已安裝 Visual Studio，請在 Windows 的 [Visual Studio Tools] 資料夾中找出並選擇 [Visual Studio 命令提示字元]。</span><span class="sxs-lookup"><span data-stu-id="73ea6-129">If Visual Studio is installed on the build server, locate and choose **Visual Studio Command Prompt** in the **Visual Studio Tools** folder in Windows.</span></span>

   <span data-ttu-id="73ea6-130">如果組建伺服器上未安裝 Visual Studio，請開啟命令提示字元，並確定可在路徑上存取 MSBuild.exe。</span><span class="sxs-lookup"><span data-stu-id="73ea6-130">If Visual Studio is not installed on the build server, open a command prompt and make sure that MSBuild.exe is accessible on the path.</span></span> <span data-ttu-id="73ea6-131">MSBuild 會與 .NET Framework 一起安裝在路徑 %WINDIR%\\Microsoft.NET\\Framework\\Version。</span><span class="sxs-lookup"><span data-stu-id="73ea6-131">MSBuild is installed with the .NET Framework in the path %WINDIR%\\Microsoft.NET\\Framework\\*Version*.</span></span> <span data-ttu-id="73ea6-132">例如，若要在已安裝 .NET Framework 4 時，將 MSBuild.exe 新增至 PATH 環境變數，請在命令提示字元中輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="73ea6-132">For example, to add MSBuild.exe to the PATH environment variable when you have .NET Framework 4 installed, type the following command at the command prompt:</span></span>

       set PATH=%PATH%;"C:\Windows\Microsoft.NET\Framework\v4.0.30319"
2. <span data-ttu-id="73ea6-133">在命令提示字元中，瀏覽至包含您要建置之 Azure 專案檔案的資料夾。</span><span class="sxs-lookup"><span data-stu-id="73ea6-133">At the command prompt, navigate to the folder containing the Azure project file that you want to build.</span></span>
3. <span data-ttu-id="73ea6-134">搭配 /target:Publish 選項執行 MSBuild，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="73ea6-134">Run MSBuild with the /target:Publish option as in the following example:</span></span>

       MSBuild /target:Publish

   <span data-ttu-id="73ea6-135">此選項可以縮寫為 /t:Publish。</span><span class="sxs-lookup"><span data-stu-id="73ea6-135">This option can be abbreviated as /t:Publish.</span></span> <span data-ttu-id="73ea6-136">當已安裝 Azure SDK 時，MSBuild 中的 /t:Publish 選項不應該與 Visual Studio 中的 [發行] 命令混淆。</span><span class="sxs-lookup"><span data-stu-id="73ea6-136">The /t:Publish option in MSBuild should not be confused with the Publish commands available in Visual Studio when you have the Azure SDK installed.</span></span> <span data-ttu-id="73ea6-137">/t:Publish 選項只會建置 Azure 套件。</span><span class="sxs-lookup"><span data-stu-id="73ea6-137">The /t:Publish option only builds the Azure packages.</span></span> <span data-ttu-id="73ea6-138">其並不會如 Visual Studio 中的 [發行] 命令一樣部署套件。</span><span class="sxs-lookup"><span data-stu-id="73ea6-138">It does not deploy the packages as the Publish commands in Visual Studio do.</span></span>

   <span data-ttu-id="73ea6-139">(選擇性) 您可以指定專案名稱作為 MSBuild 參數。</span><span class="sxs-lookup"><span data-stu-id="73ea6-139">Optionally, you can specify the project name as an MSBuild parameter.</span></span> <span data-ttu-id="73ea6-140">如果未指定，則會使用目前目錄。</span><span class="sxs-lookup"><span data-stu-id="73ea6-140">If not specified, the current directory is used.</span></span> <span data-ttu-id="73ea6-141">如需 MSBuild 命令列選項的詳細資訊，請參閱 [MSBuild 命令列參考](https://msdn.microsoft.com/library/ms164311%28v=vs.140%29.aspx)。</span><span class="sxs-lookup"><span data-stu-id="73ea6-141">For more information about MSBuild command line options, see [MSBuild Command Line Reference](https://msdn.microsoft.com/library/ms164311%28v=vs.140%29.aspx).</span></span>
4. <span data-ttu-id="73ea6-142">尋找輸出。</span><span class="sxs-lookup"><span data-stu-id="73ea6-142">Locate the output.</span></span> <span data-ttu-id="73ea6-143">依預設，這個命令會在相對於專案根資料夾的目錄中建立目錄，例如 ProjectDir\\bin\\Configuration\\app.publish\\。</span><span class="sxs-lookup"><span data-stu-id="73ea6-143">By default, this command creates a directory in relation to the root folder for the project, such as *ProjectDir*\\bin\\*Configuration*\\app.publish\\.</span></span> <span data-ttu-id="73ea6-144">當您建置 Azure 專案時，會產生兩個檔案，即套件檔本身及伴隨的組態檔：</span><span class="sxs-lookup"><span data-stu-id="73ea6-144">When you build an Azure project, you generate two files, the package file itself and the accompanying configuration file:</span></span>

   * <span data-ttu-id="73ea6-145">Project.cspkg</span><span class="sxs-lookup"><span data-stu-id="73ea6-145">Project.cspkg</span></span>
   * <span data-ttu-id="73ea6-146">ServiceConfiguration.*TargetProfile*.cscfg</span><span class="sxs-lookup"><span data-stu-id="73ea6-146">ServiceConfiguration.*TargetProfile*.cscfg</span></span>

   <span data-ttu-id="73ea6-147">依預設，每個 Azure 專案都會包含一個服務組態檔 (.cscfg 檔) 用於本機 (偵錯) 組建，以及另一個服務組態檔用於 (預備或生產) 雲端組建，但是您可以視需要新增或移除服務組態檔。</span><span class="sxs-lookup"><span data-stu-id="73ea6-147">By default, each Azure project includes one service configuration file (.cscfg file) for local (debugging) builds and another for cloud (staging or production) builds, but you can add or remove service configuration files as needed.</span></span> <span data-ttu-id="73ea6-148">在 Visual Studio 內建置套件時，系統將問您要隨套件包含哪個服務組態檔。</span><span class="sxs-lookup"><span data-stu-id="73ea6-148">When you build a package within Visual Studio, you will be asked which service configuration file to include alongside the package.</span></span>
5. <span data-ttu-id="73ea6-149">指定服務組態檔。</span><span class="sxs-lookup"><span data-stu-id="73ea6-149">Specify the service configuration file.</span></span> <span data-ttu-id="73ea6-150">使用 MSBuild 來建置套件時，預設會包含本機服務組態檔。</span><span class="sxs-lookup"><span data-stu-id="73ea6-150">When you build a package by using MSBuild, the local service configuration file is included by default.</span></span> <span data-ttu-id="73ea6-151">若要包含不同的服務組態檔，請設定 MSBuild 命令的 TargetProfile 屬性，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="73ea6-151">To include a different service configuration file, set the TargetProfile property of the MSBuild command, as in the following example:</span></span>

       MSBuild /t:Publish /p:TargetProfile=Cloud
6. <span data-ttu-id="73ea6-152">指定輸出的位置。</span><span class="sxs-lookup"><span data-stu-id="73ea6-152">Specify the location for the output.</span></span> <span data-ttu-id="73ea6-153">使用 /p:PublishDir=Directory\\ 選項來設定路徑 (包括最後的反斜線分隔符號)，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="73ea6-153">Set the path by using the /p:PublishDir=*Directory*\\ option, including the trailing backslash separator, as in the following example:</span></span>

       MSBuild /target:Publish /p:PublishDir=\\myserver\drops\

   <span data-ttu-id="73ea6-154">一旦建構並測試出適當的 MSBuild 命令列來建置專案並將它們結合為 Azure 套件，就可以將此命令新增至組建指令碼。</span><span class="sxs-lookup"><span data-stu-id="73ea6-154">Once you've constructed and tested an appropriate MSBuild command line to build your projects and combine them into an Azure package, you can add this command line to your build scripts.</span></span> <span data-ttu-id="73ea6-155">如果您的組建伺服器使用自訂指令碼，則此程序將視您自訂建置流程的特性而定。</span><span class="sxs-lookup"><span data-stu-id="73ea6-155">If your build server uses custom scripts, this process will depend on the specifics of your custom build process.</span></span> <span data-ttu-id="73ea6-156">如果您是使用 TFS 作為組建環境，則可以遵循下一步中的指示，將 Azure 套件新增至組建程序。</span><span class="sxs-lookup"><span data-stu-id="73ea6-156">If you are using TFS as a build environment, then you can follow the instructions in the next step to add the Azure package build to your build process.</span></span>

## <a name="3-build-a-package-using-tfs-team-build"></a><span data-ttu-id="73ea6-157">3：使用 TFS Team Build 建置封裝</span><span class="sxs-lookup"><span data-stu-id="73ea6-157">3: Build a Package using TFS Team Build</span></span>
<span data-ttu-id="73ea6-158">如果已設定 Team Foundation Server (TFS) 做為組建控制器，並設定組建伺服器做為 TFS 組建電腦，則可選擇性地為 Azure 套件設定自動化組建。</span><span class="sxs-lookup"><span data-stu-id="73ea6-158">If you have Team Foundation Server (TFS) set up as a build controller and the build server set up as a TFS build machine, then you can optionally set up an automated build for your Azure package.</span></span> <span data-ttu-id="73ea6-159">如需如何設定並使用 Team Foundation Server 作為組建系統的相關資訊，請參閱[相應放大您的組建系統][Scale out your build system]。</span><span class="sxs-lookup"><span data-stu-id="73ea6-159">For information on how to set up and use Team Foundation server as a build system, see [Scale out your build system][Scale out your build system].</span></span> <span data-ttu-id="73ea6-160">特別的是，下列程序假設您已經如[部署和設定組建伺服器][Deploy and configure a build server]所述來設定組建伺服器，也已建立 Team 專案，並在 Team 專案中建立雲端服務專案。</span><span class="sxs-lookup"><span data-stu-id="73ea6-160">In particular, the following procedure assumes that you have configured your build server as described in [Deploy and configure a build server][Deploy and configure a build server], and that you have created a team project, created a cloud service project in the team project.</span></span>

<span data-ttu-id="73ea6-161">若要設定 TFS 來建置 Azure 套件，請執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="73ea6-161">To configure TFS to build Azure packages, perform the following steps:</span></span>

1. <span data-ttu-id="73ea6-162">在開發電腦上的 Visual Studio 中，於 [檢視] 功能表上，選取 [Team Explorer] 或選取 Ctrl+\\、Ctrl+M。</span><span class="sxs-lookup"><span data-stu-id="73ea6-162">In Visual Studio on your development computer, on the View menu, choose **Team Explorer**, or choose Ctrl+\\, Ctrl+M.</span></span> <span data-ttu-id="73ea6-163">在 Team Explorer 視窗中，展開 [組建] 節點或選擇 [組建] 頁面，然後選擇 [新增組建定義]。</span><span class="sxs-lookup"><span data-stu-id="73ea6-163">In the Team Explorer window, expand the **Builds** node or choose the **Builds** page, and choose **New Build Definition**.</span></span>

   ![新增組建定義選項][0]
2. <span data-ttu-id="73ea6-165">選擇 [觸發程序]  索引標籤，然後指定所需的條件來代表套件的組建時機。</span><span class="sxs-lookup"><span data-stu-id="73ea6-165">Choose the **Trigger** tab, and specify the desired conditions for when you want the package to be built.</span></span> <span data-ttu-id="73ea6-166">例如，指定 [連續整合]  ，會在每次發生原始檔控制簽入時建置套件。</span><span class="sxs-lookup"><span data-stu-id="73ea6-166">For example, specify **Continuous Integration** to build the package whenever a source control check-in occurs.</span></span>
3. <span data-ttu-id="73ea6-167">選擇 [來源設定] 索引標籤，然後確定您的專案資料夾列在 [原始檔控制資料夾] 資料行中，並且狀態為 [作用中]。</span><span class="sxs-lookup"><span data-stu-id="73ea6-167">Choose the **Source Settings** tab, and make sure your project folder is listed in the **Source Control Folder** column, and the status is **Active**.</span></span>
4. <span data-ttu-id="73ea6-168">選擇 [組建預設值]  索引標籤，然後在 [組建控制器] 下，確認組建伺服器的名稱無誤。</span><span class="sxs-lookup"><span data-stu-id="73ea6-168">Choose the **Build Defaults** tab, and under Build controller, verify the name of the build server.</span></span>  <span data-ttu-id="73ea6-169">同時，選擇 [將組建輸出複製至下列置放資料夾]  選項，並指定所需的置放位置。</span><span class="sxs-lookup"><span data-stu-id="73ea6-169">Also, choose the option **Copy build output to the following drop folder** and specify the desired drop location.</span></span>
5. <span data-ttu-id="73ea6-170">選擇 [觸發程序]  索引標籤。在 [處理序] 索引標籤上選擇預設範本，於 [組建] 下，選擇專案 (若尚未選取)，然後展開 [組建] 格線區段中的 [進階] 區段。</span><span class="sxs-lookup"><span data-stu-id="73ea6-170">Choose the **Process** tab. On the Process tab, choose the default template, under **Build**, choose the project if it is not already selected, and expand the **Advanced** section in the **Build** section of the grid.</span></span>
6. <span data-ttu-id="73ea6-171">選擇 [MSBuild 引數]，然後依上面步驟 2 所述，設定適當的 MSBuild 命令列引數。</span><span class="sxs-lookup"><span data-stu-id="73ea6-171">Choose **MSBuild Arguments**, and set the appropriate MSBuild command line arguments as described in Step 2 above.</span></span> <span data-ttu-id="73ea6-172">例如，輸入 **/t:Publish /p:PublishDir=\\\\myserver\\drops\\** 以建置套件，並將套件檔複製到位置 \\\\myserver\\drops\\：</span><span class="sxs-lookup"><span data-stu-id="73ea6-172">For example, enter **/t:Publish /p:PublishDir=\\\\myserver\\drops\\** to build a package and copy the package files to the location \\\\myserver\\drops\\:</span></span>

   ![MSBuild 引數][2]

   > [!NOTE]
   > <span data-ttu-id="73ea6-174">將檔案複製到公用共用，將可更輕鬆地手動從開發電腦部署套件。</span><span class="sxs-lookup"><span data-stu-id="73ea6-174">Copying the files to a public share makes it easier to manually deploy the packages from your development computer.</span></span>
7. <span data-ttu-id="73ea6-175">簽入專案的變更來測試組建步驟是否成功，或將新組建排入佇列。</span><span class="sxs-lookup"><span data-stu-id="73ea6-175">Test the success of your build step by checking in a change to your project, or queue up a new build.</span></span> <span data-ttu-id="73ea6-176">若要將新組建排入佇列，請在 Team Explorer 的 [所有組建定義] 上按一下滑鼠右鍵，然後選擇 [將新組建排入佇列]。</span><span class="sxs-lookup"><span data-stu-id="73ea6-176">To queue up a new build, in the Team Explorer, right-click **All Build Definitions,** and then choose **Queue New Build**.</span></span>

## <a name="4-publish-a-package-using-a-powershell-script"></a><span data-ttu-id="73ea6-177">4：使用 PowerShell 指令碼來發佈封裝</span><span class="sxs-lookup"><span data-stu-id="73ea6-177">4: Publish a Package using a PowerShell Script</span></span>
<span data-ttu-id="73ea6-178">本節說明如何建構 Windows PowerShell 指令碼，以使用選用參數將雲端應用程式套件發佈至 Azure。</span><span class="sxs-lookup"><span data-stu-id="73ea6-178">This section describes how to construct a Windows PowerShell script that will publish the Cloud app package output to Azure using optional parameters.</span></span> <span data-ttu-id="73ea6-179">呼叫此指令碼的時機可以是執行自訂組建自動化中的組建步驟之後。</span><span class="sxs-lookup"><span data-stu-id="73ea6-179">This script can be called after the build step in your custom build automation.</span></span> <span data-ttu-id="73ea6-180">也可以從 Visual Studio TFS Team Build 中的「流程範本」工作流程活動中呼叫。</span><span class="sxs-lookup"><span data-stu-id="73ea6-180">It can also be called from Process Template workflow activities in Visual Studio TFS Team Build.</span></span>

1. <span data-ttu-id="73ea6-181">安裝 [Azure PowerShell Cmdlet][Azure PowerShell cmdlets] (0.6.1 版或更高版本)。</span><span class="sxs-lookup"><span data-stu-id="73ea6-181">Install the [Azure PowerShell cmdlets][Azure PowerShell cmdlets] (v0.6.1 or higher).</span></span>
   <span data-ttu-id="73ea6-182">在 Cmdlet 設定階段期間，請選擇安裝為嵌入式管理單元。</span><span class="sxs-lookup"><span data-stu-id="73ea6-182">During the cmdlet setup phase, choose to install as a snap-in.</span></span> <span data-ttu-id="73ea6-183">請注意，此正式支援的版本會取代透過 CodePlex 提供的更舊版本 (這些舊版本的編號為 2.x.x)。</span><span class="sxs-lookup"><span data-stu-id="73ea6-183">Note that this officially supported version replaces the older version offered through CodePlex, although the previous versions were numbered 2.x.x.</span></span>
2. <span data-ttu-id="73ea6-184">使用 [開始] 功能表或 [開始] 頁面啟動 Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="73ea6-184">Start Azure PowerShell using the Start menu or Start page.</span></span> <span data-ttu-id="73ea6-185">如果以此方式啟動，則會載入 Azure PowerShell Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="73ea6-185">If you start in this way, the Azure PowerShell cmdlets will be loaded.</span></span>
3. <span data-ttu-id="73ea6-186">在 PowerShell 命令提示字元中，輸入部分命令 `Get-Azure` ，然後按 Tab 鍵來完成陳述式，以確認已載入 PowerShell Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="73ea6-186">At the PowerShell prompt, verify that the PowerShell cmdlets are loaded by entering the partial command `Get-Azure` and then pressing the Tab key for statement completion.</span></span>

   <span data-ttu-id="73ea6-187">如果您重覆按 Tab 鍵，應該會看到各種 Azure PowerShell 命令。</span><span class="sxs-lookup"><span data-stu-id="73ea6-187">If you press the Tab key repeatedly, you should see various Azure PowerShell commands.</span></span>
4. <span data-ttu-id="73ea6-188">從 .publishsettings 檔匯入您的訂閱資訊，以確認可以連線至自己的 Azure 訂閱。</span><span class="sxs-lookup"><span data-stu-id="73ea6-188">Verify that you can connect to your Azure subscription by importing your subscription information from the .publishsettings file.</span></span>

   `Import-AzurePublishSettingsFile c:\scripts\WindowsAzure\default.publishsettings`

   <span data-ttu-id="73ea6-189">然後輸入命令</span><span class="sxs-lookup"><span data-stu-id="73ea6-189">Then enter the command</span></span>

   `Get-AzureSubscription`

   <span data-ttu-id="73ea6-190">如此即會顯示訂用帳戶的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="73ea6-190">This shows information about your subscription.</span></span> <span data-ttu-id="73ea6-191">確認一切正確無誤。</span><span class="sxs-lookup"><span data-stu-id="73ea6-191">Verify that everything is correct.</span></span>
5. <span data-ttu-id="73ea6-192">將本文結尾提供的指令碼範本儲存至您的指令碼資料夾，如 c:\\scripts\\WindowsAzure\\**PublishCloudService.ps1**。</span><span class="sxs-lookup"><span data-stu-id="73ea6-192">Save the script template provided at the end of this article to your scripts folder as c:\\scripts\\WindowsAzure\\**PublishCloudService.ps1**.</span></span>
6. <span data-ttu-id="73ea6-193">檢閱指令碼的參數區段。</span><span class="sxs-lookup"><span data-stu-id="73ea6-193">Review the parameters section of the script.</span></span> <span data-ttu-id="73ea6-194">新增或修改任何預設值。</span><span class="sxs-lookup"><span data-stu-id="73ea6-194">Add or modify any default values.</span></span> <span data-ttu-id="73ea6-195">您永遠可以傳遞明確參數來覆寫這些值。</span><span class="sxs-lookup"><span data-stu-id="73ea6-195">These values can always be overridden by passing in explicit parameters.</span></span>
7. <span data-ttu-id="73ea6-196">確定訂閱中建立了可作為發佈指令碼之目標的有效雲端服務與儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="73ea6-196">Ensure there are valid cloud service and storage accounts created in your subscription that can be targeted by the publish script.</span></span> <span data-ttu-id="73ea6-197">儲存體帳戶 (Blob 儲存) 將用來在建立部署期間上傳並暫時儲存部署套件與組態檔。</span><span class="sxs-lookup"><span data-stu-id="73ea6-197">The storage account (blob storage) will be used to upload and temporarily store the deployment package and config file while the deployment is being created.</span></span>

   * <span data-ttu-id="73ea6-198">若要建立新的雲端服務，您可以呼叫此指令碼或使用 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="73ea6-198">To create a new cloud service, you can call this script or use the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="73ea6-199">雲端服務名稱將作為完整網域名稱中的首碼，因此必須是唯一的。</span><span class="sxs-lookup"><span data-stu-id="73ea6-199">The cloud service name will be used as a prefix in a fully qualified domain name and hence it must be unique.</span></span>

         New-AzureService -ServiceName "mytestcloudservice" -Location "North Central US" -Label "mytestcloudservice"
   * <span data-ttu-id="73ea6-200">若要建立新的儲存體帳戶，您可以呼叫此指令碼或使用 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="73ea6-200">To create a new storage account, you can call this script or use the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="73ea6-201">儲存體帳戶名稱將作為完整網域名稱中的首碼，因此必須是唯一的。</span><span class="sxs-lookup"><span data-stu-id="73ea6-201">The storage account name will be used as a prefix in a fully qualified domain name and hence it must be unique.</span></span> <span data-ttu-id="73ea6-202">您可以嘗試使用與雲端服務相同的名稱。</span><span class="sxs-lookup"><span data-stu-id="73ea6-202">You can try using the same name as the cloud service.</span></span>

         New-AzureStorageAccount -ServiceName "mytestcloudservice" -Location "North Central US" -Label "mytestcloudservice"
8. <span data-ttu-id="73ea6-203">直接從 Azure PowerShell 呼叫指令碼，或將此指令碼接到主機組建自動化程序中，以在建置套件之後執行。</span><span class="sxs-lookup"><span data-stu-id="73ea6-203">Call the script directly from Azure PowerShell, or wire up this script to your host build automation to occur after the package build.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="73ea6-204">依預設，指令碼如果偵測到現有的部署，會一律加以刪除或取代。</span><span class="sxs-lookup"><span data-stu-id="73ea6-204">The script will always delete or replace your existing deployments by default if they are detected.</span></span> <span data-ttu-id="73ea6-205">此為不得不的方式，因為如此一來，完全省去使用者互動過程的自動化程序才有辦法進行連續傳遞。</span><span class="sxs-lookup"><span data-stu-id="73ea6-205">This is necessary to enable continuous delivery from automation where no user prompting is possible.</span></span>
   >
   >

   <span data-ttu-id="73ea6-206">**範例案例 1：** 連續部署至服務的預備環境：</span><span class="sxs-lookup"><span data-stu-id="73ea6-206">**Example scenario 1:** continuous deployment to the staging environment of a service:</span></span>

       PowerShell c:\scripts\windowsazure\PublishCloudService.ps1 -environment Staging -serviceName mycloudservice -storageAccountName mystoragesaccount -packageLocation c:\drops\app.publish\ContactManager.Azure.cspkg -cloudConfigLocation c:\drops\app.publish\ServiceConfiguration.Cloud.cscfg -subscriptionDataFile c:\scripts\default.publishsettings

   <span data-ttu-id="73ea6-207">此作業後面通常接著測試執行驗證及 VIP 交換。</span><span class="sxs-lookup"><span data-stu-id="73ea6-207">This is typically followed up by test run verification and a VIP swap.</span></span> <span data-ttu-id="73ea6-208">VIP 交換可以透過 [Azure 入口網站](https://portal.azure.com)或使用 Move-Deployment Cmdlet 來完成。</span><span class="sxs-lookup"><span data-stu-id="73ea6-208">The VIP swap can be done via the [Azure portal](https://portal.azure.com) or by using the Move-Deployment cmdlet.</span></span>

   <span data-ttu-id="73ea6-209">**範例案例 2：** 連續部署至專用測試服務的生產環境</span><span class="sxs-lookup"><span data-stu-id="73ea6-209">**Example scenario 2:** continuous deployment to the production environment of a dedicated test service</span></span>

       PowerShell c:\scripts\windowsazure\PublishCloudService.ps1 -environment Production -enableDeploymentUpgrade 1 -serviceName mycloudservice -storageAccountName mystorageaccount -packageLocation c:\drops\app.publish\ContactManager.Azure.cspkg -cloudConfigLocation c:\drops\app.publish\ServiceConfiguration.Cloud.cscfg -subscriptionDataFile c:\scripts\default.publishsettings

   <span data-ttu-id="73ea6-210">**遠端桌面：**</span><span class="sxs-lookup"><span data-stu-id="73ea6-210">**Remote Desktop:**</span></span>

   <span data-ttu-id="73ea6-211">如果已在 Azure 專案中啟用遠端桌面，則您需要執行更多一次性步驟，以確定正確的雲端服務會上傳至所有作為此指令碼之目標的雲端服務。</span><span class="sxs-lookup"><span data-stu-id="73ea6-211">If Remote Desktop is enabled in your Azure project you will need to perform additional one-time steps to ensure the correct Cloud Service Certificate is uploaded to all cloud services targeted by this script.</span></span>

   <span data-ttu-id="73ea6-212">尋找您的角色所預期收到的憑證指紋值。</span><span class="sxs-lookup"><span data-stu-id="73ea6-212">Locate the certificate thumbprint values expected by your roles.</span></span> <span data-ttu-id="73ea6-213">指紋值可在雲端組態檔 (也就是 ServiceConfiguration.Cloud.cscfg) 的 Certificates 區段中看到。</span><span class="sxs-lookup"><span data-stu-id="73ea6-213">The thumbprint values are visible in the Certificates section of the cloud config file (i.e. ServiceConfiguration.Cloud.cscfg).</span></span> <span data-ttu-id="73ea6-214">在 Visual Studio 的 [遠端桌面組態] 對話方塊按一下 [顯示選項] 並檢視選取的憑證，也可在看到它。</span><span class="sxs-lookup"><span data-stu-id="73ea6-214">It is also visible in the Remote Desktop Configuration dialog in Visual Studio when you Show Options and view the selected certificate.</span></span>

       <Certificates>
             <Certificate name="Microsoft.WindowsAzure.Plugins.RemoteAccess.PasswordEncryption" thumbprint="C33B6C432C25581601B84C80F86EC2809DC224E8" thumbprintAlgorithm="sha1" />
       </Certificates>

   <span data-ttu-id="73ea6-215">使用下列 Cmdlet 指令碼，上傳遠端桌面憑證作為一次性設定步驟：</span><span class="sxs-lookup"><span data-stu-id="73ea6-215">Upload Remote Desktop certificates as a one-time setup step using the following cmdlet script:</span></span>

       Add-AzureCertificate -serviceName <CLOUDSERVICENAME> -certToDeploy (get-item cert:\CurrentUser\MY\<THUMBPRINT>)

   <span data-ttu-id="73ea6-216">例如：</span><span class="sxs-lookup"><span data-stu-id="73ea6-216">For example:</span></span>

       Add-AzureCertificate -serviceName 'mytestcloudservice' -certToDeploy (get-item cert:\CurrentUser\MY\C33B6C432C25581601B84C80F86EC2809DC224E8

   <span data-ttu-id="73ea6-217">或者，您也可以使用 [Azure 入口網站](https://portal.azure.com)，匯出憑證檔 PFX 與私密金鑰，並將憑證上傳至每個目標雲端服務。</span><span class="sxs-lookup"><span data-stu-id="73ea6-217">Alternatively you can export the certificate file PFX with private key and upload certificates to each target cloud service using the [Azure portal](https://portal.azure.com).</span></span>

   <!---
   Fixing broken links for Azure content migration from ACOM to DOCS. I'm unable to find a replacement links, so I'm commenting out this reference for now. The author can investigate in the future. "Read the following article to learn more: http://msdn.microsoft.com/library/windowsazure/gg443832.aspx.
   -->
   <span data-ttu-id="73ea6-218">**升級部署以及刪除部署 -\> 新增部署**</span><span class="sxs-lookup"><span data-stu-id="73ea6-218">**Upgrade Deployment vs. Delete Deployment -\> New Deployment**</span></span>

   <span data-ttu-id="73ea6-219">當未傳入任何參數，或明確傳遞了值 1 時，指令碼預設會執行升級部署 ($enableDeploymentUpgrade = 1)。</span><span class="sxs-lookup"><span data-stu-id="73ea6-219">The script will by default perform an Upgrade Deployment ($enableDeploymentUpgrade = 1) when no parameter is passed in or the value 1 is passed explicitly.</span></span> <span data-ttu-id="73ea6-220">對於單一執行個體，這具有比完整部署花費更少時間的優點。</span><span class="sxs-lookup"><span data-stu-id="73ea6-220">For single instances this has the advantage of taking less time than a full deployment.</span></span> <span data-ttu-id="73ea6-221">對於需要高可用性的執行個體，這也具有一邊升級部分執行個體，一邊留著部分執行個體繼續執行，以及您的 VIP 不會遭到刪除的優點。</span><span class="sxs-lookup"><span data-stu-id="73ea6-221">For instances that require high availability this also has the advantage of leaving some instances running while others are upgraded (walking your update domain), plus your VIP will not be deleted.</span></span>

   <span data-ttu-id="73ea6-222">若要停用升級部署，可在指令碼中停用 ($enableDeploymentUpgrade = 0) 或傳遞 *-enableDeploymentUpgrade 0* 當作參數，如此會將指令碼行為改變為先刪除任何現有的部署，再建立新的部署。</span><span class="sxs-lookup"><span data-stu-id="73ea6-222">Upgrade Deployment can be disabled in the script ($enableDeploymentUpgrade = 0) or by passing *-enableDeploymentUpgrade 0* as a parameter, which alters the script behavior to first delete any existing deployment and then create a new deployment.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="73ea6-223">依預設，指令碼如果偵測到現有的部署，會一律加以刪除或取代。</span><span class="sxs-lookup"><span data-stu-id="73ea6-223">The script will always delete or replace your existing deployments by default if they are detected.</span></span> <span data-ttu-id="73ea6-224">此為不得不的方式，因為如此一來，完全省去使用者/作業員互動過程的自動化程序才有辦法進行連續傳遞。</span><span class="sxs-lookup"><span data-stu-id="73ea6-224">This is necessary to enable continuous delivery from automation where no user/operator prompting is possible.</span></span>
   >
   >

## <a name="5-publish-a-package-using-tfs-team-build"></a><span data-ttu-id="73ea6-225">5：使用 TFS Team Build 發佈封裝</span><span class="sxs-lookup"><span data-stu-id="73ea6-225">5: Publish a Package using TFS Team Build</span></span>
<span data-ttu-id="73ea6-226">這個選用的步驟會將 TFS Team Build 連接到步驟 4 中建立的指令碼，該指令碼負責處理將套件組建發佈至 Azure。</span><span class="sxs-lookup"><span data-stu-id="73ea6-226">This optional step connects TFS Team Build to the script created in step 4, which handles publishing of the package build to Azure.</span></span> <span data-ttu-id="73ea6-227">這需要修改您的組建定義所使用的流程範本，使其在工作流程結束時執行 Publish 活動。</span><span class="sxs-lookup"><span data-stu-id="73ea6-227">This entails modifying the Process Template used by your build definition so that it runs a Publish activity at the end of the workflow.</span></span> <span data-ttu-id="73ea6-228">Publish 活動會利用組建傳入的參數，執行 PowerShell 命令。</span><span class="sxs-lookup"><span data-stu-id="73ea6-228">The Publish activity will execute your PowerShell command passing in parameters from the build.</span></span> <span data-ttu-id="73ea6-229">所輸出的 MSBuild 目標與發佈指令碼將透過管道傳送至標準組建輸出。</span><span class="sxs-lookup"><span data-stu-id="73ea6-229">Output of the MSBuild targets and publish script will be piped into the standard build output.</span></span>

1. <span data-ttu-id="73ea6-230">編輯負責連續部署的「組建定義」。</span><span class="sxs-lookup"><span data-stu-id="73ea6-230">Edit the Build Definition responsible for continuous deploy.</span></span>
2. <span data-ttu-id="73ea6-231">選取 [處理序]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="73ea6-231">Select the **Process** tab.</span></span>
3. <span data-ttu-id="73ea6-232">遵循 [下列指示](http://msdn.microsoft.com/library/dd647551.aspx) ，為建置流程範本新增活動專案、下載預設範本，將它新增至專案並簽入。</span><span class="sxs-lookup"><span data-stu-id="73ea6-232">Follow [these instructions](http://msdn.microsoft.com/library/dd647551.aspx) to add an Activity project for the build process template, download the default template, add it to the project and check it in.</span></span> <span data-ttu-id="73ea6-233">為建置流程範本提供新名稱，例如 AzureBuildProcessTemplate。</span><span class="sxs-lookup"><span data-stu-id="73ea6-233">Give the build process template a new name, such as AzureBuildProcessTemplate.</span></span>
4. <span data-ttu-id="73ea6-234">回到 [處理序] 索引標籤，並使用 [顯示詳細資料] 以顯示可用建置流程範本的清單。</span><span class="sxs-lookup"><span data-stu-id="73ea6-234">Return to the **Process** tab, and use **Show Details** to show a list of available build process templates.</span></span> <span data-ttu-id="73ea6-235">選擇 [ **新增...** ] 按鈕，然後巡覽至您剛才加入及簽入的專案。</span><span class="sxs-lookup"><span data-stu-id="73ea6-235">Choose the **New...** button, and navigate to the project you just added and checked in.</span></span> <span data-ttu-id="73ea6-236">找出剛才建立的範本並選擇 [ **確定**]。</span><span class="sxs-lookup"><span data-stu-id="73ea6-236">Locate the template you just created and choose **OK**.</span></span>
5. <span data-ttu-id="73ea6-237">開啟選取的流程範本進行編輯。</span><span class="sxs-lookup"><span data-stu-id="73ea6-237">Open the selected Process Template for editing.</span></span> <span data-ttu-id="73ea6-238">您可以在工作流程設計工具或在 XML 編輯器中直接開啟，以使用 XAML。</span><span class="sxs-lookup"><span data-stu-id="73ea6-238">You can open directly in the Workflow designer or in the XML editor to work with the XAML.</span></span>
6. <span data-ttu-id="73ea6-239">在工作流程設計工具的引數索引標籤中，分行新增下列清單中的新引數。</span><span class="sxs-lookup"><span data-stu-id="73ea6-239">Add the following list of new arguments as separate line items in the arguments tab of the workflow designer.</span></span> <span data-ttu-id="73ea6-240">所有引數都應該具有 direction=In 及 type=String。</span><span class="sxs-lookup"><span data-stu-id="73ea6-240">All arguments should have direction=In and type=String.</span></span> <span data-ttu-id="73ea6-241">這些會用來將組建定義中的參數傳到工作流程中，然後用來呼叫發佈指令碼。</span><span class="sxs-lookup"><span data-stu-id="73ea6-241">These will be used to flow parameters from the build definition into the workflow, which then get used to call the publish script.</span></span>

       SubscriptionName
       StorageAccountName
       CloudConfigLocation
       PackageLocation
       Environment
       SubscriptionDataFileLocation
       PublishScriptLocation
       ServiceName

   ![引數清單][3]

   <span data-ttu-id="73ea6-243">對應的 XAML 看起來如下：</span><span class="sxs-lookup"><span data-stu-id="73ea6-243">The corresponding XAML looks like this:</span></span>

       <Activity  _ />
         <x:Members>
           <x:Property Name="BuildSettings" Type="InArgument(mtbwa:BuildSettings)" />
           <x:Property Name="TestSpecs" Type="InArgument(mtbwa:TestSpecList)" />
           <x:Property Name="BuildNumberFormat" Type="InArgument(x:String)" />
           <x:Property Name="CleanWorkspace" Type="InArgument(mtbwa:CleanWorkspaceOption)" />
           <x:Property Name="RunCodeAnalysis" Type="InArgument(mtbwa:CodeAnalysisOption)" />
           <x:Property Name="SourceAndSymbolServerSettings" Type="InArgument(mtbwa:SourceAndSymbolServerSettings)" />
           <x:Property Name="AgentSettings" Type="InArgument(mtbwa:AgentSettings)" />
           <x:Property Name="AssociateChangesetsAndWorkItems" Type="InArgument(x:Boolean)" />
           <x:Property Name="CreateWorkItem" Type="InArgument(x:Boolean)" />
           <x:Property Name="DropBuild" Type="InArgument(x:Boolean)" />
           <x:Property Name="MSBuildArguments" Type="InArgument(x:String)" />
           <x:Property Name="MSBuildPlatform" Type="InArgument(mtbwa:ToolPlatform)" />
           <x:Property Name="PerformTestImpactAnalysis" Type="InArgument(x:Boolean)" />
           <x:Property Name="CreateLabel" Type="InArgument(x:Boolean)" />
           <x:Property Name="DisableTests" Type="InArgument(x:Boolean)" />
           <x:Property Name="GetVersion" Type="InArgument(x:String)" />
           <x:Property Name="PrivateDropLocation" Type="InArgument(x:String)" />
           <x:Property Name="Verbosity" Type="InArgument(mtbw:BuildVerbosity)" />
           <x:Property Name="Metadata" Type="mtbw:ProcessParameterMetadataCollection" />
           <x:Property Name="SupportedReasons" Type="mtbc:BuildReason" />
           <x:Property Name="SubscriptionName" Type="InArgument(x:String)" />
           <x:Property Name="StorageAccountName" Type="InArgument(x:String)" />
           <x:Property Name="CloudConfigLocation" Type="InArgument(x:String)" />
           <x:Property Name="PackageLocation" Type="InArgument(x:String)" />
           <x:Property Name="Environment" Type="InArgument(x:String)" />
           <x:Property Name="SubscriptionDataFileLocation" Type="InArgument(x:String)" />
           <x:Property Name="PublishScriptLocation" Type="InArgument(x:String)" />
           <x:Property Name="ServiceName" Type="InArgument(x:String)" />
         </x:Members>

         <this:Process.MSBuildArguments>
7. <span data-ttu-id="73ea6-244">在 [在代理程式上執行] 結尾新增一個順序：</span><span class="sxs-lookup"><span data-stu-id="73ea6-244">Add a new sequence at the end of Run On Agent:</span></span>

   1. <span data-ttu-id="73ea6-245">先新增 If Statement 活動，以檢查是否有有效指令碼檔案。</span><span class="sxs-lookup"><span data-stu-id="73ea6-245">Start by adding an If Statement activity to check for a valid script file.</span></span> <span data-ttu-id="73ea6-246">將條件設為此值：</span><span class="sxs-lookup"><span data-stu-id="73ea6-246">Set the condition to this value:</span></span>

          Not String.IsNullOrEmpty(PublishScriptLocation)
   2. <span data-ttu-id="73ea6-247">在「If 陳述式」的 Then 案例中，新增 Sequence 活動。</span><span class="sxs-lookup"><span data-stu-id="73ea6-247">In the Then case of the If Statement, add a new Sequence activity.</span></span> <span data-ttu-id="73ea6-248">將顯示名稱設為 'Start publish'</span><span class="sxs-lookup"><span data-stu-id="73ea6-248">Set the display name to 'Start publish'</span></span>
   3. <span data-ttu-id="73ea6-249">在仍選取著 Start publish 順序時，在工作流程設計工具的變數索引標籤中分行新增下列清單中的新變數。</span><span class="sxs-lookup"><span data-stu-id="73ea6-249">With the Start publish sequence still selected, add the following list of new variables as separate line items in the variables tab of the workflow designer.</span></span> <span data-ttu-id="73ea6-250">所有變數都應該具有 Variable type =String 及 Scope=Start publish。</span><span class="sxs-lookup"><span data-stu-id="73ea6-250">All variables should have Variable type =String and Scope=Start publish.</span></span> <span data-ttu-id="73ea6-251">這些會用來將組建定義中的參數傳到工作流程中，然後用來呼叫發佈指令碼。</span><span class="sxs-lookup"><span data-stu-id="73ea6-251">These will be used to flow parameters from the build definition into the workflow, which then get used to call the publish script.</span></span>

      * <span data-ttu-id="73ea6-252">SubscriptionDataFilePath，型別為 String</span><span class="sxs-lookup"><span data-stu-id="73ea6-252">SubscriptionDataFilePath, of type String</span></span>
      * <span data-ttu-id="73ea6-253">PublishScriptFilePath，型別為 String</span><span class="sxs-lookup"><span data-stu-id="73ea6-253">PublishScriptFilePath, of type String</span></span>

        ![新變數][4]
   4. <span data-ttu-id="73ea6-255">如果您使用 TFS 2012 或更早版本，請在新序列的開頭新增 ConvertWorkspaceItem 活動。</span><span class="sxs-lookup"><span data-stu-id="73ea6-255">If you are using TFS 2012 or earlier, add a ConvertWorkspaceItem activity at the beginning of the new Sequence.</span></span> <span data-ttu-id="73ea6-256">如果您使用 TFS 2013 或更新版本，請在新序列的開頭新增 GetLocalPath 活動。</span><span class="sxs-lookup"><span data-stu-id="73ea6-256">If you are using TFS 2013 or later, add a GetLocalPath activity at the beginning of the new sequence.</span></span> <span data-ttu-id="73ea6-257">針對 ConvertWorkspaceItem，請依以下方式設定內容：Direction=ServerToLocal、DisplayName='Convert publish script filename'、Input=' PublishScriptLocation'、Result='PublishScriptFilePath'、Workspace='Workspace'。</span><span class="sxs-lookup"><span data-stu-id="73ea6-257">For a ConvertWorkspaceItem, set the properties as follows: Direction=ServerToLocal, DisplayName='Convert publish script filename', Input=' PublishScriptLocation', Result='PublishScriptFilePath', Workspace='Workspace'.</span></span> <span data-ttu-id="73ea6-258">針對 GetLocalPath 活動，請將內容 IncomingPath 設定為 'PublishScriptLocation'，以及將 Result 設定為 'PublishScriptFilePath'。</span><span class="sxs-lookup"><span data-stu-id="73ea6-258">For a GetLocalPath activity, set the property IncomingPath to 'PublishScriptLocation', and the Result to 'PublishScriptFilePath'.</span></span> <span data-ttu-id="73ea6-259">此活動會將發佈指令碼的路徑從 TFS 伺服器位置 (如果適用的話) 轉換為標準本機磁碟路徑。</span><span class="sxs-lookup"><span data-stu-id="73ea6-259">This activity converts the path to the publish script from TFS server locations (if applicable) to a standard local disk path.</span></span>
   5. <span data-ttu-id="73ea6-260">如果您使用 TFS 2012 或更早版本，請在新序列的結尾新增另一個 ConvertWorkspaceItem 活動。</span><span class="sxs-lookup"><span data-stu-id="73ea6-260">If you are using TFS 2012 or earlier, add another ConvertWorkspaceItem activity at the end of the new Sequence.</span></span> <span data-ttu-id="73ea6-261">Direction=ServerToLocal、DisplayName='Convert subscription filename'、Input=' SubscriptionDataFileLocation'、Result= 'SubscriptionDataFilePath'、Workspace='Workspace'。</span><span class="sxs-lookup"><span data-stu-id="73ea6-261">Direction=ServerToLocal, DisplayName='Convert subscription filename', Input=' SubscriptionDataFileLocation', Result= 'SubscriptionDataFilePath', Workspace='Workspace'.</span></span> <span data-ttu-id="73ea6-262">如果您使用 TFS 2013 或更新版本，請新增另一個 GetLocalPath。</span><span class="sxs-lookup"><span data-stu-id="73ea6-262">If you are using TFS 2013 or later, add another GetLocalPath.</span></span> <span data-ttu-id="73ea6-263">IncomingPath='SubscriptionDataFileLocation'，以及 Result='SubscriptionDataFilePath'。</span><span class="sxs-lookup"><span data-stu-id="73ea6-263">IncomingPath='SubscriptionDataFileLocation', and Result='SubscriptionDataFilePath.'</span></span>
   6. <span data-ttu-id="73ea6-264">在新順序的結尾新增 InvokeProcess 活動。</span><span class="sxs-lookup"><span data-stu-id="73ea6-264">Add an InvokeProcess activity at the end of the new Sequence.</span></span>
      <span data-ttu-id="73ea6-265">此活動會利用組建定義傳入的引數呼叫 PowerShell.exe。</span><span class="sxs-lookup"><span data-stu-id="73ea6-265">This activity calls PowerShell.exe with the arguments passed in by the Build Definition.</span></span>

      + <span data-ttu-id="73ea6-266">Arguments = String.Format(" -File ""{0}"" -serviceName {1}  -storageAccountName {2} -packageLocation ""{3}""  -cloudConfigLocation ""{4}"" -subscriptionDataFile ""{5}""  -selectedSubscription {6} -environment ""{7}""",  PublishScriptFilePath, ServiceName, StorageAccountName,  PackageLocation, CloudConfigLocation,  SubscriptionDataFilePath, SubscriptionName, Environment)</span><span class="sxs-lookup"><span data-stu-id="73ea6-266">Arguments = String.Format(" -File ""{0}"" -serviceName {1}  -storageAccountName {2} -packageLocation ""{3}""  -cloudConfigLocation ""{4}"" -subscriptionDataFile ""{5}""  -selectedSubscription {6} -environment ""{7}""",  PublishScriptFilePath, ServiceName, StorageAccountName,  PackageLocation, CloudConfigLocation,  SubscriptionDataFilePath, SubscriptionName, Environment)</span></span>
      + <span data-ttu-id="73ea6-267">DisplayName = Execute publish script</span><span class="sxs-lookup"><span data-stu-id="73ea6-267">DisplayName = Execute publish script</span></span>
      + <span data-ttu-id="73ea6-268">FileName = "PowerShell" (包括引號)</span><span class="sxs-lookup"><span data-stu-id="73ea6-268">FileName = "PowerShell" (include the quotes)</span></span>
      + <span data-ttu-id="73ea6-269">OutputEncoding=  System.Text.Encoding.GetEncoding(System.Globalization.CultureInfo.InstalledUICulture.TextInfo.OEMCodePage)</span><span class="sxs-lookup"><span data-stu-id="73ea6-269">OutputEncoding=  System.Text.Encoding.GetEncoding(System.Globalization.CultureInfo.InstalledUICulture.TextInfo.OEMCodePage)</span></span>
   7. <span data-ttu-id="73ea6-270">在 InvokeProcess 的 [ **處理標準輸出** ] 區段文字方塊中，將文字方塊值設為 'data'。</span><span class="sxs-lookup"><span data-stu-id="73ea6-270">In the **Handle Standard Output** section textbox of the InvokeProcess, set the textbox value to 'data'.</span></span> <span data-ttu-id="73ea6-271">這是要用來儲存標準輸出資料的變數。</span><span class="sxs-lookup"><span data-stu-id="73ea6-271">This is a variable to store the standard output data.</span></span>
   8. <span data-ttu-id="73ea6-272">緊接在 [ **處理標準輸出** ] 區段下新增 WriteBuildMessage 活動。</span><span class="sxs-lookup"><span data-stu-id="73ea6-272">Add a WriteBuildMessage activity just below the **Handle Standard Output** section.</span></span> <span data-ttu-id="73ea6-273">設定 Importance = 'Microsoft.TeamFoundation.Build.Client.BuildMessageImportance.High'、Message='data'。</span><span class="sxs-lookup"><span data-stu-id="73ea6-273">Set the Importance = 'Microsoft.TeamFoundation.Build.Client.BuildMessageImportance.High' and the Message='data'.</span></span> <span data-ttu-id="73ea6-274">如此可確保指令碼的標準輸出會寫入至組建輸出。</span><span class="sxs-lookup"><span data-stu-id="73ea6-274">This ensures the standard output of the script will get written to the build output.</span></span>
   9. <span data-ttu-id="73ea6-275">在 InvokeProcess 的 [ **處理錯誤輸出** ] 區段文字方塊中，將文字方塊值設為 'data'。</span><span class="sxs-lookup"><span data-stu-id="73ea6-275">In the **Handle Error Output** section textbox of the InvokeProcess, set the textbox value to 'data'.</span></span> <span data-ttu-id="73ea6-276">這是要用來儲存標準錯誤資料的變數。</span><span class="sxs-lookup"><span data-stu-id="73ea6-276">This is a variable to store the standard error data.</span></span>
   10. <span data-ttu-id="73ea6-277">緊接在 [ **處理錯誤輸出** ] 區段下新增 WriteBuildError 活動。</span><span class="sxs-lookup"><span data-stu-id="73ea6-277">Add a WriteBuildError activity just below the **Handle Error Output** section.</span></span> <span data-ttu-id="73ea6-278">設定 Message='data'。</span><span class="sxs-lookup"><span data-stu-id="73ea6-278">Set the Message='data'.</span></span> <span data-ttu-id="73ea6-279">如此可確保指令碼的標準錯誤會寫入至組建錯誤輸出。</span><span class="sxs-lookup"><span data-stu-id="73ea6-279">This ensures the standard errors of the script will get written to the build error output.</span></span>
   11. <span data-ttu-id="73ea6-280">更正由藍色驚嘆號指出的任何錯誤。</span><span class="sxs-lookup"><span data-stu-id="73ea6-280">Correct any errors, indicated by blue exclamation marks.</span></span> <span data-ttu-id="73ea6-281">以滑鼠暫留在驚嘆號上，以取得錯誤的相關提示。</span><span class="sxs-lookup"><span data-stu-id="73ea6-281">Hover over the exclamation marks to get a hint about the error.</span></span> <span data-ttu-id="73ea6-282">儲存工作流程以清除錯誤。</span><span class="sxs-lookup"><span data-stu-id="73ea6-282">Save the workflow to clear errors.</span></span>

   <span data-ttu-id="73ea6-283">在設計工具中，發佈工作流程活動的最終結果將看起來如下：</span><span class="sxs-lookup"><span data-stu-id="73ea6-283">The final result of the publish workflow activities will look like this in the designer:</span></span>

   ![工作流程活動][5]

   <span data-ttu-id="73ea6-285">在 XAML 中，發佈工作流程活動的最終結果將看起來如下：</span><span class="sxs-lookup"><span data-stu-id="73ea6-285">The final result of the publish workflow activities will look like this in XAML:</span></span>

       <If Condition="[Not String.IsNullOrEmpty(PublishScriptLocation)]" sap2010:WorkflowViewState.IdRef="If_1">
           <If.Then>
             <Sequence DisplayName="Start Publish" sap2010:WorkflowViewState.IdRef="Sequence_4">
               <Sequence.Variables>
                 <Variable x:TypeArguments="x:String" Name="SubscriptionDataFilePath" />
                 <Variable x:TypeArguments="x:String" Name="PublishScriptFilePath" />
               </Sequence.Variables>
               <mtbwa:ConvertWorkspaceItem DisplayName="Convert publish script filename" sap2010:WorkflowViewState.IdRef="ConvertWorkspaceItem_1" Input="[PublishScriptLocation]" Result="[PublishScriptFilePath]" Workspace="[Workspace]" />
               <mtbwa:ConvertWorkspaceItem DisplayName="Convert subscription filename" sap2010:WorkflowViewState.IdRef="ConvertWorkspaceItem_2" Input="[SubscriptionDataFileLocation]" Result="[SubscriptionDataFilePath]" Workspace="[Workspace]" />
               <mtbwa:InvokeProcess Arguments="[String.Format(&quot; -File &quot;&quot;{0}&quot;&quot; -serviceName {1}&#xD;&#xA;            -storageAccountName {2} -packageLocation &quot;&quot;{3}&quot;&quot;&#xD;&#xA;            -cloudConfigLocation &quot;&quot;{4}&quot;&quot; -subscriptionDataFile &quot;&quot;{5}&quot;&quot;&#xD;&#xA;            -selectedSubscription {6} -environment &quot;&quot;{7}&quot;&quot;&quot;,&#xD;&#xA;            PublishScriptFilePath, ServiceName, StorageAccountName,&#xD;&#xA;            PackageLocation, CloudConfigLocation,&#xD;&#xA;            SubscriptionDataFilePath, SubscriptionName, Environment)]" DisplayName="'Execute Publish Script'" FileName="[PowerShell]" sap2010:WorkflowViewState.IdRef="InvokeProcess_1">
                 <mtbwa:InvokeProcess.ErrorDataReceived>
                   <ActivityAction x:TypeArguments="x:String">
                     <ActivityAction.Argument>
                       <DelegateInArgument x:TypeArguments="x:String" Name="data" />
                     </ActivityAction.Argument>
                     <mtbwa:WriteBuildError Message="{x:Null}" sap2010:WorkflowViewState.IdRef="WriteBuildError_1" />
                   </ActivityAction>
                 </mtbwa:InvokeProcess.ErrorDataReceived>
                 <mtbwa:InvokeProcess.OutputDataReceived>
                   <ActivityAction x:TypeArguments="x:String">
                     <ActivityAction.Argument>
                       <DelegateInArgument x:TypeArguments="x:String" Name="data" />
                     </ActivityAction.Argument>
                     <mtbwa:WriteBuildMessage sap2010:WorkflowViewState.IdRef="WriteBuildMessage_2" Importance="[Microsoft.TeamFoundation.Build.Client.BuildMessageImportance.High]" Message="[data]" mva:VisualBasic.Settings="Assembly references and imported namespaces serialized as XML namespaces" />
                   </ActivityAction>
                 </mtbwa:InvokeProcess.OutputDataReceived>
               </mtbwa:InvokeProcess>
             </Sequence>
           </If.Then>
         </If>
       </Sequence>
8. <span data-ttu-id="73ea6-286">儲存建置流程範本工作流程，並簽入此檔案。</span><span class="sxs-lookup"><span data-stu-id="73ea6-286">Save the build process template workflow and Check In this file.</span></span>
9. <span data-ttu-id="73ea6-287">編輯組建定義 (如果已開啟請關閉)，如果您在流程範本清單上尚未看到新範本，請選取 [ **新增** ] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="73ea6-287">Edit the build definition (close it if it is already open), and select the **New** button if you do not yet see the new template in the list of Process Templates.</span></span>
10. <span data-ttu-id="73ea6-288">在 Misc 區段中設定如下參數屬性值：</span><span class="sxs-lookup"><span data-stu-id="73ea6-288">Set the parameter property values in the Misc section as follows:</span></span>

    1. <span data-ttu-id="73ea6-289">CloudConfigLocation ='c:\\drops\\app.publish\\ServiceConfiguration.Cloud.cscfg' 此值衍生自：($PublishDir)ServiceConfiguration.Cloud.cscfg</span><span class="sxs-lookup"><span data-stu-id="73ea6-289">CloudConfigLocation ='c:\\drops\\app.publish\\ServiceConfiguration.Cloud.cscfg' *This value is derived from: ($PublishDir)ServiceConfiguration.Cloud.cscfg*</span></span>
    2. <span data-ttu-id="73ea6-290">PackageLocation = 'c:\\drops\\app.publish\\ContactManager.Azure.cspkg' 此值衍生自：($PublishDir)($ProjectName).cspkg</span><span class="sxs-lookup"><span data-stu-id="73ea6-290">PackageLocation = 'c:\\drops\\app.publish\\ContactManager.Azure.cspkg' *This value is derived from: ($PublishDir)($ProjectName).cspkg*</span></span>
    3. <span data-ttu-id="73ea6-291">PublishScriptLocation = 'c:\\scripts\\WindowsAzure\\PublishCloudService.ps1'</span><span class="sxs-lookup"><span data-stu-id="73ea6-291">PublishScriptLocation = 'c:\\scripts\\WindowsAzure\\PublishCloudService.ps1'</span></span>
    4. <span data-ttu-id="73ea6-292">ServiceName = 'mycloudservicename' *在這裡使用適當的雲端服務名稱*</span><span class="sxs-lookup"><span data-stu-id="73ea6-292">ServiceName = 'mycloudservicename' *Use the appropriate cloud service name here*</span></span>
    5. <span data-ttu-id="73ea6-293">Environment = 'Staging'</span><span class="sxs-lookup"><span data-stu-id="73ea6-293">Environment = 'Staging'</span></span>
    6. <span data-ttu-id="73ea6-294">StorageAccountName = 'mystorageaccountname' *在這裡使用適當的儲存體帳戶名稱*</span><span class="sxs-lookup"><span data-stu-id="73ea6-294">StorageAccountName = 'mystorageaccountname' *Use the appropriate storage account name here*</span></span>
    7. <span data-ttu-id="73ea6-295">SubscriptionDataFileLocation = 'c:\\scripts\\WindowsAzure\\Subscription.xml'</span><span class="sxs-lookup"><span data-stu-id="73ea6-295">SubscriptionDataFileLocation = 'c:\\scripts\\WindowsAzure\\Subscription.xml'</span></span>
    8. <span data-ttu-id="73ea6-296">SubscriptionName = 'default'</span><span class="sxs-lookup"><span data-stu-id="73ea6-296">SubscriptionName = 'default'</span></span>

    ![參數屬性值][6]
11. <span data-ttu-id="73ea6-298">儲存組建定義的變更。</span><span class="sxs-lookup"><span data-stu-id="73ea6-298">Save the changes to the Build Definition.</span></span>
12. <span data-ttu-id="73ea6-299">將組建排入佇列，以同時執行套件建置及發佈。</span><span class="sxs-lookup"><span data-stu-id="73ea6-299">Queue a Build to execute both the package build and publish.</span></span> <span data-ttu-id="73ea6-300">如果已將觸發程序設為 Continuous Integration，則每次簽入時都會執行此行為。</span><span class="sxs-lookup"><span data-stu-id="73ea6-300">If you have a trigger set to Continuous Integration, you will execute this behavior on every check-in.</span></span>

### <a name="publishcloudserviceps1-script-template"></a><span data-ttu-id="73ea6-301">PublishCloudService.ps1 指令碼範本</span><span class="sxs-lookup"><span data-stu-id="73ea6-301">PublishCloudService.ps1 script template</span></span>
```
Param(  $serviceName = "",
        $storageAccountName = "",
        $packageLocation = "",
        $cloudConfigLocation = "",
        $environment = "Staging",
        $deploymentLabel = "ContinuousDeploy to $servicename",
        $timeStampFormat = "g",
        $alwaysDeleteExistingDeployments = 1,
        $enableDeploymentUpgrade = 1,
        $selectedsubscription = "default",
        $subscriptionDataFile = ""
     )


function Publish()
{
    $deployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot -ErrorVariable a -ErrorAction silentlycontinue
    if ($a[0] -ne $null)
    {
        Write-Output "$(Get-Date -f $timeStampFormat) - No deployment is detected. Creating a new deployment. "
    }
    #check for existing deployment and then either upgrade, delete + deploy, or cancel according to $alwaysDeleteExistingDeployments and $enableDeploymentUpgrade boolean variables
    if ($deployment.Name -ne $null)
    {
        switch ($alwaysDeleteExistingDeployments)
        {
            1
            {
                switch ($enableDeploymentUpgrade)
                {
                    1  #Update deployment inplace (usually faster, cheaper, won't destroy VIP)
                    {
                        Write-Output "$(Get-Date -f $timeStampFormat) - Deployment exists in $servicename.  Upgrading deployment."
                        UpgradeDeployment
                    }
                    0  #Delete then create new deployment
                    {
                        Write-Output "$(Get-Date -f $timeStampFormat) - Deployment exists in $servicename.  Deleting deployment."
                        DeleteDeployment
                        CreateNewDeployment

                    }
                } # switch ($enableDeploymentUpgrade)
            }
            0
            {
                Write-Output "$(Get-Date -f $timeStampFormat) - ERROR: Deployment exists in $servicename.  Script execution cancelled."
                exit
            }
        } #switch ($alwaysDeleteExistingDeployments)
    } else {
            CreateNewDeployment
    }
}

function CreateNewDeployment()
{
    write-progress -id 3 -activity "Creating New Deployment" -Status "In progress"
    Write-Output "$(Get-Date -f $timeStampFormat) - Creating New Deployment: In progress"

    $opstat = New-AzureDeployment -Slot $slot -Package $packageLocation -Configuration $cloudConfigLocation -label $deploymentLabel -ServiceName $serviceName

    $completeDeployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    $completeDeploymentID = $completeDeployment.deploymentid

    write-progress -id 3 -activity "Creating New Deployment" -completed -Status "Complete"
    Write-Output "$(Get-Date -f $timeStampFormat) - Creating New Deployment: Complete, Deployment ID: $completeDeploymentID"

    StartInstances
}

function UpgradeDeployment()
{
    write-progress -id 3 -activity "Upgrading Deployment" -Status "In progress"
    Write-Output "$(Get-Date -f $timeStampFormat) - Upgrading Deployment: In progress"

    # perform Update-Deployment
    $setdeployment = Set-AzureDeployment -Upgrade -Slot $slot -Package $packageLocation -Configuration $cloudConfigLocation -label $deploymentLabel -ServiceName $serviceName -Force

    $completeDeployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    $completeDeploymentID = $completeDeployment.deploymentid

    write-progress -id 3 -activity "Upgrading Deployment" -completed -Status "Complete"
    Write-Output "$(Get-Date -f $timeStampFormat) - Upgrading Deployment: Complete, Deployment ID: $completeDeploymentID"
}

function DeleteDeployment()
{

    write-progress -id 2 -activity "Deleting Deployment" -Status "In progress"
    Write-Output "$(Get-Date -f $timeStampFormat) - Deleting Deployment: In progress"

    #WARNING - always deletes with force
    $removeDeployment = Remove-AzureDeployment -Slot $slot -ServiceName $serviceName -Force

    write-progress -id 2 -activity "Deleting Deployment: Complete" -completed -Status $removeDeployment
    Write-Output "$(Get-Date -f $timeStampFormat) - Deleting Deployment: Complete"

}

function StartInstances()
{
    write-progress -id 4 -activity "Starting Instances" -status "In progress"
    Write-Output "$(Get-Date -f $timeStampFormat) - Starting Instances: In progress"

    $deployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    $runstatus = $deployment.Status

    if ($runstatus -ne 'Running')
    {
        $run = Set-AzureDeployment -Slot $slot -ServiceName $serviceName -Status Running
    }
    $deployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    $oldStatusStr = @("") * $deployment.RoleInstanceList.Count

    while (-not(AllInstancesRunning($deployment.RoleInstanceList)))
    {
        $i = 1
        foreach ($roleInstance in $deployment.RoleInstanceList)
        {
            $instanceName = $roleInstance.InstanceName
            $instanceStatus = $roleInstance.InstanceStatus

            if ($oldStatusStr[$i - 1] -ne $roleInstance.InstanceStatus)
            {
                $oldStatusStr[$i - 1] = $roleInstance.InstanceStatus
                Write-Output "$(Get-Date -f $timeStampFormat) - Starting Instance '$instanceName': $instanceStatus"
            }

            write-progress -id (4 + $i) -activity "Starting Instance '$instanceName'" -status "$instanceStatus"
            $i = $i + 1
        }

        sleep -Seconds 1

        $deployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    }

    $i = 1
    foreach ($roleInstance in $deployment.RoleInstanceList)
    {
        $instanceName = $roleInstance.InstanceName
        $instanceStatus = $roleInstance.InstanceStatus

        if ($oldStatusStr[$i - 1] -ne $roleInstance.InstanceStatus)
        {
            $oldStatusStr[$i - 1] = $roleInstance.InstanceStatus
            Write-Output "$(Get-Date -f $timeStampFormat) - Starting Instance '$instanceName': $instanceStatus"
        }

        $i = $i + 1
    }

    $deployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    $opstat = $deployment.Status

    write-progress -id 4 -activity "Starting Instances" -completed -status $opstat
    Write-Output "$(Get-Date -f $timeStampFormat) - Starting Instances: $opstat"
}

function AllInstancesRunning($roleInstanceList)
{
    foreach ($roleInstance in $roleInstanceList)
    {
        if ($roleInstance.InstanceStatus -ne "ReadyRole")
        {
            return $false
        }
    }

    return $true
}

#configure powershell with Azure 1.7 modules
Import-Module Azure

#configure powershell with publishsettings for your subscription
$pubsettings = $subscriptionDataFile
Import-AzurePublishSettingsFile $pubsettings
Set-AzureSubscription -CurrentStorageAccountName $storageAccountName -SubscriptionName $selectedsubscription
Select-AzureSubscription $selectedsubscription

#set remaining environment variables for Azure cmdlets
$subscription = Get-AzureSubscription $selectedsubscription
$subscriptionname = $subscription.subscriptionname
$subscriptionid = $subscription.subscriptionid
$slot = $environment

#main driver - publish & write progress to activity log
Write-Output "$(Get-Date -f $timeStampFormat) - Azure Cloud Service deploy script started."
Write-Output "$(Get-Date -f $timeStampFormat) - Preparing deployment of $deploymentLabel for $subscriptionname with Subscription ID $subscriptionid."

Publish

$deployment = Get-AzureDeployment -slot $slot -serviceName $servicename
$deploymentUrl = $deployment.Url

Write-Output "$(Get-Date -f $timeStampFormat) - Created Cloud Service with URL $deploymentUrl."
Write-Output "$(Get-Date -f $timeStampFormat) - Azure Cloud Service deploy script finished."
```

## <a name="next-steps"></a><span data-ttu-id="73ea6-302">後續步驟</span><span class="sxs-lookup"><span data-stu-id="73ea6-302">Next steps</span></span>
<span data-ttu-id="73ea6-303">若要在使用連續傳遞時啟用遠端偵錯，請參閱 [使用連續傳遞來發行至 Azure 時啟用遠端偵錯](cloud-services-virtual-machines-dotnet-continuous-delivery-remote-debugging.md)。</span><span class="sxs-lookup"><span data-stu-id="73ea6-303">To enable remote debugging when using continuous delivery, see [Enable remote debugging when using continuous delivery to publish to Azure](cloud-services-virtual-machines-dotnet-continuous-delivery-remote-debugging.md).</span></span>

[Team Foundation Build Service]: https://msdn.microsoft.com/library/ee259687.aspx
[.NET Framework 4]: https://www.microsoft.com/download/details.aspx?id=17851
[.NET Framework 4.5]: https://www.microsoft.com/download/details.aspx?id=30653
[.NET Framework 4.5.2]: https://www.microsoft.com/download/details.aspx?id=42643
[Scale out your build system]: https://msdn.microsoft.com/library/dd793166.aspx
[Deploy and configure a build server]: https://msdn.microsoft.com/library/ms181712.aspx
[Azure PowerShell cmdlets]: /powershell/azureps-cmdlets-docs
[the .publishsettings file]: https://manage.windowsazure.com/download/publishprofile.aspx?wa=wsignin1.0
[0]: ./media/cloud-services-dotnet-continuous-delivery/tfs-01bc.png
[2]: ./media/cloud-services-dotnet-continuous-delivery/tfs-02.png
[3]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-03.png
[4]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-04.png
[5]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-05.png
[6]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-06.png
