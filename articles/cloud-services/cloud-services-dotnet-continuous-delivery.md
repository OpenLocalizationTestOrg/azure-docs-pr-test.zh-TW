---
title: "aaaContinuous 傳遞的雲端服務在 Azure 中與 TFS |Microsoft 文件"
description: "深入了解如何註冊 azure 持續傳遞 tooset 雲端應用程式。 MSBuild 命令列陳述式和 PowerShell 指令碼的程式碼範例。"
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
ms.openlocfilehash: c0e5e72ffbd3c05b84ce1733068e92c528bcc4b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-delivery-for-cloud-services-in-azure"></a><span data-ttu-id="f6ed7-104">Azure 中雲端服務的連續傳遞</span><span class="sxs-lookup"><span data-stu-id="f6ed7-104">Continuous Delivery for Cloud Services in Azure</span></span>
<span data-ttu-id="f6ed7-105">hello 本文中所述的程序為您示範如何設定 Azure 雲端應用程式的持續傳遞 tooset。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-105">hello process described in this article shows you how tooset up continuous delivery for Azure cloud apps.</span></span> <span data-ttu-id="f6ed7-106">此程序可讓您自動建立封裝和部署 hello 封裝 tooAzure 之後每個程式碼簽入。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-106">This process enables you to automatically create packages and deploy hello package tooAzure after every code check-in.</span></span> <span data-ttu-id="f6ed7-107">hello 本文中所述的封裝建置程序是相當 toohello**封裝**在 Visual Studio 中的命令，並發行步驟是對等 toohello**發行**Visual Studio 中的命令。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-107">hello package build process described in this article is equivalent toohello **Package** command in Visual Studio, and the publishing steps are equivalent toohello **Publish** command in Visual Studio.</span></span>
<span data-ttu-id="f6ed7-108">您會使用 MSBuild 命令列陳述式和 Windows PowerShell 指令碼，而且與 toocreate 組建伺服器也 hello 文章涵蓋 hello 方法示範 toooptionally 如何設定 Visual 的 Studio Team Foundation Server-Team Build 定義toouse hello MSBuild 命令和 PowerShell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-108">hello article covers hello methods you would use toocreate a build server with MSBuild command-line statements and Windows PowerShell scripts, and it also demonstrates how toooptionally configure Visual Studio Team Foundation Server - Team Build definitions toouse hello MSBuild commands and PowerShell scripts.</span></span> <span data-ttu-id="f6ed7-109">hello 程序是可自訂的建置環境和 Azure 的目標環境。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-109">hello process is customizable for your build environment and Azure target environments.</span></span>

<span data-ttu-id="f6ed7-110">您也可以使用 Visual Studio Team Services 的是的 TFS 版本的 Azure 中裝載，toodo 這更容易。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-110">You can also use Visual Studio Team Services, a version of TFS that is hosted in Azure, toodo this more easily.</span></span> 

<span data-ttu-id="f6ed7-111">開始之前，您應該先從 Visual Studio 發佈應用程式。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-111">Before you start, you should publish your application from Visual Studio.</span></span>
<span data-ttu-id="f6ed7-112">這可確保所有 hello 資源，都可供使用且初始化當您嘗試 tooautomate hello 發行集的程序。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-112">This will ensure that all hello resources are available and initialized when you attempt tooautomate hello publication process.</span></span>

## <a name="1-configure-hello-build-server"></a><span data-ttu-id="f6ed7-113">1： 設定組建伺服器 hello</span><span class="sxs-lookup"><span data-stu-id="f6ed7-113">1: Configure hello Build Server</span></span>
<span data-ttu-id="f6ed7-114">您可以使用 MSBuild 建立 Azure 的封裝之前，您必須 hello 組建伺服器上安裝所需的 hello 軟體和工具。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-114">Before you can create an Azure package by using MSBuild, you must install hello required software and tools on hello build server.</span></span>

<span data-ttu-id="f6ed7-115">Visual Studio 不必要的 toobe hello 組建伺服器上安裝。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-115">Visual Studio is not required toobe installed on hello build server.</span></span> <span data-ttu-id="f6ed7-116">如果您想 toouse Team Foundation Build Service toomanage 組建伺服器，請遵循 hello 中的 hello 指示[Team Foundation Build Service] [ Team Foundation Build Service]文件。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-116">If you want toouse Team Foundation Build Service toomanage your build server, follow hello instructions in hello [Team Foundation Build Service][Team Foundation Build Service] documentation.</span></span>

