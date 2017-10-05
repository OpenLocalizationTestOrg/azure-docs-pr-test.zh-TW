---
title: "針對無法啟動的角色進行疑難排解 | Microsoft Docs"
description: "以下是雲端服務角色無法啟動的一些常見原因。 此外也提供這些問題的解決方案。"
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
ms.openlocfilehash: 7d956192e8b9c3688b8b6f0108bd9296f66fbd62
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="troubleshoot-cloud-service-roles-that-fail-to-start"></a><span data-ttu-id="0ee55-104">對無法啟動的雲端服務角色進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="0ee55-104">Troubleshoot Cloud Service roles that fail to start</span></span>
<span data-ttu-id="0ee55-105">以下是與無法啟動的 Azure 雲端服務角色相關的一些常見問題和解決方案。</span><span class="sxs-lookup"><span data-stu-id="0ee55-105">Here are some common problems and solutions related to Azure Cloud Services roles that fail to start.</span></span>

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="missing-dlls-or-dependencies"></a><span data-ttu-id="0ee55-106">遺失 Dll 或相依性</span><span class="sxs-lookup"><span data-stu-id="0ee55-106">Missing DLLs or dependencies</span></span>
<span data-ttu-id="0ee55-107">角色沒有回應，以及角色在 [正在初始化]、[忙碌] 和 [正在停止] 狀態之間循環，有可能是因為遺失 DLL 或組件所致。</span><span class="sxs-lookup"><span data-stu-id="0ee55-107">Unresponsive roles and roles that are cycling between **Initializing**, **Busy**, and **Stopping** states can be caused by missing DLLs or assemblies.</span></span>

<span data-ttu-id="0ee55-108">遺失 DLL 或組件的徵狀可能是：</span><span class="sxs-lookup"><span data-stu-id="0ee55-108">Symptoms of missing DLLs or assemblies can be:</span></span>

* <span data-ttu-id="0ee55-109">您的角色執行個體在 [正在初始化]、[忙碌] 及 [正在停止] 狀態之間循環。</span><span class="sxs-lookup"><span data-stu-id="0ee55-109">Your role instance is cycling through **Initializing**, **Busy**, and **Stopping** states.</span></span>
* <span data-ttu-id="0ee55-110">您的角色執行個體已進入 [就緒]  狀態，但當您瀏覽至 Web 應用程式時，發現頁面並未顯示。</span><span class="sxs-lookup"><span data-stu-id="0ee55-110">Your role instance has moved to **Ready** but if you navigate to your web application, the page does not appear.</span></span>

<span data-ttu-id="0ee55-111">有數個建議的方法可調查這些問題。</span><span class="sxs-lookup"><span data-stu-id="0ee55-111">There are several recommended methods for investigating these issues.</span></span>

## <a name="diagnose-missing-dll-issues-in-a-web-role"></a><span data-ttu-id="0ee55-112">診斷 Web 角色中遺失 DLL 的問題</span><span class="sxs-lookup"><span data-stu-id="0ee55-112">Diagnose missing DLL issues in a web role</span></span>
<span data-ttu-id="0ee55-113">當您瀏覽至在 Web 角色中部署的網站時，瀏覽器顯示如下的伺服器錯誤，表示可能遺失 DLL。</span><span class="sxs-lookup"><span data-stu-id="0ee55-113">When you navigate to a website that is deployed in a web role, and the browser displays a server error similar to the following, it may indicate that a DLL is missing.</span></span>

!['/' 應用程式中有伺服器錯誤。](./media/cloud-services-troubleshoot-roles-that-fail-start/ic503388.png)

## <a name="diagnose-issues-by-turning-off-custom-errors"></a><span data-ttu-id="0ee55-115">關閉自訂錯誤以診斷問題</span><span class="sxs-lookup"><span data-stu-id="0ee55-115">Diagnose issues by turning off custom errors</span></span>
<span data-ttu-id="0ee55-116">設定 Web 角色的 web.config 以將自訂錯誤模式設為關閉，並重新部署服務，可以檢視更完整的錯誤資訊。</span><span class="sxs-lookup"><span data-stu-id="0ee55-116">More complete error information can be viewed by configuring the web.config for the web role to set the custom error mode to Off and redeploying the service.</span></span>

<span data-ttu-id="0ee55-117">若要檢視更完整的錯誤而不使用遠端桌面：</span><span class="sxs-lookup"><span data-stu-id="0ee55-117">To view more complete errors without using Remote Desktop:</span></span>

