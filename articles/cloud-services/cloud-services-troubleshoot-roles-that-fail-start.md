---
title: "無法 toostart 的 aaaTroubleshoot 角色 |Microsoft 文件"
description: "以下是雲端服務角色為什麼無法 toostart 一些常見原因。 也提供解決方案 toothese 問題。"
services: cloud-services
documentationcenter: 
author: simonxjx
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: 674b2faf-26d7-4f54-99ea-a9e02ef0eb2f
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 7/26/2017
ms.author: v-six
ms.openlocfilehash: e2fbecb08a10984add79dfc74e73de6869bb314f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-cloud-service-roles-that-fail-toostart"></a><span data-ttu-id="73ada-104">疑難排解失敗 toostart 的雲端服務角色</span><span class="sxs-lookup"><span data-stu-id="73ada-104">Troubleshoot Cloud Service roles that fail toostart</span></span>
<span data-ttu-id="73ada-105">以下是一些常見的問題和解決方案無法 toostart 的相關的 tooAzure 雲端服務角色。</span><span class="sxs-lookup"><span data-stu-id="73ada-105">Here are some common problems and solutions related tooAzure Cloud Services roles that fail toostart.</span></span>

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="missing-dlls-or-dependencies"></a><span data-ttu-id="73ada-106">遺失 Dll 或相依性</span><span class="sxs-lookup"><span data-stu-id="73ada-106">Missing DLLs or dependencies</span></span>
<span data-ttu-id="73ada-107">角色沒有回應，以及角色在 [正在初始化]、[忙碌] 和 [正在停止] 狀態之間循環，有可能是因為遺失 DLL 或組件所致。</span><span class="sxs-lookup"><span data-stu-id="73ada-107">Unresponsive roles and roles that are cycling between **Initializing**, **Busy**, and **Stopping** states can be caused by missing DLLs or assemblies.</span></span>

<span data-ttu-id="73ada-108">遺失 DLL 或組件的徵狀可能是：</span><span class="sxs-lookup"><span data-stu-id="73ada-108">Symptoms of missing DLLs or assemblies can be:</span></span>

* <span data-ttu-id="73ada-109">您的角色執行個體在 [正在初始化]、[忙碌] 及 [正在停止] 狀態之間循環。</span><span class="sxs-lookup"><span data-stu-id="73ada-109">Your role instance is cycling through **Initializing**, **Busy**, and **Stopping** states.</span></span>
* <span data-ttu-id="73ada-110">您的角色執行個體已經移動過**準備**但如果您導覽 tooyour web 應用程式時，不會出現 hello 頁面。</span><span class="sxs-lookup"><span data-stu-id="73ada-110">Your role instance has moved too**Ready** but if you navigate tooyour web application, hello page does not appear.</span></span>

<span data-ttu-id="73ada-111">有數個建議的方法可調查這些問題。</span><span class="sxs-lookup"><span data-stu-id="73ada-111">There are several recommended methods for investigating these issues.</span></span>

## <a name="diagnose-missing-dll-issues-in-a-web-role"></a><span data-ttu-id="73ada-112">診斷 Web 角色中遺失 DLL 的問題</span><span class="sxs-lookup"><span data-stu-id="73ada-112">Diagnose missing DLL issues in a web role</span></span>
<span data-ttu-id="73ada-113">當您瀏覽 tooa 網站，部署在 web 角色，並 hello 瀏覽器會顯示伺服器錯誤類似 toohello 後的時，它可能表示 DLL 遺失。</span><span class="sxs-lookup"><span data-stu-id="73ada-113">When you navigate tooa website that is deployed in a web role, and hello browser displays a server error similar toohello following, it may indicate that a DLL is missing.</span></span>

!['/' 應用程式中有伺服器錯誤。](./media/cloud-services-troubleshoot-roles-that-fail-start/ic503388.png)

## <a name="diagnose-issues-by-turning-off-custom-errors"></a><span data-ttu-id="73ada-115">關閉自訂錯誤以診斷問題</span><span class="sxs-lookup"><span data-stu-id="73ada-115">Diagnose issues by turning off custom errors</span></span>
<span data-ttu-id="73ada-116">可以藉由設定 hello web 角色 tooset hello 自訂錯誤模式 tooOff hello web.config 和重新部署 hello 服務檢視更完整資訊時發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="73ada-116">More complete error information can be viewed by configuring hello web.config for hello web role tooset hello custom error mode tooOff and redeploying hello service.</span></span>

<span data-ttu-id="73ada-117">tooview 更完成而不需要使用遠端桌面的錯誤：</span><span class="sxs-lookup"><span data-stu-id="73ada-117">tooview more complete errors without using Remote Desktop:</span></span>

