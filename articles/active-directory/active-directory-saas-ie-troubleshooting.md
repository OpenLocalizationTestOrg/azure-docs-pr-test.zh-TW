---
title: "針對適用於 IE 的 Azure 存取面板延伸模組進行疑難排解 | Microsoft Docs"
description: "如何使用群組原則針對我的 app 入口網站部署 Internet Explorer 附加元件。"
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
ms.openlocfilehash: 938d0b4046afa8c80eabe542f4541d0554948f5d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="troubleshooting-the-access-panel-extension-for-internet-explorer"></a><span data-ttu-id="f8479-103">疑難排解 Internet explorer 的存取面板延伸模組</span><span class="sxs-lookup"><span data-stu-id="f8479-103">Troubleshooting the Access Panel Extension for Internet Explorer</span></span>
<span data-ttu-id="f8479-104">這篇文章可協助您疑難排解下列問題：</span><span class="sxs-lookup"><span data-stu-id="f8479-104">This article helps you troubleshoot the following problems:</span></span>

* <span data-ttu-id="f8479-105">使用 Internet Explorer 時無法透過「我的 app」入口網站存取您的 app。</span><span class="sxs-lookup"><span data-stu-id="f8479-105">You're unable to access your apps through the My Apps portal while using Internet Explorer.</span></span>
* <span data-ttu-id="f8479-106">即使您已經安裝軟體，還是看到「安裝軟體」訊息。</span><span class="sxs-lookup"><span data-stu-id="f8479-106">You see the "Install Software" message even though you've already installed the software.</span></span>

<span data-ttu-id="f8479-107">如果您是管理員，另請參閱： [如何使用群組原則部署 Internet Explorer 的存取面板延伸模組](active-directory-saas-ie-group-policy.md)</span><span class="sxs-lookup"><span data-stu-id="f8479-107">If you are an admin, see also: [How to Deploy the Access Panel Extension for Internet Explorer using Group Policy](active-directory-saas-ie-group-policy.md)</span></span>

## <a name="run-the-diagnostic-tool"></a><span data-ttu-id="f8479-108">執行診斷工具</span><span class="sxs-lookup"><span data-stu-id="f8479-108">Run the Diagnostic Tool</span></span>
<span data-ttu-id="f8479-109">您可以下載並執行「存取面板」診斷工具來診斷存取面板延伸模組的安裝問題：</span><span class="sxs-lookup"><span data-stu-id="f8479-109">You can diagnose installation problems with the Access Panel Extension by downloading and running the Access Panel diagnostic tool:</span></span>