1. <span data-ttu-id="0ee55-118">在 Microsoft Visual Studio 中開啟解決方案。</span><span class="sxs-lookup"><span data-stu-id="0ee55-118">Open the solution in Microsoft Visual Studio.</span></span>
2. <span data-ttu-id="0ee55-119">在 [方案總管] 中找出 web.config 檔案，並加以開啟。</span><span class="sxs-lookup"><span data-stu-id="0ee55-119">In the **Solution Explorer**, locate the web.config file and open it.</span></span>
3. <span data-ttu-id="0ee55-120">在 web.config 檔案中找出 system.web 區段，並加入下面這一行：</span><span class="sxs-lookup"><span data-stu-id="0ee55-120">In the web.config file, locate the system.web section and add the following line:</span></span>

    ```xml
    <customErrors mode="Off" />
    ```
4. <span data-ttu-id="0ee55-121">儲存檔案。</span><span class="sxs-lookup"><span data-stu-id="0ee55-121">Save the file.</span></span>
5. <span data-ttu-id="0ee55-122">重新封裝並重新部署服務。</span><span class="sxs-lookup"><span data-stu-id="0ee55-122">Repackage and redeploy the service.</span></span>

<span data-ttu-id="0ee55-123">重新部署服務之後，您會看到下列錯誤訊息，以及遺失組件或 DLL 的名稱。</span><span class="sxs-lookup"><span data-stu-id="0ee55-123">Once the service is redeployed, you will see an error message with the name of the missing assembly or DLL.</span></span>

## <a name="diagnose-issues-by-viewing-the-error-remotely"></a><span data-ttu-id="0ee55-124">從遠端檢視錯誤以診斷問題</span><span class="sxs-lookup"><span data-stu-id="0ee55-124">Diagnose issues by viewing the error remotely</span></span>
<span data-ttu-id="0ee55-125">您可以使用遠端桌面存取角色，並從遠端檢視更完整的錯誤資訊。</span><span class="sxs-lookup"><span data-stu-id="0ee55-125">You can use Remote Desktop to access the role and view more complete error information remotely.</span></span> <span data-ttu-id="0ee55-126">使用下列步驟，可使用遠端桌面檢視錯誤：</span><span class="sxs-lookup"><span data-stu-id="0ee55-126">Use the following steps to view the errors by using Remote Desktop:</span></span>

1. <span data-ttu-id="0ee55-127">確定已安裝 Azure SDK 1.3 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="0ee55-127">Ensure that Azure SDK 1.3 or later is installed.</span></span>
2. <span data-ttu-id="0ee55-128">在使用 Visual Studio 部署解決方案期間，選擇「設定遠端桌面連線...」。</span><span class="sxs-lookup"><span data-stu-id="0ee55-128">During the deployment of the solution by using Visual Studio, choose to “Configure Remote Desktop connections…”.</span></span> <span data-ttu-id="0ee55-129">如需設定遠端桌面連線的詳細資訊，請參閱 [搭配使用遠端桌面與 Azure 角色](../vs-azure-tools-remote-desktop-roles.md)。</span><span class="sxs-lookup"><span data-stu-id="0ee55-129">For more information on configuring the Remote Desktop connection, see [Using Remote Desktop with Azure Roles](../vs-azure-tools-remote-desktop-roles.md).</span></span>
3. <span data-ttu-id="0ee55-130">在 Microsoft Azure 傳統入口網站中，當執行個體的顯示狀態為 [就緒] 時，按一下其中一個角色執行個體。</span><span class="sxs-lookup"><span data-stu-id="0ee55-130">In the Microsoft Azure classic portal, once the instance shows a status of **Ready**, click one of the role instances.</span></span>
4. <span data-ttu-id="0ee55-131">在功能區的 [遠端存取] 區域中，按一下 [連接] 圖示。</span><span class="sxs-lookup"><span data-stu-id="0ee55-131">Click the **Connect** icon in the **Remote Access** area of the ribbon.</span></span>
5. <span data-ttu-id="0ee55-132">使用在遠端桌面設定期間指定的認證登入虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="0ee55-132">Sign in to the virtual machine by using the credentials that were specified during the Remote Desktop configuration.</span></span>
6. <span data-ttu-id="0ee55-133">開啟命令視窗。</span><span class="sxs-lookup"><span data-stu-id="0ee55-133">Open a command window.</span></span>
7. <span data-ttu-id="0ee55-134">輸入 `IPconfig`。</span><span class="sxs-lookup"><span data-stu-id="0ee55-134">Type `IPconfig`.</span></span>
8. <span data-ttu-id="0ee55-135">記下 IPV4 位址值。</span><span class="sxs-lookup"><span data-stu-id="0ee55-135">Note the IPV4 Address value.</span></span>
9. <span data-ttu-id="0ee55-136">開啟 Internet Explorer。</span><span class="sxs-lookup"><span data-stu-id="0ee55-136">Open Internet Explorer.</span></span>
10. <span data-ttu-id="0ee55-137">輸入 Web 應用程式的位址和名稱。</span><span class="sxs-lookup"><span data-stu-id="0ee55-137">Type the address and the name of the web application.</span></span> <span data-ttu-id="0ee55-138">例如， `http://<IPV4 Address>/default.aspx`。</span><span class="sxs-lookup"><span data-stu-id="0ee55-138">For example, `http://<IPV4 Address>/default.aspx`.</span></span>