1. <span data-ttu-id="73ada-118">開啟 Microsoft Visual Studio 中的 hello 方案。</span><span class="sxs-lookup"><span data-stu-id="73ada-118">Open hello solution in Microsoft Visual Studio.</span></span>
2. <span data-ttu-id="73ada-119">在 [hello**方案總管] 中**，找出 hello web.config 檔案，並將它開啟。</span><span class="sxs-lookup"><span data-stu-id="73ada-119">In hello **Solution Explorer**, locate hello web.config file and open it.</span></span>
3. <span data-ttu-id="73ada-120">在 hello web.config 檔案中，找出 hello system.web 區段並加入以下的 hello:</span><span class="sxs-lookup"><span data-stu-id="73ada-120">In hello web.config file, locate hello system.web section and add hello following line:</span></span>

    ```xml
    <customErrors mode="Off" />
    ```
4. <span data-ttu-id="73ada-121">儲存 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="73ada-121">Save hello file.</span></span>
5. <span data-ttu-id="73ada-122">重新封裝，然後重新部署 hello 服務。</span><span class="sxs-lookup"><span data-stu-id="73ada-122">Repackage and redeploy hello service.</span></span>

<span data-ttu-id="73ada-123">一旦 hello 服務重新部署之後，您會看到 hello hello 遺漏組件或 DLL 名稱的錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="73ada-123">Once hello service is redeployed, you will see an error message with hello name of hello missing assembly or DLL.</span></span>

## <a name="diagnose-issues-by-viewing-hello-error-remotely"></a><span data-ttu-id="73ada-124">藉由從遠端檢視 hello 錯誤診斷問題</span><span class="sxs-lookup"><span data-stu-id="73ada-124">Diagnose issues by viewing hello error remotely</span></span>
<span data-ttu-id="73ada-125">您可以使用遠端桌面 tooaccess hello 角色，並從遠端檢視更完整資訊時發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="73ada-125">You can use Remote Desktop tooaccess hello role and view more complete error information remotely.</span></span> <span data-ttu-id="73ada-126">使用下列步驟 tooview hello 錯誤使用遠端桌面的 hello:</span><span class="sxs-lookup"><span data-stu-id="73ada-126">Use hello following steps tooview hello errors by using Remote Desktop:</span></span>

1. <span data-ttu-id="73ada-127">確定已安裝 Azure SDK 1.3 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="73ada-127">Ensure that Azure SDK 1.3 or later is installed.</span></span>
2. <span data-ttu-id="73ada-128">太 hello 部署期間使用 Visual Studio 的 hello 方案，選擇  設定遠端桌面連線。</span><span class="sxs-lookup"><span data-stu-id="73ada-128">During hello deployment of hello solution by using Visual Studio, choose too“Configure Remote Desktop connections…”.</span></span> <span data-ttu-id="73ada-129">如需設定 hello 遠端桌面連線的詳細資訊，請參閱[透過 Azure 角色使用遠端桌面](../vs-azure-tools-remote-desktop-roles.md)。</span><span class="sxs-lookup"><span data-stu-id="73ada-129">For more information on configuring hello Remote Desktop connection, see [Using Remote Desktop with Azure Roles](../vs-azure-tools-remote-desktop-roles.md).</span></span>
3. <span data-ttu-id="73ada-130">Hello Microsoft Azure 傳統入口網站中，一旦 hello 執行個體顯示狀態**準備**，按一下其中一個 hello 角色執行個體。</span><span class="sxs-lookup"><span data-stu-id="73ada-130">In hello Microsoft Azure classic portal, once hello instance shows a status of **Ready**, click one of hello role instances.</span></span>
4. <span data-ttu-id="73ada-131">按一下 hello**連接**圖示 hello**遠端存取**hello 功能區的區域。</span><span class="sxs-lookup"><span data-stu-id="73ada-131">Click hello **Connect** icon in hello **Remote Access** area of hello ribbon.</span></span>
5. <span data-ttu-id="73ada-132">使用 hello hello 遠端桌面組態期間指定的認證登入 toohello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="73ada-132">Sign in toohello virtual machine by using hello credentials that were specified during hello Remote Desktop configuration.</span></span>
6. <span data-ttu-id="73ada-133">開啟命令視窗。</span><span class="sxs-lookup"><span data-stu-id="73ada-133">Open a command window.</span></span>
7. <span data-ttu-id="73ada-134">輸入 `IPconfig`。</span><span class="sxs-lookup"><span data-stu-id="73ada-134">Type `IPconfig`.</span></span>
8. <span data-ttu-id="73ada-135">請注意 hello IPV4 位址的值。</span><span class="sxs-lookup"><span data-stu-id="73ada-135">Note hello IPV4 Address value.</span></span>
9. <span data-ttu-id="73ada-136">開啟 Internet Explorer。</span><span class="sxs-lookup"><span data-stu-id="73ada-136">Open Internet Explorer.</span></span>
10. <span data-ttu-id="73ada-137">輸入 hello 位址和 hello hello web 應用程式名稱。</span><span class="sxs-lookup"><span data-stu-id="73ada-137">Type hello address and hello name of hello web application.</span></span> <span data-ttu-id="73ada-138">例如： `http://<IPV4 Address>/default.aspx`。</span><span class="sxs-lookup"><span data-stu-id="73ada-138">For example, `http://<IPV4 Address>/default.aspx`.</span></span>

