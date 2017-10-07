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
# <a name="troubleshooting-hello-access-panel-extension-for-internet-explorer"></a>疑難排解 hello Internet explorer 的 存取面板延伸模組
這篇文章可協助您疑難排解 hello 下列問題：

* 您正在使用 Internet Explorer 時無法 tooaccess 透過 hello 我的應用程式入口網站應用程式。
* 您會看到 「 安裝軟體 」 訊息，即使您已經安裝 hello 軟體 hello。

如果您是系統管理員，請參閱： [tooDeploy 如何使用群組原則 Internet Explorer 的 hello 存取面板延伸模組](active-directory-saas-ie-group-policy.md)

## <a name="run-hello-diagnostic-tool"></a>執行 hello 診斷工具
您可以藉由下載並執行 hello 存取面板診斷工具診斷 hello 存取面板延伸模組的安裝問題：

1. [按一下這裡 toodownload hello 診斷工具。](https://account.activedirectory.windowsazure.com/applications/AccessPanelExtensionDiagnosticTool/AccessPanelExtensionDiagnosticTool.zip)
2. 開啟 hello 檔案，並按**擷取所有** 按鈕。
   
    ![按下 [解壓縮全部]](./media/active-directory-saas-ie-troubleshooting/extract1.png)
3. 然後按 hello**擷取**按鈕 toocontinue。
   
    ![按下 [解壓縮]](./media/active-directory-saas-ie-troubleshooting/extract2.png)
4. toorun hello 工具，以滑鼠右鍵按一下名為 hello 檔案**AccessPanelExtensionDiagnosticTool**，然後選取**開啟 > Microsoft Windows 指令碼主機**。
   
    ![[開啟檔案] > [Microsoft Windows Based Script Host]](./media/active-directory-saas-ie-troubleshooting/open_tool.png)
5. 然後，您會看到下列描述可能有什麼錯誤與您的安裝中的診斷視窗 hello。
   
    ![樣本的 hello 診斷視窗](./media/active-directory-saas-ie-troubleshooting/tool_preview.png)
6. 按一下 「**是**"toolet hello 程式修正 hello 問題，找不到。
7. toosave 這些變更，關閉每個 Internet Explorer 視窗，然後再重新開啟 Internet Explorer。<br />如果仍然無法存取您的應用程式，請嘗試下列 hello 步驟。

## <a name="check-that-hello-access-panel-extension-is-enabled"></a>請檢查存取面板延伸模組已啟用該 hello
在 Internet Explorer 中啟用 hello 存取面板延伸模組的 tooverify:

1. 在 Internet Explorer 中，按一下 hello**齒輪圖示**hello 右上角的 hello 視窗。 然後選取 [網際網路選項]。<br />(在舊版 Internet Explorer 中可以在 [工具] > [網際網路選項] 下找到。
   
    ![移 tooTools > 網際網路選項](./media/active-directory-saas-ie-troubleshooting/internetoptions.png)
2. 按一下 hello**程式**索引標籤，然後按一下 [hello**管理附加元件**] 按鈕。
   
    ![按一下 [管理附加元件]](./media/active-directory-saas-ie-troubleshooting/internetoptions_programs.png)
3. 在這個對話方塊中，選取**存取面板延伸模組**然後按一下hello**啟用** 按鈕。
   
    ![按一下 [啟用]](./media/active-directory-saas-ie-troubleshooting/enableaddon.png)
4. toosave 這些變更，關閉所有 Internet Explorer 視窗，然後再開啟 Internet Explorer。

## <a name="enable-extensions-for-inprivate-browsing"></a>啟用 InPrivate 瀏覽的延伸模組
如果您使用 hello InPrivate 瀏覽模式：

1. 在 Internet Explorer 中，按一下 hello**齒輪圖示**hello 右上角的 hello 視窗。 然後選取 [網際網路選項]。<br />(在舊版 Internet Explorer 中可以在 [工具] > [網際網路選項] 下找到。
   
    ![樣本的 hello 診斷視窗](./media/active-directory-saas-ie-troubleshooting/inprivateoptions.png)
2. 移 toohello**隱私權**索引標籤，然後**取消核取**hello 核取方塊標示為**InPrivate 瀏覽開始時停用工具列和延伸模組**</p>
   
    ![取消核取 [InPrivate 瀏覽啟動時停用工具列和延伸模組]](./media/active-directory-saas-ie-troubleshooting/enabletoolbars.png)
3. toosave 這些變更，關閉所有 Internet Explorer 視窗，然後再開啟 Internet Explorer。

## <a name="uninstall-hello-access-panel-extension"></a>解除安裝 hello 存取面板延伸模組
toouninstall hello 存取面板延伸模組，從您的電腦：

1. 在鍵盤上按 hello **Windows 鍵**tooopen hello 開始 功能表。 Hello 功能表開啟時，您可以輸入任何項目 toodo 搜尋。 輸入 控制台，然後開啟 hello**控制台**hello 搜尋結果中出現。
   
    ![搜尋「控制台」](./media/active-directory-saas-ie-troubleshooting/search_sm.png)
2. 在 hello 右上角的 hello 控制台中，變更 hello**檢視**太選項**大圖示**。 然後，尋找並按一下 hello**程式和功能** 按鈕。
   
    ![變更 hello 檢視 tooshow 大圖示](./media/active-directory-saas-ie-troubleshooting/control_panel.png)
3. 從 [hello] 清單中，選取 [**存取面板延伸模組**，並按一下 hello hello**解除安裝**] 按鈕。
   
    ![按一下 [解除安裝]](./media/active-directory-saas-ie-troubleshooting/uninstall.png)
4. 然後，您可以嘗試 tooinstall hello 延伸一次 toosee 如果 hello 問題已經解決。

如果您遇到 hello 延伸模組正在解除安裝的問題，您也可以移除它使用 hello [Microsoft 修正它](https://go.microsoft.com/?linkid=9779673)工具。

## <a name="related-articles"></a>相關文章
* [Article Index for Application Management in Azure Active Directory (Azure Active Directory 中應用程式管理的文件索引)](active-directory-apps-index.md)
* [搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)
* [如何 tooDeploy hello Internet explorer 使用群組原則的存取面板延伸模組](active-directory-saas-ie-group-policy.md)