<span data-ttu-id="0ee55-139">瀏覽至網站現在會傳回更明確的錯誤訊息：</span><span class="sxs-lookup"><span data-stu-id="0ee55-139">Navigating to the website will now return more explicit error messages:</span></span>

* <span data-ttu-id="0ee55-140">'/' 應用程式中有伺服器錯誤。</span><span class="sxs-lookup"><span data-stu-id="0ee55-140">Server Error in '/' Application.</span></span>
* <span data-ttu-id="0ee55-141">說明：執行目前的 Web 要求期間發生未處理的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="0ee55-141">Description: An unhandled exception occurred during the execution of the current web request.</span></span> <span data-ttu-id="0ee55-142">請檢閱堆疊追蹤，以進一步了解錯誤以及它產生於程式碼中的何處。</span><span class="sxs-lookup"><span data-stu-id="0ee55-142">Please review the stack trace for more information about the error and where it originated in the code.</span></span>
* <span data-ttu-id="0ee55-143">例外狀況詳細資料：System.IO.FIleNotFoundException：無法載入檔案或組件 ‘Microsoft.WindowsAzure.StorageClient，Version=1.1.0.0，Culture=neutral，PublicKeyToken=31bf856ad364e35’ 或其相依性之一。</span><span class="sxs-lookup"><span data-stu-id="0ee55-143">Exception Details: System.IO.FIleNotFoundException: Could not load file or assembly ‘Microsoft.WindowsAzure.StorageClient, Version=1.1.0.0, Culture=neutral, PublicKeyToken=31bf856ad364e35’ or one of its dependencies.</span></span> <span data-ttu-id="0ee55-144">系統找不到指定的檔案。</span><span class="sxs-lookup"><span data-stu-id="0ee55-144">The system cannot find the file specified.</span></span>

<span data-ttu-id="0ee55-145">例如：</span><span class="sxs-lookup"><span data-stu-id="0ee55-145">For example:</span></span>

!['/' 應用程式中有明確的伺服器錯誤。](./media/cloud-services-troubleshoot-roles-that-fail-start/ic503389.png)

## <a name="diagnose-issues-by-using-the-compute-emulator"></a><span data-ttu-id="0ee55-147">使用計算模擬器診斷問題</span><span class="sxs-lookup"><span data-stu-id="0ee55-147">Diagnose issues by using the compute emulator</span></span>
<span data-ttu-id="0ee55-148">您可以使用 Microsoft Azure 計算模擬器來診斷和排解遺失相依性與 web.config 錯誤的問題。</span><span class="sxs-lookup"><span data-stu-id="0ee55-148">You can use the Microsoft Azure compute emulator to diagnose and troubleshoot issues of missing dependencies and web.config errors.</span></span>

<span data-ttu-id="0ee55-149">若要讓這種診斷方法獲得最佳結果，您應該使用具有 Windows 全新安裝的電腦或虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="0ee55-149">For best results in using this method of diagnosis, you should use a computer or virtual machine that has a clean installation of Windows.</span></span> <span data-ttu-id="0ee55-150">若要達到模擬 Azure 環境的最佳效果，請使用 Windows Server 2008 R2 x64。</span><span class="sxs-lookup"><span data-stu-id="0ee55-150">To best simulate the Azure environment, use Windows Server 2008 R2 x64.</span></span>