<span data-ttu-id="73ada-139">瀏覽 toohello 網站現在會傳回更明確的錯誤訊息：</span><span class="sxs-lookup"><span data-stu-id="73ada-139">Navigating toohello website will now return more explicit error messages:</span></span>

* <span data-ttu-id="73ada-140">'/' 應用程式中有伺服器錯誤。</span><span class="sxs-lookup"><span data-stu-id="73ada-140">Server Error in '/' Application.</span></span>
* <span data-ttu-id="73ada-141">描述： Hello 執行 hello 目前 web 要求期間發生未處理的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="73ada-141">Description: An unhandled exception occurred during hello execution of hello current web request.</span></span> <span data-ttu-id="73ada-142">請檢閱有關 hello 錯誤更多資訊的 hello 堆疊追蹤以及產生 hello 程式碼中的位置。</span><span class="sxs-lookup"><span data-stu-id="73ada-142">Please review hello stack trace for more information about hello error and where it originated in hello code.</span></span>
* <span data-ttu-id="73ada-143">例外狀況詳細資料：System.IO.FIleNotFoundException：無法載入檔案或組件 ‘Microsoft.WindowsAzure.StorageClient，Version=1.1.0.0，Culture=neutral，PublicKeyToken=31bf856ad364e35’ 或其相依性之一。</span><span class="sxs-lookup"><span data-stu-id="73ada-143">Exception Details: System.IO.FIleNotFoundException: Could not load file or assembly ‘Microsoft.WindowsAzure.StorageClient, Version=1.1.0.0, Culture=neutral, PublicKeyToken=31bf856ad364e35’ or one of its dependencies.</span></span> <span data-ttu-id="73ada-144">hello 系統找不到指定的 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="73ada-144">hello system cannot find hello file specified.</span></span>

<span data-ttu-id="73ada-145">例如：</span><span class="sxs-lookup"><span data-stu-id="73ada-145">For example:</span></span>

!['/' 應用程式中有明確的伺服器錯誤。](./media/cloud-services-troubleshoot-roles-that-fail-start/ic503389.png)

## <a name="diagnose-issues-by-using-hello-compute-emulator"></a><span data-ttu-id="73ada-147">使用 hello 計算模擬器來診斷問題</span><span class="sxs-lookup"><span data-stu-id="73ada-147">Diagnose issues by using hello compute emulator</span></span>
<span data-ttu-id="73ada-148">您可以使用 hello Microsoft Azure 計算模擬器 toodiagnose 後遺失相依性與 web.config 錯誤的問題進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="73ada-148">You can use hello Microsoft Azure compute emulator toodiagnose and troubleshoot issues of missing dependencies and web.config errors.</span></span>

<span data-ttu-id="73ada-149">若要讓這種診斷方法獲得最佳結果，您應該使用具有 Windows 全新安裝的電腦或虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="73ada-149">For best results in using this method of diagnosis, you should use a computer or virtual machine that has a clean installation of Windows.</span></span> <span data-ttu-id="73ada-150">toobest 模擬 hello Azure 環境，請使用 Windows Server 2008 R2 x64。</span><span class="sxs-lookup"><span data-stu-id="73ada-150">toobest simulate hello Azure environment, use Windows Server 2008 R2 x64.</span></span>

