---
title: "aaaTroubleshooting hello Azure 存取面板延伸模組，ie |Microsoft 文件"
description: "如何 toouse 群組原則 toodeploy hello Internet Explorer 附加元件 hello 我的應用程式入口網站。"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: f56b3230-26fd-42ec-9e3d-2c12daf15479
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/02/2017
ms.author: markvi
ms.reviewer: asteen
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 23cbb6117f34759330206de3a26f1397486acedb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-hello-access-panel-extension-for-internet-explorer"></a><span data-ttu-id="d2340-103">疑難排解 hello Internet explorer 的 存取面板延伸模組</span><span class="sxs-lookup"><span data-stu-id="d2340-103">Troubleshooting hello Access Panel Extension for Internet Explorer</span></span>
<span data-ttu-id="d2340-104">這篇文章可協助您疑難排解 hello 下列問題：</span><span class="sxs-lookup"><span data-stu-id="d2340-104">This article helps you troubleshoot hello following problems:</span></span>

* <span data-ttu-id="d2340-105">您正在使用 Internet Explorer 時無法 tooaccess 透過 hello 我的應用程式入口網站應用程式。</span><span class="sxs-lookup"><span data-stu-id="d2340-105">You're unable tooaccess your apps through hello My Apps portal while using Internet Explorer.</span></span>
* <span data-ttu-id="d2340-106">您會看到 「 安裝軟體 」 訊息，即使您已經安裝 hello 軟體 hello。</span><span class="sxs-lookup"><span data-stu-id="d2340-106">You see hello "Install Software" message even though you've already installed hello software.</span></span>

<span data-ttu-id="d2340-107">如果您是系統管理員，請參閱： [tooDeploy 如何使用群組原則 Internet Explorer 的 hello 存取面板延伸模組](active-directory-saas-ie-group-policy.md)</span><span class="sxs-lookup"><span data-stu-id="d2340-107">If you are an admin, see also: [How tooDeploy hello Access Panel Extension for Internet Explorer using Group Policy](active-directory-saas-ie-group-policy.md)</span></span>

## <a name="run-hello-diagnostic-tool"></a><span data-ttu-id="d2340-108">執行 hello 診斷工具</span><span class="sxs-lookup"><span data-stu-id="d2340-108">Run hello Diagnostic Tool</span></span>
<span data-ttu-id="d2340-109">您可以藉由下載並執行 hello 存取面板診斷工具診斷 hello 存取面板延伸模組的安裝問題：</span><span class="sxs-lookup"><span data-stu-id="d2340-109">You can diagnose installation problems with hello Access Panel Extension by downloading and running hello Access Panel diagnostic tool:</span></span>