1. <span data-ttu-id="0ee55-151">安裝獨立版的 [Azure SDK](https://azure.microsoft.com/downloads/)。</span><span class="sxs-lookup"><span data-stu-id="0ee55-151">Install the standalone version of the [Azure SDK](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="0ee55-152">在開發電腦上建置雲端服務專案。</span><span class="sxs-lookup"><span data-stu-id="0ee55-152">On the development machine, build the cloud service project.</span></span>
3. <span data-ttu-id="0ee55-153">在 Windows 檔案總管中，瀏覽至雲端服務專案的 bin\debug 資料夾。</span><span class="sxs-lookup"><span data-stu-id="0ee55-153">In Windows Explorer, navigate to the bin\debug folder of the cloud service project.</span></span>
4. <span data-ttu-id="0ee55-154">將 .csx 資料夾及 .cscfg 檔案複製到您用來偵錯問題的電腦。</span><span class="sxs-lookup"><span data-stu-id="0ee55-154">Copy the .csx folder and .cscfg file to the computer that you are using to debug the issues.</span></span>
5. <span data-ttu-id="0ee55-155">在初始狀態的電腦上開啟 Azure SDK 命令提示字元視窗，並輸入 `csrun.exe /devstore:start`。</span><span class="sxs-lookup"><span data-stu-id="0ee55-155">On the clean machine, open an Azure SDK Command Prompt window and type `csrun.exe /devstore:start`.</span></span>
6. <span data-ttu-id="0ee55-156">在命令提示字元中，輸入 `run csrun <path to .csx folder> <path to .cscfg file> /launchBrowser`。</span><span class="sxs-lookup"><span data-stu-id="0ee55-156">At the command prompt, type `run csrun <path to .csx folder> <path to .cscfg file> /launchBrowser`.</span></span>
7. <span data-ttu-id="0ee55-157">在角色啟動時，您會在 Internet Explorer 中看到詳細的錯誤資訊。</span><span class="sxs-lookup"><span data-stu-id="0ee55-157">When the role starts, you will see detailed error information in Internet Explorer.</span></span> <span data-ttu-id="0ee55-158">您也可以使用標準 Windows 疑難排解工具進一步診斷問題。</span><span class="sxs-lookup"><span data-stu-id="0ee55-158">You can also use standard Windows troubleshooting tools to further diagnose the problem.</span></span>

## <a name="diagnose-issues-by-using-intellitrace"></a><span data-ttu-id="0ee55-159">使用 IntelliTrace 診斷問題</span><span class="sxs-lookup"><span data-stu-id="0ee55-159">Diagnose issues by using IntelliTrace</span></span>
<span data-ttu-id="0ee55-160">對於使用 .NET Framework 4 的背景工作角色和 Web 角色，您可以使用 Microsoft Visual Studio Enterprise 所提供的 [IntelliTrace](https://msdn.microsoft.com/library/dd264915.aspx)。</span><span class="sxs-lookup"><span data-stu-id="0ee55-160">For worker and web roles that use .NET Framework 4, you can use [IntelliTrace](https://msdn.microsoft.com/library/dd264915.aspx), which is available in Microsoft Visual Studio Enterprise.</span></span>

<span data-ttu-id="0ee55-161">請遵循下列步驟，部署已啟用 IntelliTrace 的服務：</span><span class="sxs-lookup"><span data-stu-id="0ee55-161">Follow these steps to deploy the service with IntelliTrace enabled:</span></span>

1. <span data-ttu-id="0ee55-162">確定已安裝 Azure SDK 1.3 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="0ee55-162">Confirm that Azure SDK 1.3 or later is installed.</span></span>
2. <span data-ttu-id="0ee55-163">使用 Visual Studio 部署解決方案。</span><span class="sxs-lookup"><span data-stu-id="0ee55-163">Deploy the solution by using Visual Studio.</span></span> <span data-ttu-id="0ee55-164">在部署期間，勾選 [為 .NET 4 角色啟用 IntelliTrace]  核取方塊。</span><span class="sxs-lookup"><span data-stu-id="0ee55-164">During deployment, check the **Enable IntelliTrace for .NET 4 roles** check box.</span></span>
3. <span data-ttu-id="0ee55-165">執行個體啟動後，請開啟 [伺服器總管] 。</span><span class="sxs-lookup"><span data-stu-id="0ee55-165">Once the instance starts, open the **Server Explorer**.</span></span>
4. <span data-ttu-id="0ee55-166">展開 [Azure]\\[雲端服務] 節點，並找出部署。</span><span class="sxs-lookup"><span data-stu-id="0ee55-166">Expand the **Azure\\Cloud Services** node and locate the deployment.</span></span>
5. <span data-ttu-id="0ee55-167">展開部署，直到您看見角色執行個體。</span><span class="sxs-lookup"><span data-stu-id="0ee55-167">Expand the deployment until you see the role instances.</span></span> <span data-ttu-id="0ee55-168">以滑鼠右鍵按一下其中一個執行個體。</span><span class="sxs-lookup"><span data-stu-id="0ee55-168">Right-click on one of the instances.</span></span>
6. <span data-ttu-id="0ee55-169">選擇 [檢視 IntelliTrace 記錄檔] 。</span><span class="sxs-lookup"><span data-stu-id="0ee55-169">Choose **View IntelliTrace logs**.</span></span> <span data-ttu-id="0ee55-170">[IntelliTrace 摘要]  隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="0ee55-170">The **IntelliTrace Summary** will open.</span></span>
7. <span data-ttu-id="0ee55-171">找出摘要的例外狀況區段。</span><span class="sxs-lookup"><span data-stu-id="0ee55-171">Locate the exceptions section of the summary.</span></span> <span data-ttu-id="0ee55-172">如果有例外狀況，區段會標示 [例外狀況資料] 。</span><span class="sxs-lookup"><span data-stu-id="0ee55-172">If there are exceptions, the section will be labeled **Exception Data**.</span></span>
8. <span data-ttu-id="0ee55-173">展開 [例外狀況資料]，並尋找類似如下的 **System.IO.FileNotFoundException** 錯誤：</span><span class="sxs-lookup"><span data-stu-id="0ee55-173">Expand the **Exception Data** and look for **System.IO.FileNotFoundException** errors similar to the following:</span></span>

![例外狀況資料、遺失檔案或組件](./media/cloud-services-troubleshoot-roles-that-fail-start/ic503390.png)

## <a name="address-missing-dlls-and-assemblies"></a><span data-ttu-id="0ee55-175">解決遺失 Dll 和組件的問題</span><span class="sxs-lookup"><span data-stu-id="0ee55-175">Address missing DLLs and assemblies</span></span>
<span data-ttu-id="0ee55-176">若要解決遺失 DLL 和組件錯誤，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="0ee55-176">To address missing DLL and assembly errors, follow these steps:</span></span>

1. <span data-ttu-id="0ee55-177">在 Visual Studio 中開啟解決方案。</span><span class="sxs-lookup"><span data-stu-id="0ee55-177">Open the solution in Visual Studio.</span></span>
2. <span data-ttu-id="0ee55-178">在 [方案總管] 中，開啟 [參考] 資料夾。</span><span class="sxs-lookup"><span data-stu-id="0ee55-178">In **Solution Explorer**, open the **References** folder.</span></span>
3. <span data-ttu-id="0ee55-179">按一下錯誤中識別的組件。</span><span class="sxs-lookup"><span data-stu-id="0ee55-179">Click the assembly identified in the error.</span></span>
4. <span data-ttu-id="0ee55-180">在 [屬性] 窗格中找出 [複製本機] 屬性，並將值設為 **True**。</span><span class="sxs-lookup"><span data-stu-id="0ee55-180">In the **Properties** pane, locate **Copy Local property** and set the value to **True**.</span></span>
5. <span data-ttu-id="0ee55-181">重新部署雲端服務。</span><span class="sxs-lookup"><span data-stu-id="0ee55-181">Redeploy the cloud service.</span></span>

<span data-ttu-id="0ee55-182">在確認所有錯誤皆已修正後，即可在未勾選 [為 .NET 4 角色啟用 IntelliTrace]  核取方塊的情況下部署服務。</span><span class="sxs-lookup"><span data-stu-id="0ee55-182">Once you have verified that all errors have been corrected, you can deploy the service without checking the **Enable IntelliTrace for .NET 4 roles** check box.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0ee55-183">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0ee55-183">Next steps</span></span>
<span data-ttu-id="0ee55-184">檢視更多雲端服務的 [疑難排解文章](https://azure.microsoft.com/documentation/articles/?tag=top-support-issue&product=cloud-services) 。</span><span class="sxs-lookup"><span data-stu-id="0ee55-184">View more [troubleshooting articles](https://azure.microsoft.com/documentation/articles/?tag=top-support-issue&product=cloud-services) for cloud services.</span></span>

<span data-ttu-id="0ee55-185">若要了解如何利用 Azure PaaS 電腦診斷資料對雲端服務角色問題進行疑難排解，請參閱 [Kevin Williamson 的部落格系列](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx)。</span><span class="sxs-lookup"><span data-stu-id="0ee55-185">To learn how to troubleshoot cloud service role issues by using Azure PaaS computer diagnostics data, see [Kevin Williamson's blog series](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).</span></span>