1. <span data-ttu-id="73ada-151">安裝 hello 獨立版的 hello [Azure SDK](https://azure.microsoft.com/downloads/)。</span><span class="sxs-lookup"><span data-stu-id="73ada-151">Install hello standalone version of hello [Azure SDK](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="73ada-152">Hello 開發在電腦上，建置 hello 雲端服務專案。</span><span class="sxs-lookup"><span data-stu-id="73ada-152">On hello development machine, build hello cloud service project.</span></span>
3. <span data-ttu-id="73ada-153">在 Windows 檔案總管，瀏覽 toohello hello 雲端服務專案的 bin\debug 資料夾。</span><span class="sxs-lookup"><span data-stu-id="73ada-153">In Windows Explorer, navigate toohello bin\debug folder of hello cloud service project.</span></span>
4. <span data-ttu-id="73ada-154">複製 hello.csx 資料夾及.cscfg 檔案 toohello 電腦使用 toodebug hello 問題。</span><span class="sxs-lookup"><span data-stu-id="73ada-154">Copy hello .csx folder and .cscfg file toohello computer that you are using toodebug hello issues.</span></span>
5. <span data-ttu-id="73ada-155">Hello 清除電腦上開啟 Azure SDK 命令提示字元視窗，輸入`csrun.exe /devstore:start`。</span><span class="sxs-lookup"><span data-stu-id="73ada-155">On hello clean machine, open an Azure SDK Command Prompt window and type `csrun.exe /devstore:start`.</span></span>
6. <span data-ttu-id="73ada-156">在 hello 命令提示字元中輸入`run csrun <path too.csx folder> <path too.cscfg file> /launchBrowser`。</span><span class="sxs-lookup"><span data-stu-id="73ada-156">At hello command prompt, type `run csrun <path too.csx folder> <path too.cscfg file> /launchBrowser`.</span></span>
7. <span data-ttu-id="73ada-157">Hello 角色啟動時，您會看到詳細的錯誤資訊，在 Internet Explorer 中。</span><span class="sxs-lookup"><span data-stu-id="73ada-157">When hello role starts, you will see detailed error information in Internet Explorer.</span></span> <span data-ttu-id="73ada-158">您也可以使用標準的 Windows 疑難排解工具 toofurther 診斷 hello 問題。</span><span class="sxs-lookup"><span data-stu-id="73ada-158">You can also use standard Windows troubleshooting tools toofurther diagnose hello problem.</span></span>

## <a name="diagnose-issues-by-using-intellitrace"></a><span data-ttu-id="73ada-159">使用 IntelliTrace 診斷問題</span><span class="sxs-lookup"><span data-stu-id="73ada-159">Diagnose issues by using IntelliTrace</span></span>
<span data-ttu-id="73ada-160">對於使用 .NET Framework 4 的背景工作角色和 Web 角色，您可以使用 Microsoft Visual Studio Enterprise 所提供的 [IntelliTrace](https://msdn.microsoft.com/library/dd264915.aspx)。</span><span class="sxs-lookup"><span data-stu-id="73ada-160">For worker and web roles that use .NET Framework 4, you can use [IntelliTrace](https://msdn.microsoft.com/library/dd264915.aspx), which is available in Microsoft Visual Studio Enterprise.</span></span>

<span data-ttu-id="73ada-161">啟用了 IntelliTrace，請遵循這些步驟 toodeploy hello 服務：</span><span class="sxs-lookup"><span data-stu-id="73ada-161">Follow these steps toodeploy hello service with IntelliTrace enabled:</span></span>

1. <span data-ttu-id="73ada-162">確定已安裝 Azure SDK 1.3 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="73ada-162">Confirm that Azure SDK 1.3 or later is installed.</span></span>
2. <span data-ttu-id="73ada-163">使用 Visual Studio 部署 hello 方案。</span><span class="sxs-lookup"><span data-stu-id="73ada-163">Deploy hello solution by using Visual Studio.</span></span> <span data-ttu-id="73ada-164">在部署期間，檢查 hello**為.NET 4 角色啟用 IntelliTrace**核取方塊。</span><span class="sxs-lookup"><span data-stu-id="73ada-164">During deployment, check hello **Enable IntelliTrace for .NET 4 roles** check box.</span></span>
3. <span data-ttu-id="73ada-165">一旦 hello 執行個體啟動時，開啟 hello**伺服器總管**。</span><span class="sxs-lookup"><span data-stu-id="73ada-165">Once hello instance starts, open hello **Server Explorer**.</span></span>
4. <span data-ttu-id="73ada-166">展開 hello **Azure\\雲端服務**節點並找出 hello 部署。</span><span class="sxs-lookup"><span data-stu-id="73ada-166">Expand hello **Azure\\Cloud Services** node and locate hello deployment.</span></span>
5. <span data-ttu-id="73ada-167">展開 hello 部署，直到您看到 hello 角色執行個體。</span><span class="sxs-lookup"><span data-stu-id="73ada-167">Expand hello deployment until you see hello role instances.</span></span> <span data-ttu-id="73ada-168">以滑鼠右鍵按一下其中一個 hello 執行個體。</span><span class="sxs-lookup"><span data-stu-id="73ada-168">Right-click on one of hello instances.</span></span>
6. <span data-ttu-id="73ada-169">選擇 [檢視 IntelliTrace 記錄檔] 。</span><span class="sxs-lookup"><span data-stu-id="73ada-169">Choose **View IntelliTrace logs**.</span></span> <span data-ttu-id="73ada-170">hello **IntelliTrace 摘要**隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="73ada-170">hello **IntelliTrace Summary** will open.</span></span>
7. <span data-ttu-id="73ada-171">找出 hello hello 摘要的例外狀況 > 一節。</span><span class="sxs-lookup"><span data-stu-id="73ada-171">Locate hello exceptions section of hello summary.</span></span> <span data-ttu-id="73ada-172">如果有例外狀況，將會標示為 hello 區段**例外狀況資料**。</span><span class="sxs-lookup"><span data-stu-id="73ada-172">If there are exceptions, hello section will be labeled **Exception Data**.</span></span>
8. <span data-ttu-id="73ada-173">展開 hello**例外狀況資料**並尋找**System.IO.FileNotFoundException**類似 toohello 下列錯誤：</span><span class="sxs-lookup"><span data-stu-id="73ada-173">Expand hello **Exception Data** and look for **System.IO.FileNotFoundException** errors similar toohello following:</span></span>

![例外狀況資料、遺失檔案或組件](./media/cloud-services-troubleshoot-roles-that-fail-start/ic503390.png)

## <a name="address-missing-dlls-and-assemblies"></a><span data-ttu-id="73ada-175">解決遺失 Dll 和組件的問題</span><span class="sxs-lookup"><span data-stu-id="73ada-175">Address missing DLLs and assemblies</span></span>
<span data-ttu-id="73ada-176">tooaddress 遺失 DLL 和組件的錯誤，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="73ada-176">tooaddress missing DLL and assembly errors, follow these steps:</span></span>

1. <span data-ttu-id="73ada-177">開啟 Visual Studio 中的 hello 方案。</span><span class="sxs-lookup"><span data-stu-id="73ada-177">Open hello solution in Visual Studio.</span></span>
2. <span data-ttu-id="73ada-178">在**方案總管 中**，開啟 hello**參考**資料夾。</span><span class="sxs-lookup"><span data-stu-id="73ada-178">In **Solution Explorer**, open hello **References** folder.</span></span>
3. <span data-ttu-id="73ada-179">按一下 hello hello 錯誤中指出的組件。</span><span class="sxs-lookup"><span data-stu-id="73ada-179">Click hello assembly identified in hello error.</span></span>
4. <span data-ttu-id="73ada-180">在 hello**屬性** 窗格中，找出**複製本機屬性**並將 hello 值設定為太**True**。</span><span class="sxs-lookup"><span data-stu-id="73ada-180">In hello **Properties** pane, locate **Copy Local property** and set hello value too**True**.</span></span>
5. <span data-ttu-id="73ada-181">重新部署 hello 雲端服務。</span><span class="sxs-lookup"><span data-stu-id="73ada-181">Redeploy hello cloud service.</span></span>

<span data-ttu-id="73ada-182">一旦您確認已更正所有錯誤時，您可以部署 hello 服務而不檢查 hello**為.NET 4 角色啟用 IntelliTrace**核取方塊。</span><span class="sxs-lookup"><span data-stu-id="73ada-182">Once you have verified that all errors have been corrected, you can deploy hello service without checking hello **Enable IntelliTrace for .NET 4 roles** check box.</span></span>

## <a name="next-steps"></a><span data-ttu-id="73ada-183">後續步驟</span><span class="sxs-lookup"><span data-stu-id="73ada-183">Next steps</span></span>
<span data-ttu-id="73ada-184">檢視更多雲端服務的 [疑難排解文章](https://azure.microsoft.com/documentation/articles/?tag=top-support-issue&product=cloud-services) 。</span><span class="sxs-lookup"><span data-stu-id="73ada-184">View more [troubleshooting articles](https://azure.microsoft.com/documentation/articles/?tag=top-support-issue&product=cloud-services) for cloud services.</span></span>

<span data-ttu-id="73ada-185">toolearn tootroubleshoot 雲端服務角色如何發出使用 Azure PaaS 電腦診斷資料，請參閱[Kevin Williamson 部落格系列](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx)。</span><span class="sxs-lookup"><span data-stu-id="73ada-185">toolearn how tootroubleshoot cloud service role issues by using Azure PaaS computer diagnostics data, see [Kevin Williamson's blog series](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).</span></span>