1. [<span data-ttu-id="d2340-110">按一下這裡 toodownload hello 診斷工具。</span><span class="sxs-lookup"><span data-stu-id="d2340-110">Click here toodownload hello diagnostic tool.</span></span>](https://account.activedirectory.windowsazure.com/applications/AccessPanelExtensionDiagnosticTool/AccessPanelExtensionDiagnosticTool.zip)
2. <span data-ttu-id="d2340-111">開啟 hello 檔案，並按**擷取所有** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="d2340-111">Open hello file, and press **Extract all** button.</span></span>
   
    ![按下 [解壓縮全部]](./media/active-directory-saas-ie-troubleshooting/extract1.png)
3. <span data-ttu-id="d2340-113">然後按 hello**擷取**按鈕 toocontinue。</span><span class="sxs-lookup"><span data-stu-id="d2340-113">Then press hello **Extract** button toocontinue.</span></span>
   
    ![按下 [解壓縮]](./media/active-directory-saas-ie-troubleshooting/extract2.png)
4. <span data-ttu-id="d2340-115">toorun hello 工具，以滑鼠右鍵按一下名為 hello 檔案**AccessPanelExtensionDiagnosticTool**，然後選取**開啟 > Microsoft Windows 指令碼主機**。</span><span class="sxs-lookup"><span data-stu-id="d2340-115">toorun hello tool, right-click hello file named **AccessPanelExtensionDiagnosticTool**, then select **Open with > Microsoft Windows Based Script Host**.</span></span>
   
    ![[開啟檔案] > [Microsoft Windows Based Script Host]](./media/active-directory-saas-ie-troubleshooting/open_tool.png)
5. <span data-ttu-id="d2340-117">然後，您會看到下列描述可能有什麼錯誤與您的安裝中的診斷視窗 hello。</span><span class="sxs-lookup"><span data-stu-id="d2340-117">You will then see hello following diagnostic window, which describes what might be wrong with your installation.</span></span>
   
    ![樣本的 hello 診斷視窗](./media/active-directory-saas-ie-troubleshooting/tool_preview.png)
6. <span data-ttu-id="d2340-119">按一下 「**是**"toolet hello 程式修正 hello 問題，找不到。</span><span class="sxs-lookup"><span data-stu-id="d2340-119">Click "**YES**" toolet hello program fix hello issues that have been found.</span></span>
7. <span data-ttu-id="d2340-120">toosave 這些變更，關閉每個 Internet Explorer 視窗，然後再重新開啟 Internet Explorer。</span><span class="sxs-lookup"><span data-stu-id="d2340-120">toosave these changes, close every Internet Explorer window, and then open Internet Explorer again.</span></span><br /><span data-ttu-id="d2340-121">如果仍然無法存取您的應用程式，請嘗試下列 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="d2340-121">If you still can't access your apps, try hello steps below.</span></span>

## <a name="check-that-hello-access-panel-extension-is-enabled"></a><span data-ttu-id="d2340-122">請檢查存取面板延伸模組已啟用該 hello</span><span class="sxs-lookup"><span data-stu-id="d2340-122">Check that hello Access Panel Extension is enabled</span></span>
<span data-ttu-id="d2340-123">在 Internet Explorer 中啟用 hello 存取面板延伸模組的 tooverify:</span><span class="sxs-lookup"><span data-stu-id="d2340-123">tooverify that hello Access Panel Extension is enabled in Internet Explorer:</span></span>

1. <span data-ttu-id="d2340-124">在 Internet Explorer 中，按一下 hello**齒輪圖示**hello 右上角的 hello 視窗。</span><span class="sxs-lookup"><span data-stu-id="d2340-124">In Internet Explorer, click hello **Gear icon** on hello top right corner of hello window.</span></span> <span data-ttu-id="d2340-125">然後選取 [網際網路選項]。</span><span class="sxs-lookup"><span data-stu-id="d2340-125">Then select **Internet options**.</span></span><br /><span data-ttu-id="d2340-126">(在舊版 Internet Explorer 中可以在 [工具] > [網際網路選項] 下找到。</span><span class="sxs-lookup"><span data-stu-id="d2340-126">(In older versions of Internet Explorer you can find this under **Tools > Internet options**.</span></span>
   
    ![移 tooTools > 網際網路選項](./media/active-directory-saas-ie-troubleshooting/internetoptions.png)
2. <span data-ttu-id="d2340-128">按一下 hello**程式**索引標籤，然後按一下 [hello**管理附加元件**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="d2340-128">Click hello **Programs** tab, then click hello **Manage add-ons** button.</span></span>
   
    ![按一下 [管理附加元件]](./media/active-directory-saas-ie-troubleshooting/internetoptions_programs.png)
3. <span data-ttu-id="d2340-130">在這個對話方塊中，選取**存取面板延伸模組**然後按一下hello**啟用** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="d2340-130">In this dialog, select **Access Panel Extension** and then click hello **Enable** button.</span></span>
   
    ![按一下 [啟用]](./media/active-directory-saas-ie-troubleshooting/enableaddon.png)
4. <span data-ttu-id="d2340-132">toosave 這些變更，關閉所有 Internet Explorer 視窗，然後再開啟 Internet Explorer。</span><span class="sxs-lookup"><span data-stu-id="d2340-132">toosave these changes, close every Internet Explorer window and then open Internet Explorer again.</span></span>

## <a name="enable-extensions-for-inprivate-browsing"></a><span data-ttu-id="d2340-133">啟用 InPrivate 瀏覽的延伸模組</span><span class="sxs-lookup"><span data-stu-id="d2340-133">Enable Extensions for InPrivate Browsing</span></span>
<span data-ttu-id="d2340-134">如果您使用 hello InPrivate 瀏覽模式：</span><span class="sxs-lookup"><span data-stu-id="d2340-134">If you are using hello InPrivate Browsing mode:</span></span>

1. <span data-ttu-id="d2340-135">在 Internet Explorer 中，按一下 hello**齒輪圖示**hello 右上角的 hello 視窗。</span><span class="sxs-lookup"><span data-stu-id="d2340-135">In Internet Explorer, click hello **Gear icon** on hello top right corner of hello window.</span></span> <span data-ttu-id="d2340-136">然後選取 [網際網路選項]。</span><span class="sxs-lookup"><span data-stu-id="d2340-136">Then select **Internet options**.</span></span><br /><span data-ttu-id="d2340-137">(在舊版 Internet Explorer 中可以在 [工具] > [網際網路選項] 下找到。</span><span class="sxs-lookup"><span data-stu-id="d2340-137">(In older versions of Internet Explorer you can find this under **Tools > Internet options**.</span></span>
   
    ![樣本的 hello 診斷視窗](./media/active-directory-saas-ie-troubleshooting/inprivateoptions.png)
2. <span data-ttu-id="d2340-139">移 toohello**隱私權**索引標籤，然後**取消核取**hello 核取方塊標示為**InPrivate 瀏覽開始時停用工具列和延伸模組**</span><span class="sxs-lookup"><span data-stu-id="d2340-139">Go toohello **Privacy** tab, then **uncheck** hello checkbox labeled **Disable toolbars and extensions when InPrivate Browsing starts**</span></span></p>
   
    ![取消核取 [InPrivate 瀏覽啟動時停用工具列和延伸模組]](./media/active-directory-saas-ie-troubleshooting/enabletoolbars.png)
3. <span data-ttu-id="d2340-141">toosave 這些變更，關閉所有 Internet Explorer 視窗，然後再開啟 Internet Explorer。</span><span class="sxs-lookup"><span data-stu-id="d2340-141">toosave these changes, close every Internet Explorer window and then open Internet Explorer again.</span></span>

## <a name="uninstall-hello-access-panel-extension"></a><span data-ttu-id="d2340-142">解除安裝 hello 存取面板延伸模組</span><span class="sxs-lookup"><span data-stu-id="d2340-142">Uninstall hello Access Panel Extension</span></span>
<span data-ttu-id="d2340-143">toouninstall hello 存取面板延伸模組，從您的電腦：</span><span class="sxs-lookup"><span data-stu-id="d2340-143">toouninstall hello Access Panel extension from your computer:</span></span>

1. <span data-ttu-id="d2340-144">在鍵盤上按 hello **Windows 鍵**tooopen hello 開始 功能表。</span><span class="sxs-lookup"><span data-stu-id="d2340-144">On your keyboard, press hello **Windows key** tooopen hello Start menu.</span></span> <span data-ttu-id="d2340-145">Hello 功能表開啟時，您可以輸入任何項目 toodo 搜尋。</span><span class="sxs-lookup"><span data-stu-id="d2340-145">When hello menu is open, you can type anything toodo a search.</span></span> <span data-ttu-id="d2340-146">輸入 控制台，然後開啟 hello**控制台**hello 搜尋結果中出現。</span><span class="sxs-lookup"><span data-stu-id="d2340-146">Type "Control Panel" and then open hello **Control Panel** when it appears in hello search results.</span></span>
   
    ![搜尋「控制台」](./media/active-directory-saas-ie-troubleshooting/search_sm.png)
2. <span data-ttu-id="d2340-148">在 hello 右上角的 hello 控制台中，變更 hello**檢視**太選項**大圖示**。</span><span class="sxs-lookup"><span data-stu-id="d2340-148">In hello top right corner of hello Control Panel, change hello **View by** option too**Large icons**.</span></span> <span data-ttu-id="d2340-149">然後，尋找並按一下 hello**程式和功能** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="d2340-149">Then find and click hello **Programs and Features** button.</span></span>
   
    ![變更 hello 檢視 tooshow 大圖示](./media/active-directory-saas-ie-troubleshooting/control_panel.png)
3. <span data-ttu-id="d2340-151">從 [hello] 清單中，選取 [**存取面板延伸模組**，並按一下 hello hello**解除安裝**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="d2340-151">From hello list, select **Access Panel Extension**, and hello click hello **Uninstall** button.</span></span>
   
    ![按一下 [解除安裝]](./media/active-directory-saas-ie-troubleshooting/uninstall.png)
4. <span data-ttu-id="d2340-153">然後，您可以嘗試 tooinstall hello 延伸一次 toosee 如果 hello 問題已經解決。</span><span class="sxs-lookup"><span data-stu-id="d2340-153">You can then try tooinstall hello extension again toosee if hello problem has been resolved.</span></span>

<span data-ttu-id="d2340-154">如果您遇到 hello 延伸模組正在解除安裝的問題，您也可以移除它使用 hello [Microsoft 修正它](https://go.microsoft.com/?linkid=9779673)工具。</span><span class="sxs-lookup"><span data-stu-id="d2340-154">If you encounter issues uninstalling hello extension, you can also remove it using hello [Microsoft Fix It](https://go.microsoft.com/?linkid=9779673) tool.</span></span>

## <a name="related-articles"></a><span data-ttu-id="d2340-155">相關文章</span><span class="sxs-lookup"><span data-stu-id="d2340-155">Related Articles</span></span>
* [<span data-ttu-id="d2340-156">Article Index for Application Management in Azure Active Directory (Azure Active Directory 中應用程式管理的文件索引)</span><span class="sxs-lookup"><span data-stu-id="d2340-156">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="d2340-157">搭配 Azure Active Directory 的應用程式存取和單一登入</span><span class="sxs-lookup"><span data-stu-id="d2340-157">Application access and single sign-on with Azure Active Directory</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="d2340-158">如何 tooDeploy hello Internet explorer 使用群組原則的存取面板延伸模組</span><span class="sxs-lookup"><span data-stu-id="d2340-158">How tooDeploy hello Access Panel Extension for Internet Explorer using Group Policy</span></span>](active-directory-saas-ie-group-policy.md)