1. <span data-ttu-id="f6ed7-117">Hello 組建伺服器上，安裝 hello [.NET Framework 4.5.2][.NET Framework 4.5.2]，其中包括 MSBuild。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-117">On hello build server, install hello [.NET Framework 4.5.2][.NET Framework 4.5.2], which includes MSBuild.</span></span>
2. <span data-ttu-id="f6ed7-118">安裝最新的 hello[適用於.NET 的 Azure Authoring Tools](https://azure.microsoft.com/develop/net/)。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-118">Install hello latest [Azure Authoring Tools for .NET](https://azure.microsoft.com/develop/net/).</span></span>
3. <span data-ttu-id="f6ed7-119">安裝 hello [Azure Libraries for.NET](http://go.microsoft.com/fwlink/?LinkId=623519)。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-119">Install hello [Azure Libraries for .NET](http://go.microsoft.com/fwlink/?LinkId=623519).</span></span>
4. <span data-ttu-id="f6ed7-120">從 Visual Studio 安裝 toohello 複製 hello Microsoft.WebApplication.targets 檔案部署組建伺服器。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-120">Copy hello Microsoft.WebApplication.targets file from a Visual Studio installation toohello build server.</span></span>

   <span data-ttu-id="f6ed7-121">電腦上安裝 Visual Studio，這個檔案位於 hello 目錄 c:\\Program files （x86)\\MSBuild\\Microsoft\\VisualStudio\\v14.0\\WebApplications。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-121">On a computer with Visual Studio installed, this file is located in hello directory C:\\Program Files(x86)\\MSBuild\\Microsoft\\VisualStudio\\v14.0\\WebApplications.</span></span> <span data-ttu-id="f6ed7-122">您應該將它複製 toohello hello 組建伺服器上相同的目錄。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-122">You should copy it toohello same directory on hello build server.</span></span>
5. <span data-ttu-id="f6ed7-123">安裝 hello [Azure Tools for Visual Studio](https://www.visualstudio.com/features/azure-tools-vs.aspx)。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-123">Install hello [Azure Tools for Visual Studio](https://www.visualstudio.com/features/azure-tools-vs.aspx).</span></span>

## <a name="2-build-a-package-using-msbuild-commands"></a><span data-ttu-id="f6ed7-124">2：使用 MSBuild 命令來建置封裝</span><span class="sxs-lookup"><span data-stu-id="f6ed7-124">2: Build a Package using MSBuild Commands</span></span>
<span data-ttu-id="f6ed7-125">本章節描述如何 tooconstruct MSBuild 命令，建立 Azure 的封裝。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-125">This section describes how tooconstruct an MSBuild command that builds an Azure package.</span></span> <span data-ttu-id="f6ed7-126">上的所有項目已正確設定，而且 hello MSBuild 命令會是您要它 hello 組建伺服器 tooverify toodo 執行此步驟。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-126">Run this step on hello build server tooverify that everything is configured correctly and that hello MSBuild command does what you want it toodo.</span></span> <span data-ttu-id="f6ed7-127">您可以加入這個命令列 tooexisting hello 組建伺服器上，建立指令碼，或者您可以使用 TFS 組建定義中的 hello 命令列 hello 下一節中所述。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-127">You can either add this command line tooexisting build scripts on hello build server, or you can use hello command line in a TFS Build Definition, as described in hello next section.</span></span> <span data-ttu-id="f6ed7-128">如需命令列參數及 MSBuild 的詳細資訊，請參閱 [MSBuild 命令列參考](https://msdn.microsoft.com/library/ms164311%28v=vs.140%29.aspx)。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-128">For more information about command-line parameters and MSBuild, see [MSBuild Command Line Reference](https://msdn.microsoft.com/library/ms164311%28v=vs.140%29.aspx).</span></span>

1. <span data-ttu-id="f6ed7-129">如果在 hello 組建伺服器上安裝 Visual Studio，找出並選擇**Visual Studio 命令提示字元**在 hello **Visual Studio Tools** Windows 中的資料夾。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-129">If Visual Studio is installed on hello build server, locate and choose **Visual Studio Command Prompt** in hello **Visual Studio Tools** folder in Windows.</span></span>

   <span data-ttu-id="f6ed7-130">如果 hello 組建伺服器上未安裝 Visual Studio，開啟命令提示字元，並確認 MSBuild.exe 路徑上，您可以存取。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-130">If Visual Studio is not installed on hello build server, open a command prompt and make sure that MSBuild.exe is accessible on the path.</span></span> <span data-ttu-id="f6ed7-131">MSBuild 會隨 hello.NET Framework 在 hello 路徑 %WINDIR%\\Microsoft.NET\\Framework\\*版本*。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-131">MSBuild is installed with hello .NET Framework in hello path %WINDIR%\\Microsoft.NET\\Framework\\*Version*.</span></span> <span data-ttu-id="f6ed7-132">比方說，若要加入 MSBuild.exe toohello PATH 環境變數，當您安裝.NET Framework 4 時，輸入下列命令在 hello 命令提示字元的 hello:</span><span class="sxs-lookup"><span data-stu-id="f6ed7-132">For example, to add MSBuild.exe toohello PATH environment variable when you have .NET Framework 4 installed, type hello following command at hello command prompt:</span></span>

       set PATH=%PATH%;"C:\Windows\Microsoft.NET\Framework\v4.0.30319"
2. <span data-ttu-id="f6ed7-133">Hello 命令提示字元，瀏覽 toohello 資料夾包含您想 toobuild Azure 專案檔。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-133">At hello command prompt, navigate toohello folder containing the Azure project file that you want toobuild.</span></span>
3. <span data-ttu-id="f6ed7-134">執行 MSBuild 與 hello /target： 發行選項，如 hello 下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="f6ed7-134">Run MSBuild with hello /target:Publish option as in hello following example:</span></span>

       MSBuild /target:Publish

   <span data-ttu-id="f6ed7-135">此選項可以縮寫為 /t:Publish。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-135">This option can be abbreviated as /t:Publish.</span></span> <span data-ttu-id="f6ed7-136">不應將在 MSBuild 中的 hello /t:Publish 選項混淆 hello 發行 Visual Studio 中提供的命令，當您擁有的 hello 安裝 Azure SDK。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-136">hello /t:Publish option in MSBuild should not be confused with hello Publish commands available in Visual Studio when you have hello Azure SDK installed.</span></span> <span data-ttu-id="f6ed7-137">hello /t： 組建 hello Azure 套件只發佈選項。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-137">hello /t:Publish option only builds hello Azure packages.</span></span> <span data-ttu-id="f6ed7-138">它不會部署 hello 封裝 Visual Studio 中的 hello 發行命令一樣。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-138">It does not deploy hello packages as hello Publish commands in Visual Studio do.</span></span>

   <span data-ttu-id="f6ed7-139">（選擇性） 您可以指定 hello 專案名稱做為 MSBuild 參數。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-139">Optionally, you can specify hello project name as an MSBuild parameter.</span></span> <span data-ttu-id="f6ed7-140">如果未指定，會使用 hello 目前的目錄。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-140">If not specified, hello current directory is used.</span></span> <span data-ttu-id="f6ed7-141">如需 MSBuild 命令列選項的詳細資訊，請參閱 [MSBuild 命令列參考](https://msdn.microsoft.com/library/ms164311%28v=vs.140%29.aspx)。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-141">For more information about MSBuild command line options, see [MSBuild Command Line Reference](https://msdn.microsoft.com/library/ms164311%28v=vs.140%29.aspx).</span></span>
4. <span data-ttu-id="f6ed7-142">找出 hello 輸出。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-142">Locate hello output.</span></span> <span data-ttu-id="f6ed7-143">根據預設，此命令會建立一個目錄關聯 toohello 根 hello 專案資料夾，例如*ProjectDir*\\bin\\*組態*\\app.publish\\。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-143">By default, this command creates a directory in relation toohello root folder for hello project, such as *ProjectDir*\\bin\\*Configuration*\\app.publish\\.</span></span> <span data-ttu-id="f6ed7-144">當您建置 Azure 專案時，會產生兩個檔案、 hello 封裝檔本身和伴隨的組態檔的 hello:</span><span class="sxs-lookup"><span data-stu-id="f6ed7-144">When you build an Azure project, you generate two files, hello package file itself and hello accompanying configuration file:</span></span>

   * <span data-ttu-id="f6ed7-145">Project.cspkg</span><span class="sxs-lookup"><span data-stu-id="f6ed7-145">Project.cspkg</span></span>
   * <span data-ttu-id="f6ed7-146">ServiceConfiguration.*TargetProfile*.cscfg</span><span class="sxs-lookup"><span data-stu-id="f6ed7-146">ServiceConfiguration.*TargetProfile*.cscfg</span></span>

   <span data-ttu-id="f6ed7-147">依預設，每個 Azure 專案都會包含一個服務組態檔 (.cscfg 檔) 用於本機 (偵錯) 組建，以及另一個服務組態檔用於 (預備或生產) 雲端組建，但是您可以視需要新增或移除服務組態檔。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-147">By default, each Azure project includes one service configuration file (.cscfg file) for local (debugging) builds and another for cloud (staging or production) builds, but you can add or remove service configuration files as needed.</span></span> <span data-ttu-id="f6ed7-148">當您建置 Visual Studio 中的封裝時，系統會詢問與 hello 封裝一起哪一個服務組態檔 tooinclude。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-148">When you build a package within Visual Studio, you will be asked which service configuration file tooinclude alongside hello package.</span></span>
5. <span data-ttu-id="f6ed7-149">指定 hello 服務組態檔。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-149">Specify hello service configuration file.</span></span> <span data-ttu-id="f6ed7-150">當您使用 MSBuild 建置封裝時，預設會包含 hello 本機服務組態檔。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-150">When you build a package by using MSBuild, hello local service configuration file is included by default.</span></span> <span data-ttu-id="f6ed7-151">tooinclude 不同的服務組態檔，設定如 hello 下列範例所示的 hello MSBuild 命令的 TargetProfile 屬性：</span><span class="sxs-lookup"><span data-stu-id="f6ed7-151">tooinclude a different service configuration file, set the TargetProfile property of hello MSBuild command, as in hello following example:</span></span>

       MSBuild /t:Publish /p:TargetProfile=Cloud
6. <span data-ttu-id="f6ed7-152">指定 hello hello 輸出的位置。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-152">Specify hello location for hello output.</span></span> <span data-ttu-id="f6ed7-153">設定 hello 路徑使用 publishdir =*目錄*\\選項，包括 hello 尾端的反斜線分隔，如 hello 下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="f6ed7-153">Set hello path by using the /p:PublishDir=*Directory*\\ option, including hello trailing backslash separator, as in hello following example:</span></span>

       MSBuild /target:Publish /p:PublishDir=\\myserver\drops\

   <span data-ttu-id="f6ed7-154">一旦您建構並測試適當的 MSBuild 命令列 toobuild 您的專案，並將它們結合於 Azure 的封裝，您可以加入這個命令列 tooyour 建置指令碼。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-154">Once you've constructed and tested an appropriate MSBuild command line toobuild your projects and combine them into an Azure package, you can add this command line tooyour build scripts.</span></span> <span data-ttu-id="f6ed7-155">如果您的組建伺服器使用自訂指令碼，則此程序將視您自訂建置流程的特性而定。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-155">If your build server uses custom scripts, this process will depend on the specifics of your custom build process.</span></span> <span data-ttu-id="f6ed7-156">如果您使用 TFS 做為建置環境，您可以依照 hello hello 下一個步驟 tooadd hello Azure 封裝組建 tooyour 建置流程中的指示。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-156">If you are using TFS as a build environment, then you can follow hello instructions in hello next step tooadd hello Azure package build tooyour build process.</span></span>

## <a name="3-build-a-package-using-tfs-team-build"></a><span data-ttu-id="f6ed7-157">3：使用 TFS Team Build 建置封裝</span><span class="sxs-lookup"><span data-stu-id="f6ed7-157">3: Build a Package using TFS Team Build</span></span>
<span data-ttu-id="f6ed7-158">如果您有 Team Foundation Server (TFS) 設定組建控制器和 hello 組建伺服器設定為 TFS 組建電腦，然後您可以選擇性地設定自動化建置您的 Azure 套件。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-158">If you have Team Foundation Server (TFS) set up as a build controller and hello build server set up as a TFS build machine, then you can optionally set up an automated build for your Azure package.</span></span> <span data-ttu-id="f6ed7-159">如需有關如何向上 tooset 和做為 Team Foundation server 建置系統，請參閱詳細[向外延展您的建置系統][Scale out your build system]。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-159">For information on how tooset up and use Team Foundation server as a build system, see [Scale out your build system][Scale out your build system].</span></span> <span data-ttu-id="f6ed7-160">特別是，下列程序假設您已設定您的組建伺服器中所述[部署和設定組建伺服器][Deploy and configure a build server]，而且您已建立 team 專案時，建立雲端hello team 專案中的服務專案。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-160">In particular, the following procedure assumes that you have configured your build server as described in [Deploy and configure a build server][Deploy and configure a build server], and that you have created a team project, created a cloud service project in hello team project.</span></span>

<span data-ttu-id="f6ed7-161">tooconfigure TFS toobuild Azure 封裝，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="f6ed7-161">tooconfigure TFS toobuild Azure packages, perform hello following steps:</span></span>

1. <span data-ttu-id="f6ed7-162">在 Visual Studio 在開發電腦，hello 檢視 功能表上選擇**Team Explorer**，或選擇 Ctrl +\\，Ctrl + M。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-162">In Visual Studio on your development computer, on hello View menu, choose **Team Explorer**, or choose Ctrl+\\, Ctrl+M.</span></span> <span data-ttu-id="f6ed7-163">在 Team Explorer 視窗中，展開 hello**建置**節點，或選擇 hello**建置**頁面，然後選擇 **新增組建定義**。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-163">In the Team Explorer window, expand hello **Builds** node or choose hello **Builds** page, and choose **New Build Definition**.</span></span>

   ![新增組建定義選項][0]
2. <span data-ttu-id="f6ed7-165">選擇 hello**觸發程序**索引標籤，並指定當您想要的條件 hello 封裝 toobe 建置所需的 hello。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-165">Choose hello **Trigger** tab, and specify hello desired conditions for when you want hello package toobe built.</span></span> <span data-ttu-id="f6ed7-166">例如，指定**連續整合**toobuild hello 封裝簽入原始檔控制時，就會發生。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-166">For example, specify **Continuous Integration** toobuild hello package whenever a source control check-in occurs.</span></span>
3. <span data-ttu-id="f6ed7-167">選擇 hello**來源設定**索引標籤，然後確認您的專案資料夾會列在 hello**原始檔控制資料夾**資料行，且 hello 狀態為**Active**。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-167">Choose hello **Source Settings** tab, and make sure your project folder is listed in hello **Source Control Folder** column, and hello status is **Active**.</span></span>
4. <span data-ttu-id="f6ed7-168">選擇 hello**組建預設值**索引標籤，然後在之下，組建控制器，確認 hello hello 組建伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-168">Choose hello **Build Defaults** tab, and under Build controller, verify hello name of hello build server.</span></span>  <span data-ttu-id="f6ed7-169">而且請選擇 hello 選項**複製組建輸出 toohello 下列置放資料夾**並指定所需的 hello 置放位置。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-169">Also, choose hello option **Copy build output toohello following drop folder** and specify hello desired drop location.</span></span>
5. <span data-ttu-id="f6ed7-170">選擇 hello**程序** 索引標籤。Hello 程序 索引標籤上選擇 hello 預設範本，在**建置**，如果尚未選取，並展開 hello 選擇 hello 專案**進階**> 一節中 hello**建置**hello 方格的區段。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-170">Choose hello **Process** tab. On hello Process tab, choose hello default template, under **Build**, choose hello project if it is not already selected, and expand hello **Advanced** section in hello **Build** section of hello grid.</span></span>
6. <span data-ttu-id="f6ed7-171">選擇**MSBuild 引數**，並依照上述步驟 2 中所述設定 hello 適當 MSBuild 命令列引數。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-171">Choose **MSBuild Arguments**, and set hello appropriate MSBuild command line arguments as described in Step 2 above.</span></span> <span data-ttu-id="f6ed7-172">例如，輸入**/t： 發行 publishdir =\\\\myserver\\卸除\\** toobuild 封裝並複製 hello 封裝檔案 toohello 位置\\ \\myserver\\卸除\\:</span><span class="sxs-lookup"><span data-stu-id="f6ed7-172">For example, enter **/t:Publish /p:PublishDir=\\\\myserver\\drops\\** toobuild a package and copy hello package files toohello location \\\\myserver\\drops\\:</span></span>

   ![MSBuild 引數][2]

   > [!NOTE]
   > <span data-ttu-id="f6ed7-174">複製 hello 檔案 tooa 公用共用可讓您更輕鬆 toomanually 部署 hello 封裝從開發電腦。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-174">Copying hello files tooa public share makes it easier toomanually deploy hello packages from your development computer.</span></span>
7. <span data-ttu-id="f6ed7-175">藉由在變更 tooyour 專案中，檢查測試 hello 成功的建置步驟或佇列新組建。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-175">Test hello success of your build step by checking in a change tooyour project, or queue up a new build.</span></span> <span data-ttu-id="f6ed7-176">tooqueue 新的組建，在 Team Explorer 中，以滑鼠右鍵按一下**所有組建定義，** ，然後選擇 **佇列新組建**。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-176">tooqueue up a new build, in the Team Explorer, right-click **All Build Definitions,** and then choose **Queue New Build**.</span></span>

## <a name="4-publish-a-package-using-a-powershell-script"></a><span data-ttu-id="f6ed7-177">4：使用 PowerShell 指令碼來發佈封裝</span><span class="sxs-lookup"><span data-stu-id="f6ed7-177">4: Publish a Package using a PowerShell Script</span></span>
<span data-ttu-id="f6ed7-178">本章節描述如何 tooconstruct Windows PowerShell 指令碼會將發佈 hello 雲端應用程式封裝輸出 tooAzure 使用選擇性參數。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-178">This section describes how tooconstruct a Windows PowerShell script that will publish hello Cloud app package output tooAzure using optional parameters.</span></span> <span data-ttu-id="f6ed7-179">在自訂建置自動化中的 hello 建置步驟後，可以呼叫此指令碼。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-179">This script can be called after hello build step in your custom build automation.</span></span> <span data-ttu-id="f6ed7-180">也可以從 Visual Studio TFS Team Build 中的「流程範本」工作流程活動中呼叫。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-180">It can also be called from Process Template workflow activities in Visual Studio TFS Team Build.</span></span>

1. <span data-ttu-id="f6ed7-181">安裝 hello [Azure PowerShell cmdlet] [ Azure PowerShell cmdlets] (v0.6.1 或更高版本)。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-181">Install hello [Azure PowerShell cmdlets][Azure PowerShell cmdlets] (v0.6.1 or higher).</span></span>
   <span data-ttu-id="f6ed7-182">在 hello cmdlet 安裝階段中，選擇 tooinstall 嵌入式管理單元。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-182">During hello cmdlet setup phase, choose tooinstall as a snap-in.</span></span> <span data-ttu-id="f6ed7-183">請注意，雖然 hello 舊版已編號 2.x.x 這個正式支援的版本會取代 hello 透過 CodePlex 提供的舊版。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-183">Note that this officially supported version replaces hello older version offered through CodePlex, although hello previous versions were numbered 2.x.x.</span></span>
2. <span data-ttu-id="f6ed7-184">啟動 Azure PowerShell 中使用 hello [開始] 功能表或起始頁。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-184">Start Azure PowerShell using hello Start menu or Start page.</span></span> <span data-ttu-id="f6ed7-185">如果您在這種方式啟動，就會載入 hello Azure PowerShell cmdlet。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-185">If you start in this way, hello Azure PowerShell cmdlets will be loaded.</span></span>
3. <span data-ttu-id="f6ed7-186">Hello PowerShell 命令提示字元中，確認 hello PowerShell 指令程式會載入輸入 hello 部分命令`Get-Azure`，然後按 hello Tab 鍵，以完成陳述式。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-186">At hello PowerShell prompt, verify that hello PowerShell cmdlets are loaded by entering hello partial command `Get-Azure` and then pressing hello Tab key for statement completion.</span></span>

   <span data-ttu-id="f6ed7-187">如果您重複按 hello Tab 鍵，您應該會看到不同的 Azure PowerShell 命令。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-187">If you press hello Tab key repeatedly, you should see various Azure PowerShell commands.</span></span>
4. <span data-ttu-id="f6ed7-188">請確認您可以從 hello.publishsettings 檔案匯入您的訂用帳戶資訊來連接 tooyour Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-188">Verify that you can connect tooyour Azure subscription by importing your subscription information from hello .publishsettings file.</span></span>

   `Import-AzurePublishSettingsFile c:\scripts\WindowsAzure\default.publishsettings`

   <span data-ttu-id="f6ed7-189">然後輸入 hello 命令</span><span class="sxs-lookup"><span data-stu-id="f6ed7-189">Then enter hello command</span></span>

   `Get-AzureSubscription`

   <span data-ttu-id="f6ed7-190">如此即會顯示訂用帳戶的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-190">This shows information about your subscription.</span></span> <span data-ttu-id="f6ed7-191">確認一切正確無誤。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-191">Verify that everything is correct.</span></span>
5. <span data-ttu-id="f6ed7-192">儲存在 hello 到您指令碼的資料夾為 c： 本文結尾處提供的 hello 指令碼範本\\指令碼\\WindowsAzure\\**PublishCloudService.ps1**。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-192">Save hello script template provided at hello end of this article to your scripts folder as c:\\scripts\\WindowsAzure\\**PublishCloudService.ps1**.</span></span>
6. <span data-ttu-id="f6ed7-193">檢閱 hello hello 指令碼參數區段。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-193">Review hello parameters section of hello script.</span></span> <span data-ttu-id="f6ed7-194">新增或修改任何預設值。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-194">Add or modify any default values.</span></span> <span data-ttu-id="f6ed7-195">您永遠可以傳遞明確參數來覆寫這些值。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-195">These values can always be overridden by passing in explicit parameters.</span></span>
7. <span data-ttu-id="f6ed7-196">請確定沒有有效的雲端服務，而且您可以將目標設 hello 的訂閱中建立的儲存體帳戶的發行指令碼。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-196">Ensure there are valid cloud service and storage accounts created in your subscription that can be targeted by hello publish script.</span></span> <span data-ttu-id="f6ed7-197">儲存體帳戶 （blob 儲存） 會使用的 tooupload 並在建立部署時，暫時儲存 hello 部署封裝和組態檔。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-197">The storage account (blob storage) will be used tooupload and temporarily store hello deployment package and config file while the deployment is being created.</span></span>

   * <span data-ttu-id="f6ed7-198">toocreate 新的雲端服務，您可以呼叫此指令碼或使用 hello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-198">toocreate a new cloud service, you can call this script or use hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="f6ed7-199">hello 雲端服務名稱會用作中完整的網域名稱的前置詞，因此它必須是唯一的。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-199">hello cloud service name will be used as a prefix in a fully qualified domain name and hence it must be unique.</span></span>

         New-AzureService -ServiceName "mytestcloudservice" -Location "North Central US" -Label "mytestcloudservice"
   * <span data-ttu-id="f6ed7-200">toocreate 新的儲存體帳戶，您可以呼叫此指令碼或使用 hello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-200">toocreate a new storage account, you can call this script or use hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="f6ed7-201">hello 儲存體帳戶名稱會用作中完整的網域名稱的前置詞，因此它必須是唯一的。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-201">hello storage account name will be used as a prefix in a fully qualified domain name and hence it must be unique.</span></span> <span data-ttu-id="f6ed7-202">您可以嘗試使用名稱相同的 hello 與雲端服務。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-202">You can try using hello same name as the cloud service.</span></span>

         New-AzureStorageAccount -ServiceName "mytestcloudservice" -Location "North Central US" -Label "mytestcloudservice"
8. <span data-ttu-id="f6ed7-203">直接從 Azure PowerShell，呼叫 hello 指令碼，或連接此指令碼 tooyour 主機組建自動化 toooccur 之後 hello 封裝組建。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-203">Call hello script directly from Azure PowerShell, or wire up this script tooyour host build automation toooccur after hello package build.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="f6ed7-204">hello 指令碼將會永遠刪除，或您現有的部署取代依預設，如果偵測到。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-204">hello script will always delete or replace your existing deployments by default if they are detected.</span></span> <span data-ttu-id="f6ed7-205">此為不得不的方式，因為如此一來，完全省去使用者互動過程的自動化程序才有辦法進行連續傳遞。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-205">This is necessary to enable continuous delivery from automation where no user prompting is possible.</span></span>
   >
   >

   <span data-ttu-id="f6ed7-206">**範例案例 1:**連續部署 toohello 預備環境的服務：</span><span class="sxs-lookup"><span data-stu-id="f6ed7-206">**Example scenario 1:** continuous deployment toohello staging environment of a service:</span></span>

       PowerShell c:\scripts\windowsazure\PublishCloudService.ps1 -environment Staging -serviceName mycloudservice -storageAccountName mystoragesaccount -packageLocation c:\drops\app.publish\ContactManager.Azure.cspkg -cloudConfigLocation c:\drops\app.publish\ServiceConfiguration.Cloud.cscfg -subscriptionDataFile c:\scripts\default.publishsettings

   <span data-ttu-id="f6ed7-207">此作業後面通常接著測試執行驗證及 VIP 交換。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-207">This is typically followed up by test run verification and a VIP swap.</span></span> <span data-ttu-id="f6ed7-208">hello VIP 交換可透過 hello [Azure 入口網站](https://portal.azure.com)或使用 hello 移動部署 cmdlet。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-208">hello VIP swap can be done via hello [Azure portal](https://portal.azure.com) or by using hello Move-Deployment cmdlet.</span></span>

   <span data-ttu-id="f6ed7-209">**範例案例 2:**連續部署 toohello 實際執行環境的專用的測試服務</span><span class="sxs-lookup"><span data-stu-id="f6ed7-209">**Example scenario 2:** continuous deployment toohello production environment of a dedicated test service</span></span>

       PowerShell c:\scripts\windowsazure\PublishCloudService.ps1 -environment Production -enableDeploymentUpgrade 1 -serviceName mycloudservice -storageAccountName mystorageaccount -packageLocation c:\drops\app.publish\ContactManager.Azure.cspkg -cloudConfigLocation c:\drops\app.publish\ServiceConfiguration.Cloud.cscfg -subscriptionDataFile c:\scripts\default.publishsettings

   <span data-ttu-id="f6ed7-210">**遠端桌面：**</span><span class="sxs-lookup"><span data-stu-id="f6ed7-210">**Remote Desktop:**</span></span>

   <span data-ttu-id="f6ed7-211">遠端桌面已啟用 Azure 專案中，如果您需要 tooperform 額外的單次步驟 tooensure hello 是正確的雲端服務憑證上傳 tooall 雲端服務，此指令碼的目標。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-211">If Remote Desktop is enabled in your Azure project you will need tooperform additional one-time steps tooensure hello correct Cloud Service Certificate is uploaded tooall cloud services targeted by this script.</span></span>

   <span data-ttu-id="f6ed7-212">找出您的角色所預期的 hello 憑證指紋值。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-212">Locate hello certificate thumbprint values expected by your roles.</span></span> <span data-ttu-id="f6ed7-213">憑證指紋值 hello 的雲端組態檔 (也就是 ServiceConfiguration.Cloud.cscfg) 的憑證 > 一節中會出現的。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-213">The thumbprint values are visible in hello Certificates section of the cloud config file (i.e. ServiceConfiguration.Cloud.cscfg).</span></span> <span data-ttu-id="f6ed7-214">您的顯示選項和檢視 hello 選取憑證時，它會也在 Visual Studio 中的 hello 遠端桌面設定對話方塊中顯示。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-214">It is also visible in hello Remote Desktop Configuration dialog in Visual Studio when you Show Options and view hello selected certificate.</span></span>

       <Certificates>
             <Certificate name="Microsoft.WindowsAzure.Plugins.RemoteAccess.PasswordEncryption" thumbprint="C33B6C432C25581601B84C80F86EC2809DC224E8" thumbprintAlgorithm="sha1" />
       </Certificates>

   <span data-ttu-id="f6ed7-215">遠端桌面憑證上傳一次設定步驟，使用下列 cmdlet 指令碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="f6ed7-215">Upload Remote Desktop certificates as a one-time setup step using hello following cmdlet script:</span></span>

       Add-AzureCertificate -serviceName <CLOUDSERVICENAME> -certToDeploy (get-item cert:\CurrentUser\MY\<THUMBPRINT>)

   <span data-ttu-id="f6ed7-216">例如：</span><span class="sxs-lookup"><span data-stu-id="f6ed7-216">For example:</span></span>

       Add-AzureCertificate -serviceName 'mytestcloudservice' -certToDeploy (get-item cert:\CurrentUser\MY\C33B6C432C25581601B84C80F86EC2809DC224E8

   <span data-ttu-id="f6ed7-217">或者，您可以匯出使用私用金鑰和上傳憑證 tooeach 目標雲端服務的 hello 憑證檔案 PFX [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-217">Alternatively you can export hello certificate file PFX with private key and upload certificates tooeach target cloud service using the [Azure portal](https://portal.azure.com).</span></span>

   <!---
   Fixing broken links for Azure content migration from ACOM tooDOCS. I'm unable toofind a replacement links, so I'm commenting out this reference for now. hello author can investigate in hello future. "Read hello following article toolearn more: http://msdn.microsoft.com/library/windowsazure/gg443832.aspx.
   -->
   <span data-ttu-id="f6ed7-218">**升級部署以及刪除部署 -\> 新增部署**</span><span class="sxs-lookup"><span data-stu-id="f6ed7-218">**Upgrade Deployment vs. Delete Deployment -\> New Deployment**</span></span>

   <span data-ttu-id="f6ed7-219">hello 指令碼會根據預設執行升級的部署 ($enableDeploymentUpgrade = 1) 在沒有參數傳遞或明確傳遞的值為 1 時。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-219">hello script will by default perform an Upgrade Deployment ($enableDeploymentUpgrade = 1) when no parameter is passed in or the value 1 is passed explicitly.</span></span> <span data-ttu-id="f6ed7-220">對於單一執行個體，這具有比完整部署花費更少時間的優點。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-220">For single instances this has the advantage of taking less time than a full deployment.</span></span> <span data-ttu-id="f6ed7-221">針對需要高可用性，這也有某些情況下執行，而其他則可能會留下 hello 優點的執行個體升級 （查核更新網域），加上將不會刪除您的 VIP。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-221">For instances that require high availability this also has hello advantage of leaving some instances running while others are upgraded (walking your update domain), plus your VIP will not be deleted.</span></span>

   <span data-ttu-id="f6ed7-222">升級部署，您可以在 hello 指令碼中停用 ($enableDeploymentUpgrade = 0) 或藉由傳遞*-enableDeploymentUpgrade 0*做為參數，其中改變指令碼行為 toofirst 刪除任何現有的部署，然後建立新的部署。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-222">Upgrade Deployment can be disabled in hello script ($enableDeploymentUpgrade = 0) or by passing *-enableDeploymentUpgrade 0* as a parameter, which alters the script behavior toofirst delete any existing deployment and then create a new deployment.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="f6ed7-223">hello 指令碼將會永遠刪除，或您現有的部署取代依預設，如果偵測到。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-223">hello script will always delete or replace your existing deployments by default if they are detected.</span></span> <span data-ttu-id="f6ed7-224">此為不得不的方式，因為如此一來，完全省去使用者/作業員互動過程的自動化程序才有辦法進行連續傳遞。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-224">This is necessary to enable continuous delivery from automation where no user/operator prompting is possible.</span></span>
   >
   >

## <a name="5-publish-a-package-using-tfs-team-build"></a><span data-ttu-id="f6ed7-225">5：使用 TFS Team Build 發佈封裝</span><span class="sxs-lookup"><span data-stu-id="f6ed7-225">5: Publish a Package using TFS Team Build</span></span>
<span data-ttu-id="f6ed7-226">此選擇性步驟中連接的 TFS Team Build toohello 指令碼在步驟 4 中，建立用來處理 hello 封裝組建 tooAzure 發行。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-226">This optional step connects TFS Team Build toohello script created in step 4, which handles publishing of hello package build tooAzure.</span></span> <span data-ttu-id="f6ed7-227">這需要修改 hello 供您的組建定義，使其執行的發佈活動結尾 hello hello 工作流程的流程範本。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-227">This entails modifying hello Process Template used by your build definition so that it runs a Publish activity at hello end of hello workflow.</span></span> <span data-ttu-id="f6ed7-228">hello 發行活動會執行您從 hello 組建傳入參數的 PowerShell 命令。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-228">hello Publish activity will execute your PowerShell command passing in parameters from hello build.</span></span> <span data-ttu-id="f6ed7-229">Hello MSBuild 目標和發行指令碼的輸出會經由管道輸出到 hello 標準的建置輸出。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-229">Output of hello MSBuild targets and publish script will be piped into hello standard build output.</span></span>

1. <span data-ttu-id="f6ed7-230">編輯組建定義負責 hello 連續部署。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-230">Edit hello Build Definition responsible for continuous deploy.</span></span>
2. <span data-ttu-id="f6ed7-231">選取 hello**程序** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-231">Select hello **Process** tab.</span></span>
3. <span data-ttu-id="f6ed7-232">請遵循[這些指示](http://msdn.microsoft.com/library/dd647551.aspx)tooadd hello 活動專案建置流程範本，請下載 hello 預設範本，將它加入 hello 專案並將它簽入。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-232">Follow [these instructions](http://msdn.microsoft.com/library/dd647551.aspx) tooadd an Activity project for hello build process template, download hello default template, add it to hello project and check it in.</span></span> <span data-ttu-id="f6ed7-233">請提供新的名稱，例如 AzureBuildProcessTemplate hello 建置流程範本。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-233">Give hello build process template a new name, such as AzureBuildProcessTemplate.</span></span>
4. <span data-ttu-id="f6ed7-234">傳回 toohello**程序**索引標籤，然後使用**顯示詳細資料**tooshow 可用的建置流程範本的清單。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-234">Return toohello **Process** tab, and use **Show Details** tooshow a list of available build process templates.</span></span> <span data-ttu-id="f6ed7-235">選擇 hello**新增...**按鈕，然後瀏覽 toohello 專案只需要加入，並簽入。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-235">Choose hello **New...** button, and navigate toohello project you just added and checked in.</span></span> <span data-ttu-id="f6ed7-236">找出您剛才建立的 hello 範本，然後選擇 **確定**。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-236">Locate hello template you just created and choose **OK**.</span></span>
5. <span data-ttu-id="f6ed7-237">開啟 hello 選取流程範本進行編輯。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-237">Open hello selected Process Template for editing.</span></span> <span data-ttu-id="f6ed7-238">您可以開啟直接在 hello 工作流程設計工具或 hello XML 編輯器 toowork 以 hello XAML 中。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-238">You can open directly in hello Workflow designer or in hello XML editor toowork with hello XAML.</span></span>
6. <span data-ttu-id="f6ed7-239">新增新引數清單後面 hello 的 hello 工作流程設計工具的引數 索引標籤中的個別明細項目為 hello。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-239">Add hello following list of new arguments as separate line items in hello arguments tab of hello workflow designer.</span></span> <span data-ttu-id="f6ed7-240">所有引數都應該具有 direction=In 及 type=String。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-240">All arguments should have direction=In and type=String.</span></span> <span data-ttu-id="f6ed7-241">這些會是使用的 tooflow hello 到 hello 流程中，哪些然後 get 使用的 toocall hello 發行指令碼的組建定義的參數。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-241">These will be used tooflow parameters from hello build definition into hello workflow, which then get used toocall hello publish script.</span></span>

       SubscriptionName
       StorageAccountName
       CloudConfigLocation
       PackageLocation
       Environment
       SubscriptionDataFileLocation
       PublishScriptLocation
       ServiceName

   ![引數清單][3]

   <span data-ttu-id="f6ed7-243">hello 對應 XAML 看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="f6ed7-243">hello corresponding XAML looks like this:</span></span>

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
7. <span data-ttu-id="f6ed7-244">在代理程式上執行的 hello 結尾處加入新的順序：</span><span class="sxs-lookup"><span data-stu-id="f6ed7-244">Add a new sequence at hello end of Run On Agent:</span></span>

   1. <span data-ttu-id="f6ed7-245">將有效的指令碼檔案的 If 陳述式活動 toocheck 來開始。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-245">Start by adding an If Statement activity toocheck for a valid script file.</span></span> <span data-ttu-id="f6ed7-246">設定 hello 條件 toothis 值：</span><span class="sxs-lookup"><span data-stu-id="f6ed7-246">Set hello condition toothis value:</span></span>

          Not String.IsNullOrEmpty(PublishScriptLocation)
   2. <span data-ttu-id="f6ed7-247">然後在 hello hello If 陳述式的情況下加入新的序列活動。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-247">In hello Then case of hello If Statement, add a new Sequence activity.</span></span> <span data-ttu-id="f6ed7-248">發行集 hello 顯示名稱 too'Start'</span><span class="sxs-lookup"><span data-stu-id="f6ed7-248">Set hello display name too'Start publish'</span></span>
   3. <span data-ttu-id="f6ed7-249">Hello 開始發行仍選取的順序，加入下列新的變數清單為 hello 工作流程設計工具中的 [變數] 索引標籤中的個別明細項目。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-249">With hello Start publish sequence still selected, add the following list of new variables as separate line items in the variables tab of hello workflow designer.</span></span> <span data-ttu-id="f6ed7-250">所有變數都應該具有 Variable type =String 及 Scope=Start publish。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-250">All variables should have Variable type =String and Scope=Start publish.</span></span> <span data-ttu-id="f6ed7-251">這些會是使用的 tooflow hello 到哪些然後 get 使用的 toocall hello 發行指令碼的工作流程的組建定義的參數。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-251">These will be used tooflow parameters from hello build definition into the workflow, which then get used toocall hello publish script.</span></span>

      * <span data-ttu-id="f6ed7-252">SubscriptionDataFilePath，型別為 String</span><span class="sxs-lookup"><span data-stu-id="f6ed7-252">SubscriptionDataFilePath, of type String</span></span>
      * <span data-ttu-id="f6ed7-253">PublishScriptFilePath，型別為 String</span><span class="sxs-lookup"><span data-stu-id="f6ed7-253">PublishScriptFilePath, of type String</span></span>

        ![新變數][4]
   4. <span data-ttu-id="f6ed7-255">如果您使用 TFS 2012 或更早版本，在 hello 開頭加入 ConvertWorkspaceItem 活動 hello 新的順序。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-255">If you are using TFS 2012 or earlier, add a ConvertWorkspaceItem activity at hello beginning of hello new Sequence.</span></span> <span data-ttu-id="f6ed7-256">如果您使用 TFS 2013 或更新版本，新增 GetLocalPath 活動 hello hello 新序列開頭。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-256">If you are using TFS 2013 or later, add a GetLocalPath activity at hello beginning of hello new sequence.</span></span> <span data-ttu-id="f6ed7-257">對於 ConvertWorkspaceItem，設定 hello 屬性，如下所示： 方向 = ServerToLocal，DisplayName = 'Convert 發佈指令碼檔案名稱 輸入 = 'PublishScriptLocation'，結果 = 'PublishScriptFilePath'，工作空間 = '工作區'。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-257">For a ConvertWorkspaceItem, set hello properties as follows: Direction=ServerToLocal, DisplayName='Convert publish script filename', Input=' PublishScriptLocation', Result='PublishScriptFilePath', Workspace='Workspace'.</span></span> <span data-ttu-id="f6ed7-258">是 GetLocalPath 活動，請設定 hello 屬性 IncomingPath too'PublishScriptLocation'，與 hello 結果 too'PublishScriptFilePath'。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-258">For a GetLocalPath activity, set hello property IncomingPath too'PublishScriptLocation', and hello Result too'PublishScriptFilePath'.</span></span> <span data-ttu-id="f6ed7-259">（如果適用），此活動將 hello 路徑 toohello 發行指令碼，從 TFS 伺服器位置 tooa 標準的本機磁碟的路徑。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-259">This activity converts hello path toohello publish script from TFS server locations (if applicable) tooa standard local disk path.</span></span>
   5. <span data-ttu-id="f6ed7-260">如果您使用 TFS 2012 或更早版本，新增另一個 ConvertWorkspaceItem 活動結尾的 hello hello 新的順序。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-260">If you are using TFS 2012 or earlier, add another ConvertWorkspaceItem activity at hello end of hello new Sequence.</span></span> <span data-ttu-id="f6ed7-261">Direction=ServerToLocal、DisplayName='Convert subscription filename'、Input=' SubscriptionDataFileLocation'、Result= 'SubscriptionDataFilePath'、Workspace='Workspace'。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-261">Direction=ServerToLocal, DisplayName='Convert subscription filename', Input=' SubscriptionDataFileLocation', Result= 'SubscriptionDataFilePath', Workspace='Workspace'.</span></span> <span data-ttu-id="f6ed7-262">如果您使用 TFS 2013 或更新版本，請新增另一個 GetLocalPath。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-262">If you are using TFS 2013 or later, add another GetLocalPath.</span></span> <span data-ttu-id="f6ed7-263">IncomingPath='SubscriptionDataFileLocation'，以及 Result='SubscriptionDataFilePath'。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-263">IncomingPath='SubscriptionDataFileLocation', and Result='SubscriptionDataFilePath.'</span></span>
   6. <span data-ttu-id="f6ed7-264">加入 InvokeProcess 活動結尾 hello hello 新的順序。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-264">Add an InvokeProcess activity at hello end of hello new Sequence.</span></span>
      <span data-ttu-id="f6ed7-265">此活動 PowerShell.exe 具 hello 引數呼叫傳入 hello 組建定義。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-265">This activity calls PowerShell.exe with hello arguments passed in by hello Build Definition.</span></span>

      + <span data-ttu-id="f6ed7-266">Arguments = String.Format(" -File ""{0}"" -serviceName {1}  -storageAccountName {2} -packageLocation ""{3}""  -cloudConfigLocation ""{4}"" -subscriptionDataFile ""{5}""  -selectedSubscription {6} -environment ""{7}""",  PublishScriptFilePath, ServiceName, StorageAccountName,  PackageLocation, CloudConfigLocation,  SubscriptionDataFilePath, SubscriptionName, Environment)</span><span class="sxs-lookup"><span data-stu-id="f6ed7-266">Arguments = String.Format(" -File ""{0}"" -serviceName {1}  -storageAccountName {2} -packageLocation ""{3}""  -cloudConfigLocation ""{4}"" -subscriptionDataFile ""{5}""  -selectedSubscription {6} -environment ""{7}""",  PublishScriptFilePath, ServiceName, StorageAccountName,  PackageLocation, CloudConfigLocation,  SubscriptionDataFilePath, SubscriptionName, Environment)</span></span>
      + <span data-ttu-id="f6ed7-267">DisplayName = Execute publish script</span><span class="sxs-lookup"><span data-stu-id="f6ed7-267">DisplayName = Execute publish script</span></span>
      + <span data-ttu-id="f6ed7-268">檔案名稱 ="PowerShell"（包括 hello 引號）</span><span class="sxs-lookup"><span data-stu-id="f6ed7-268">FileName = "PowerShell" (include hello quotes)</span></span>
      + <span data-ttu-id="f6ed7-269">OutputEncoding=  System.Text.Encoding.GetEncoding(System.Globalization.CultureInfo.InstalledUICulture.TextInfo.OEMCodePage)</span><span class="sxs-lookup"><span data-stu-id="f6ed7-269">OutputEncoding=  System.Text.Encoding.GetEncoding(System.Globalization.CultureInfo.InstalledUICulture.TextInfo.OEMCodePage)</span></span>
   7. <span data-ttu-id="f6ed7-270">在 hello**處理標準輸出**區段 InvokeProcess 的文字方塊中，將 hello textbox 值 too'data'。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-270">In hello **Handle Standard Output** section textbox of the InvokeProcess, set hello textbox value too'data'.</span></span> <span data-ttu-id="f6ed7-271">這是變數 toostore hello 標準輸出資料。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-271">This is a variable toostore hello standard output data.</span></span>
   8. <span data-ttu-id="f6ed7-272">新增正下方 hello WriteBuildMessage 活動**處理標準輸出**> 一節。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-272">Add a WriteBuildMessage activity just below hello **Handle Standard Output** section.</span></span> <span data-ttu-id="f6ed7-273">設定 hello 重要性 = 'Microsoft.TeamFoundation.Build.Client.BuildMessageImportance.High' 和 hello 訊息 = 'data'。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-273">Set hello Importance = 'Microsoft.TeamFoundation.Build.Client.BuildMessageImportance.High' and hello Message='data'.</span></span> <span data-ttu-id="f6ed7-274">這可確保指令碼的 hello 標準輸出會寫入 toohello 組建輸出。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-274">This ensures hello standard output of the script will get written toohello build output.</span></span>
   9. <span data-ttu-id="f6ed7-275">在 hello**處理錯誤輸出**區段 InvokeProcess 的文字方塊中，將 hello textbox 值 too'data'。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-275">In hello **Handle Error Output** section textbox of the InvokeProcess, set hello textbox value too'data'.</span></span> <span data-ttu-id="f6ed7-276">這是變數 toostore hello 標準錯誤資料。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-276">This is a variable toostore hello standard error data.</span></span>
   10. <span data-ttu-id="f6ed7-277">新增正下方 hello WriteBuildError 活動**處理錯誤輸出**> 一節。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-277">Add a WriteBuildError activity just below hello **Handle Error Output** section.</span></span> <span data-ttu-id="f6ed7-278">設定 hello 訊息 = 'data'。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-278">Set hello Message='data'.</span></span> <span data-ttu-id="f6ed7-279">這可確保 hello 指令碼的 hello 標準錯誤會寫入 toohello 建置錯誤輸出。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-279">This ensures hello standard errors of hello script will get written toohello build error output.</span></span>
   11. <span data-ttu-id="f6ed7-280">更正由藍色驚嘆號指出的任何錯誤。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-280">Correct any errors, indicated by blue exclamation marks.</span></span> <span data-ttu-id="f6ed7-281">將滑鼠停留在驚歎 tooget hello 錯誤有關的提示。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-281">Hover over the exclamation marks tooget a hint about hello error.</span></span> <span data-ttu-id="f6ed7-282">儲存要清除錯誤 hello 工作流程。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-282">Save hello workflow to clear errors.</span></span>

   <span data-ttu-id="f6ed7-283">hello hello 最終結果會發行工作流程活動 hello 設計工具中，看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="f6ed7-283">hello final result of hello publish workflow activities will look like this in hello designer:</span></span>

   ![工作流程活動][5]

   <span data-ttu-id="f6ed7-285">hello 最終結果的 hello 發行工作流程活動 XAML 中，看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="f6ed7-285">hello final result of hello publish workflow activities will look like this in XAML:</span></span>

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
8. <span data-ttu-id="f6ed7-286">儲存建置流程範本工作流程 hello 和簽入這個檔案。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-286">Save hello build process template workflow and Check In this file.</span></span>
9. <span data-ttu-id="f6ed7-287">編輯 hello 組建定義 （關閉它如果已經開啟），並選取 hello**新增**按鈕，如果您有尚未看到 hello hello 流程範本清單中的新範本。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-287">Edit hello build definition (close it if it is already open), and select hello **New** button if you do not yet see hello new template in hello list of Process Templates.</span></span>
10. <span data-ttu-id="f6ed7-288">設定 hello 參數屬性值在 hello 其他區段如下所示：</span><span class="sxs-lookup"><span data-stu-id="f6ed7-288">Set hello parameter property values in hello Misc section as follows:</span></span>

    1. <span data-ttu-id="f6ed7-289">CloudConfigLocation ='c:\\drops\\app.publish\\ServiceConfiguration.Cloud.cscfg' 此值衍生自：($PublishDir)ServiceConfiguration.Cloud.cscfg</span><span class="sxs-lookup"><span data-stu-id="f6ed7-289">CloudConfigLocation ='c:\\drops\\app.publish\\ServiceConfiguration.Cloud.cscfg' *This value is derived from: ($PublishDir)ServiceConfiguration.Cloud.cscfg*</span></span>
    2. <span data-ttu-id="f6ed7-290">PackageLocation = 'c:\\drops\\app.publish\\ContactManager.Azure.cspkg' 此值衍生自：($PublishDir)($ProjectName).cspkg</span><span class="sxs-lookup"><span data-stu-id="f6ed7-290">PackageLocation = 'c:\\drops\\app.publish\\ContactManager.Azure.cspkg' *This value is derived from: ($PublishDir)($ProjectName).cspkg*</span></span>
    3. <span data-ttu-id="f6ed7-291">PublishScriptLocation = 'c:\\scripts\\WindowsAzure\\PublishCloudService.ps1'</span><span class="sxs-lookup"><span data-stu-id="f6ed7-291">PublishScriptLocation = 'c:\\scripts\\WindowsAzure\\PublishCloudService.ps1'</span></span>
    4. <span data-ttu-id="f6ed7-292">ServiceName = 'mycloudservicename'*使用 hello 適當的雲端服務名稱*</span><span class="sxs-lookup"><span data-stu-id="f6ed7-292">ServiceName = 'mycloudservicename' *Use hello appropriate cloud service name here*</span></span>
    5. <span data-ttu-id="f6ed7-293">Environment = 'Staging'</span><span class="sxs-lookup"><span data-stu-id="f6ed7-293">Environment = 'Staging'</span></span>
    6. <span data-ttu-id="f6ed7-294">StorageAccountName = 'mystorageaccountname'*使用 hello 適當的儲存體帳戶名稱*</span><span class="sxs-lookup"><span data-stu-id="f6ed7-294">StorageAccountName = 'mystorageaccountname' *Use hello appropriate storage account name here*</span></span>
    7. <span data-ttu-id="f6ed7-295">SubscriptionDataFileLocation = 'c:\\scripts\\WindowsAzure\\Subscription.xml'</span><span class="sxs-lookup"><span data-stu-id="f6ed7-295">SubscriptionDataFileLocation = 'c:\\scripts\\WindowsAzure\\Subscription.xml'</span></span>
    8. <span data-ttu-id="f6ed7-296">SubscriptionName = 'default'</span><span class="sxs-lookup"><span data-stu-id="f6ed7-296">SubscriptionName = 'default'</span></span>

    ![參數屬性值][6]
11. <span data-ttu-id="f6ed7-298">儲存 hello 變更 toohello 組建定義。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-298">Save hello changes toohello Build Definition.</span></span>
12. <span data-ttu-id="f6ed7-299">佇列組建 tooexecute 兩者 hello 封裝組建和發行。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-299">Queue a Build tooexecute both hello package build and publish.</span></span> <span data-ttu-id="f6ed7-300">如果您有設定 tooContinuous 整合觸發程序，您也會執行這項行為每個簽入。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-300">If you have a trigger set tooContinuous Integration, you will execute this behavior on every check-in.</span></span>

### <a name="publishcloudserviceps1-script-template"></a><span data-ttu-id="f6ed7-301">PublishCloudService.ps1 指令碼範本</span><span class="sxs-lookup"><span data-stu-id="f6ed7-301">PublishCloudService.ps1 script template</span></span>
```
Param(  $serviceName = "",
        $storageAccountName = "",
        $packageLocation = "",
        $cloudConfigLocation = "",
        $environment = "Staging",
        $deploymentLabel = "ContinuousDeploy too$servicename",
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
    #check for existing deployment and then either upgrade, delete + deploy, or cancel according too$alwaysDeleteExistingDeployments and $enableDeploymentUpgrade boolean variables
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

#main driver - publish & write progress tooactivity log
Write-Output "$(Get-Date -f $timeStampFormat) - Azure Cloud Service deploy script started."
Write-Output "$(Get-Date -f $timeStampFormat) - Preparing deployment of $deploymentLabel for $subscriptionname with Subscription ID $subscriptionid."

Publish

$deployment = Get-AzureDeployment -slot $slot -serviceName $servicename
$deploymentUrl = $deployment.Url

Write-Output "$(Get-Date -f $timeStampFormat) - Created Cloud Service with URL $deploymentUrl."
Write-Output "$(Get-Date -f $timeStampFormat) - Azure Cloud Service deploy script finished."
```

## <a name="next-steps"></a><span data-ttu-id="f6ed7-302">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f6ed7-302">Next steps</span></span>
<span data-ttu-id="f6ed7-303">tooenable 遠端偵錯時使用連續的傳遞，請參閱[啟用遠端偵錯時使用持續傳遞 toopublish tooAzure](cloud-services-virtual-machines-dotnet-continuous-delivery-remote-debugging.md)。</span><span class="sxs-lookup"><span data-stu-id="f6ed7-303">tooenable remote debugging when using continuous delivery, see [Enable remote debugging when using continuous delivery toopublish tooAzure](cloud-services-virtual-machines-dotnet-continuous-delivery-remote-debugging.md).</span></span>

[Team Foundation Build Service]: https://msdn.microsoft.com/library/ee259687.aspx
[.NET Framework 4]: https://www.microsoft.com/download/details.aspx?id=17851
[.NET Framework 4.5]: https://www.microsoft.com/download/details.aspx?id=30653
[.NET Framework 4.5.2]: https://www.microsoft.com/download/details.aspx?id=42643
[Scale out your build system]: https://msdn.microsoft.com/library/dd793166.aspx
[Deploy and configure a build server]: https://msdn.microsoft.com/library/ms181712.aspx
[Azure PowerShell cmdlets]: /powershell/azureps-cmdlets-docs
[hello .publishsettings file]: https://manage.windowsazure.com/download/publishprofile.aspx?wa=wsignin1.0
[0]: ./media/cloud-services-dotnet-continuous-delivery/tfs-01bc.png
[2]: ./media/cloud-services-dotnet-continuous-delivery/tfs-02.png
[3]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-03.png
[4]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-04.png
[5]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-05.png
[6]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-06.png