1. [<span data-ttu-id="f8479-110">按一下這裡下載診斷工具。</span><span class="sxs-lookup"><span data-stu-id="f8479-110">Click here to download the diagnostic tool.</span></span>](https://account.activedirectory.windowsazure.com/applications/AccessPanelExtensionDiagnosticTool/AccessPanelExtensionDiagnosticTool.zip)
2. <span data-ttu-id="f8479-111">開啟檔案，然後按下 [解壓縮全部]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="f8479-111">Open the file, and press **Extract all** button.</span></span>
   
    ![按下 [解壓縮全部]](./media/active-directory-saas-ie-troubleshooting/extract1.png)
3. <span data-ttu-id="f8479-113">然後按下 [解壓縮]  按鈕繼續。</span><span class="sxs-lookup"><span data-stu-id="f8479-113">Then press the **Extract** button to continue.</span></span>
   
    ![按下 [解壓縮]](./media/active-directory-saas-ie-troubleshooting/extract2.png)
4. <span data-ttu-id="f8479-115">若要執行工具，請以滑鼠右鍵按一下名為 **AccessPanelExtensionDiagnosticTool** 的檔案，然後選取 [開啟檔案] > [Microsoft Windows Based Script Host]。</span><span class="sxs-lookup"><span data-stu-id="f8479-115">To run the tool, right-click the file named **AccessPanelExtensionDiagnosticTool**, then select **Open with > Microsoft Windows Based Script Host**.</span></span>
   
    ![[開啟檔案] > [Microsoft Windows Based Script Host]](./media/active-directory-saas-ie-troubleshooting/open_tool.png)
5. <span data-ttu-id="f8479-117">然後您會看到下列診斷視窗，描述您的安裝可能有哪些錯誤。</span><span class="sxs-lookup"><span data-stu-id="f8479-117">You will then see the following diagnostic window, which describes what might be wrong with your installation.</span></span>
   
    ![一個診斷視窗範例](./media/active-directory-saas-ie-troubleshooting/tool_preview.png)
6. <span data-ttu-id="f8479-119">按一下 [是]讓程式修正發現的問題。</span><span class="sxs-lookup"><span data-stu-id="f8479-119">Click "**YES**" to let the program fix the issues that have been found.</span></span>
7. <span data-ttu-id="f8479-120">若要儲存這些變更，請關閉所有 Internet Explorer 視窗，然後再次開啟 Internet Explorer。</span><span class="sxs-lookup"><span data-stu-id="f8479-120">To save these changes, close every Internet Explorer window, and then open Internet Explorer again.</span></span><br /><span data-ttu-id="f8479-121">如果您仍然無法存取您的應用程式，請嘗試下列步驟。</span><span class="sxs-lookup"><span data-stu-id="f8479-121">If you still can't access your apps, try the steps below.</span></span>

## <a name="check-that-the-access-panel-extension-is-enabled"></a><span data-ttu-id="f8479-122">檢查存取面板延伸模組是否已啟用</span><span class="sxs-lookup"><span data-stu-id="f8479-122">Check that the Access Panel Extension is enabled</span></span>
<span data-ttu-id="f8479-123">確認 Internet Explorer 中已啟用存取面板延伸模組：</span><span class="sxs-lookup"><span data-stu-id="f8479-123">To verify that the Access Panel Extension is enabled in Internet Explorer:</span></span>

1. <span data-ttu-id="f8479-124">在 Internet Explorer 中按一下視窗右上角的「齒輪」圖示。</span><span class="sxs-lookup"><span data-stu-id="f8479-124">In Internet Explorer, click the **Gear icon** on the top right corner of the window.</span></span> <span data-ttu-id="f8479-125">然後選取 [網際網路選項]。</span><span class="sxs-lookup"><span data-stu-id="f8479-125">Then select **Internet options**.</span></span><br /><span data-ttu-id="f8479-126">(在舊版 Internet Explorer 中可以在 [工具] > [網際網路選項] 下找到。</span><span class="sxs-lookup"><span data-stu-id="f8479-126">(In older versions of Internet Explorer you can find this under **Tools > Internet options**.</span></span>
   
    ![移至 [工具] > [網際網路選項]](./media/active-directory-saas-ie-troubleshooting/internetoptions.png)
2. <span data-ttu-id="f8479-128">按一下 [程式] 索引標籤，然後按一下 [管理附加元件] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="f8479-128">Click the **Programs** tab, then click the **Manage add-ons** button.</span></span>
   
    ![按一下 [管理附加元件]](./media/active-directory-saas-ie-troubleshooting/internetoptions_programs.png)
3. <span data-ttu-id="f8479-130">在此對話方塊中，選取 [存取面板延伸模組]，然後按一下 [啟用] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="f8479-130">In this dialog, select **Access Panel Extension** and then click the **Enable** button.</span></span>
   
    ![按一下 [啟用]](./media/active-directory-saas-ie-troubleshooting/enableaddon.png)
4. <span data-ttu-id="f8479-132">若要儲存這些變更，請關閉所有 Internet Explorer 視窗，然後再次開啟 Internet Explorer。</span><span class="sxs-lookup"><span data-stu-id="f8479-132">To save these changes, close every Internet Explorer window and then open Internet Explorer again.</span></span>

## <a name="enable-extensions-for-inprivate-browsing"></a><span data-ttu-id="f8479-133">啟用 InPrivate 瀏覽的延伸模組</span><span class="sxs-lookup"><span data-stu-id="f8479-133">Enable Extensions for InPrivate Browsing</span></span>
<span data-ttu-id="f8479-134">如果您正在使用 InPrivate 瀏覽模式：</span><span class="sxs-lookup"><span data-stu-id="f8479-134">If you are using the InPrivate Browsing mode:</span></span>

1. <span data-ttu-id="f8479-135">在 Internet Explorer 中按一下視窗右上角的「齒輪」圖示。</span><span class="sxs-lookup"><span data-stu-id="f8479-135">In Internet Explorer, click the **Gear icon** on the top right corner of the window.</span></span> <span data-ttu-id="f8479-136">然後選取 [網際網路選項]。</span><span class="sxs-lookup"><span data-stu-id="f8479-136">Then select **Internet options**.</span></span><br /><span data-ttu-id="f8479-137">(在舊版 Internet Explorer 中可以在 [工具] > [網際網路選項] 下找到。</span><span class="sxs-lookup"><span data-stu-id="f8479-137">(In older versions of Internet Explorer you can find this under **Tools > Internet options**.</span></span>
   
    ![一個診斷視窗範例](./media/active-directory-saas-ie-troubleshooting/inprivateoptions.png)
2. <span data-ttu-id="f8479-139">移至 [隱私權] 索引標籤，然後**取消核取**標示為 [InPrivate 瀏覽啟動時停用工具列和延伸模組] 的核取方塊</span><span class="sxs-lookup"><span data-stu-id="f8479-139">Go to the **Privacy** tab, then **uncheck** the checkbox labeled **Disable toolbars and extensions when InPrivate Browsing starts**</span></span></p>
   
    ![取消核取 [InPrivate 瀏覽啟動時停用工具列和延伸模組]](./media/active-directory-saas-ie-troubleshooting/enabletoolbars.png)
3. <span data-ttu-id="f8479-141">若要儲存這些變更，請關閉所有 Internet Explorer 視窗，然後再次開啟 Internet Explorer。</span><span class="sxs-lookup"><span data-stu-id="f8479-141">To save these changes, close every Internet Explorer window and then open Internet Explorer again.</span></span>

## <a name="uninstall-the-access-panel-extension"></a><span data-ttu-id="f8479-142">解除安裝存取面板延伸模組</span><span class="sxs-lookup"><span data-stu-id="f8479-142">Uninstall the Access Panel Extension</span></span>
<span data-ttu-id="f8479-143">從您的電腦解除安裝存取面板延伸模組：</span><span class="sxs-lookup"><span data-stu-id="f8479-143">To uninstall the Access Panel extension from your computer:</span></span>

1. <span data-ttu-id="f8479-144">在鍵盤上按下 **Windows 鍵** 以開啟 [開始] 功能表。</span><span class="sxs-lookup"><span data-stu-id="f8479-144">On your keyboard, press the **Windows key** to open the Start menu.</span></span> <span data-ttu-id="f8479-145">功能表開啟時，您可以輸入任何內容進行搜尋。</span><span class="sxs-lookup"><span data-stu-id="f8479-145">When the menu is open, you can type anything to do a search.</span></span> <span data-ttu-id="f8479-146">請輸入「控制台」，然後當控制台  出現在搜尋結果中時將它開啟。</span><span class="sxs-lookup"><span data-stu-id="f8479-146">Type "Control Panel" and then open the **Control Panel** when it appears in the search results.</span></span>
   
    ![搜尋「控制台」](./media/active-directory-saas-ie-troubleshooting/search_sm.png)
2. <span data-ttu-id="f8479-148">在控制台的右上角，將 [檢視方式] 選項變更為 [大圖示]。</span><span class="sxs-lookup"><span data-stu-id="f8479-148">In the top right corner of the Control Panel, change the **View by** option to **Large icons**.</span></span> <span data-ttu-id="f8479-149">然後尋找 [程式和功能] 按鈕並按一下。</span><span class="sxs-lookup"><span data-stu-id="f8479-149">Then find and click the **Programs and Features** button.</span></span>
   
    ![變更檢視以顯示大圖示](./media/active-directory-saas-ie-troubleshooting/control_panel.png)
3. <span data-ttu-id="f8479-151">從清單中選取 [存取面板延伸模組]，再按一下 [解除安裝] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="f8479-151">From the list, select **Access Panel Extension**, and the click the **Uninstall** button.</span></span>
   
    ![按一下 [解除安裝]](./media/active-directory-saas-ie-troubleshooting/uninstall.png)
4. <span data-ttu-id="f8479-153">您可以嘗試再安裝一次延伸模組，看看是否已經解決問題。</span><span class="sxs-lookup"><span data-stu-id="f8479-153">You can then try to install the extension again to see if the problem has been resolved.</span></span>

<span data-ttu-id="f8479-154">如果您解除安裝延伸模組時遇到問題，也可以使用 [Microsoft Fix It](https://go.microsoft.com/?linkid=9779673) 工具移除延伸模組。</span><span class="sxs-lookup"><span data-stu-id="f8479-154">If you encounter issues uninstalling the extension, you can also remove it using the [Microsoft Fix It](https://go.microsoft.com/?linkid=9779673) tool.</span></span>

## <a name="related-articles"></a><span data-ttu-id="f8479-155">相關文章</span><span class="sxs-lookup"><span data-stu-id="f8479-155">Related Articles</span></span>
* [<span data-ttu-id="f8479-156">Article Index for Application Management in Azure Active Directory (Azure Active Directory 中應用程式管理的文件索引)</span><span class="sxs-lookup"><span data-stu-id="f8479-156">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="f8479-157">搭配 Azure Active Directory 的應用程式存取和單一登入</span><span class="sxs-lookup"><span data-stu-id="f8479-157">Application access and single sign-on with Azure Active Directory</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="f8479-158">如何使用群組原則部署 Internet Explorer 的存取面板擴充功能</span><span class="sxs-lookup"><span data-stu-id="f8479-158">How to Deploy the Access Panel Extension for Internet Explorer using Group Policy</span></span>](active-directory-saas-ie-group-policy.md)

