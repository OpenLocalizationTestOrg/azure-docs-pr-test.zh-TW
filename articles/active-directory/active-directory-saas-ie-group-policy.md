---
title: "aaaDeploy Azure 存取面板延伸模組使用 GPO 的 ie |Microsoft 文件"
description: "如何 toouse 群組原則 toodeploy hello Internet Explorer 附加元件 hello 我的應用程式入口網站。"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 7c2d49c8-5be0-4e7e-abac-332f9dfda736
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/02/2017
ms.author: markvi
ms.reviewer: asteen
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 926f15950bbe81d2fbfe1b0b856470da40880d7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodeploy-hello-access-panel-extension-for-internet-explorer-using-group-policy"></a>如何 tooDeploy hello Internet explorer 使用群組原則的存取面板延伸模組
本教學課程會示範如何 toouse 群組原則 tooremotely hello 存取面板延伸模組 Internet Explorer 的電腦上安裝您的使用者。 這項擴充功能都需要 Internet Explorer，使用者需要 toosign 到應用程式使用的設定[密碼型單一登入](active-directory-appssoaccess-whatis.md#password-based-single-sign-on)。

建議系統管理員自動化 hello 部署這項擴充功能。 否則，使用者有 toodownload 和 hello 延伸自行安裝，是很容易出錯的 toouser 錯誤，需要系統管理員權限。 本教學課程涵蓋使用群組原則自動化軟體部署的一種方法。 [深入了解群組原則。](https://technet.microsoft.com/windowsserver/bb310732.aspx)

hello 存取面板延伸模組也會提供如[Chrome](https://go.microsoft.com/fwLink/?LinkID=311859)和[Firefox](https://go.microsoft.com/fwLink/?LinkID=626998)，這兩者需要系統管理員權限 tooinstall。

## <a name="prerequisites"></a>必要條件
* 您已設定[Active Directory 網域服務](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx)，及您已加入您的使用者機器 tooyour 網域。
* 您必須擁有 hello [編輯設定] 的權限 tooedit hello 群組原則物件 (GPO)。 根據預設，hello 下列安全性群組的成員擁有此權限： 網域系統管理員、 企業系統管理員和 Group Policy Creator Owners。 [深入了解。](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx)

## <a name="step-1-create-hello-distribution-point"></a>步驟 1： 建立 hello 的發佈點
首先，您必須在網路位置上 hello 機器可存取您想 tooremotely 安裝 hello 擴充功能上放置 hello 安裝程式套件。 toodo，請遵循下列步驟：

1. 系統管理員身分登入 toohello 伺服器
2. 在 hello**伺服器管理員**視窗中，跳過**檔案和存放服務**。
   
    ![開啟檔案和存放服務](./media/active-directory-saas-ie-group-policy/files-services.png)
3. 移 toohello**共用** 索引標籤。然後按一下工作 > 新增共用...
   
    ![開啟檔案和存放服務](./media/active-directory-saas-ie-group-policy/shares.png)
4. 完整的 hello**新增共用精靈**和設定權限 tooensure，可以存取從使用者的機器。 [深入了解共用。](https://technet.microsoft.com/library/cc753175.aspx)
5. 下載下列 Microsoft Windows Installer 套件 （.msi 檔案） 的 hello:[存取面板 Extension.msi](https://account.activedirectory.windowsazure.com/Applications/Installers/x64/Access Panel Extension.msi)
6. 複製 hello installer 封裝 tooa 所需的 hello 共用上的位置。
   
    ![複製 hello.msi 檔案 toohello 共用。](./media/active-directory-saas-ie-group-policy/copy-package.png)
7. 請確認用戶端電腦會從 hello 共用可以 tooaccess hello 安裝程式套件。 

## <a name="step-2-create-hello-group-policy-object"></a>步驟 2： 建立 hello 群組原則物件
1. 裝載 Active Directory 網域服務 (AD DS) 安裝 toohello 伺服器上的記錄。
2. 在 hello 伺服器管理員中，移過**工具** > **群組原則管理**。
   
    ![移 tooTools > 群組原則管理](./media/active-directory-saas-ie-group-policy/tools-gpm.png)
3. Hello hello 左窗格中**群組原則管理**視窗中，檢視您的組織單位 (OU) 階層，並判斷在哪些範圍中，您想要 tooapply hello 群組原則。 比方說，您可能會決定 toopick 小型的 OU toodeploy tooa 少數使用者來進行測試，或您可能會選取最上層 OU toodeploy tooyour 整個組織。
   
   > [!NOTE]
   > 如果您想要 toocreate 或編輯您的組織單位 (Ou)，切換後 toohello 伺服器管理員，並跳過**工具** > **Active Directory 使用者和電腦**。
   > 
   > 
4. 一旦您選取 OU，以滑鼠右鍵按一下它然後選取 [在這個網域中建立 GPO 並連結到...]
   
    ![建立新的 GPO](./media/active-directory-saas-ie-group-policy/create-gpo.png)
5. 在 hello**新的 GPO**提示字元中，輸入名稱的 hello 新群組原則物件。
   
    ![名稱 hello 新的 GPO](./media/active-directory-saas-ie-group-policy/name-gpo.png)
6. 以滑鼠右鍵按一下 hello 建立，並選取 群組原則物件**編輯**。
   
    ![編輯 hello 新的 GPO](./media/active-directory-saas-ie-group-policy/edit-gpo.png)

## <a name="step-3-assign-hello-installation-package"></a>步驟 3： 指派 hello 安裝套件
1. 判斷您是否想要根據 toodeploy hello 延伸模組**電腦設定**或**使用者設定**。 當使用[電腦設定](https://technet.microsoft.com/library/cc736413%28v=ws.10%29.aspx)，無論哪個使用者登入 tooit hello 電腦上安裝 hello 擴充功能。 與[使用者設定](https://technet.microsoft.com/library/cc781953%28v=ws.10%29.aspx)，使用者擁有 hello 擴充功能安裝，無論哪一台電腦登入。
2. Hello hello 左窗格中**群組原則管理編輯器** 視窗中，移 tooeither 的 hello 下列的組態類型視您所選擇的資料夾路徑：
   
   * `Computer Configuration/Policies/Software Settings/`
   * `User Configuration/Policies/Software Settings/`
3. 以滑鼠右鍵按一下 [軟體安裝]，然後選取 [新增] > [套件...]
   
    ![建立新的軟體安裝套件](./media/active-directory-saas-ie-group-policy/new-package.png)
4. 包含從 hello 安裝程式套件移 toohello 共用的資料夾[步驟 1： 建立 hello 的發佈點](#step-1-create-the-distribution-point)，選取 hello.msi 檔案，然後按一下**開啟**。
   
   > [!IMPORTANT]
   > 如果 hello 共用位於相同的伺服器上，確認您要執行 hello 網路檔案的路徑，而不是 hello 本機檔案路徑存取 hello.msi。
   > 
   > 
   
    ![選取 hello 安裝套件 hello 共用資料夾中。](./media/active-directory-saas-ie-group-policy/select-package.png)
5. 在 hello**部署軟體**提示，請選取**指派**部署方法。 然後按一下 [確定] 。
   
    ![選取 [已指派]，然後按一下 [確定]。](./media/active-directory-saas-ie-group-policy/deployment-method.png)

hello 延伸模組現在是已部署的 toohello 您選取的 OU。 [深入了解群組原則軟體安裝。](https://technet.microsoft.com/library/cc738858%28v=ws.10%29.aspx)

## <a name="step-4-auto-enable-hello-extension-for-internet-explorer"></a>步驟 4： 自動啟用 hello Internet Explorer 擴充功能
此外 toorunning hello 安裝程式，Internet Explorer 的每一個延伸模組必須明確啟用才能使用。 遵循以下 tooenable 的 hello 步驟 hello 使用群組原則的存取面板延伸模組：

1. 在 [hello**群組原則管理編輯器**] 視窗中，移 tooeither 的下列的路徑，您在中的組態類型視選擇的 hello[步驟 3： 指派 hello 安裝套件](#step-3-assign-the-installation-package):
   
   * `Computer Configuration/Policies/Administrative Templates/Windows Components/Internet Explorer/Security Features/Add-on Management`
   * `User Configuration/Policies/Administrative Templates/Windows Components/Internet Explorer/Security Features/Add-on Management`
2. 以滑鼠右鍵按一下 [附加元件清單]，然後選取 [編輯]。
    ![編輯附加元件清單。](./media/active-directory-saas-ie-group-policy/edit-add-on-list.png)
3. 在 hello**附加元件清單**視窗中，選取**啟用**。 然後，在 hello**選項**區段中，按一下**顯示...**.
   
    ![按一下 [啟用]，然後按一下 [顯示...]](./media/active-directory-saas-ie-group-policy/edit-add-on-list-window.png)
4. 在 hello**顯示內容**視窗中，執行下列步驟的 hello:
   
   1. Hello 第一個資料行 (hello**值名稱**欄位)、 複製及貼上下列類別識別碼 hello:`{030E9A3F-7B18-4122-9A60-B87235E4F59E}`
   2. Hello 第二個資料行 (hello**值**欄位)，輸入下列值的 hello:`1`
   3. 按一下**確定**tooclose hello**顯示內容**視窗。
      
      ![填寫 hello 和上述所指定的值。](./media/active-directory-saas-ie-group-policy/show-contents.png)
5. 按一下**確定**tooapply 變更並關閉 hello**附加元件清單**視窗。

hello 擴充功能應該已啟用的 hello 機器 hello 選取 OU。 [進一步瞭解使用群組原則 tooenable 或停用 Internet Explorer 附加元件。](https://technet.microsoft.com/library/dn454941.aspx)

## <a name="step-5-optional-disable-remember-password-prompt"></a>步驟 5 (選用)：停用 [記住密碼] 提示
當使用者登入 toowebsites 使用 hello 存取面板延伸模組，Internet Explorer 可能會顯示 hello 下列提示詢問 「 您希望？ toostore 密碼 」

![](./media/active-directory-saas-ie-group-policy/remember-password-prompt.png)

如果您想 tooprevent 看到此提示使用者，然後依照 tooprevent 自動完成下列步驟來 hello 與記住的密碼：

1. 在 hello**群組原則管理編輯器**視窗中，移 toohello 下面所列的路徑。 這項組態設定僅提供於 [使用者設定]。
   
   * `User Configuration/Policies/Administrative Templates/Windows Components/Internet Explorer/`
2. 找出 hello 設定名為**開啟表單上的使用者名稱和密碼的 hello 自動完成功能**。
   
   > [!NOTE]
   > 舊版的 Active Directory 可能會列出這項設定使用 hello 名稱**不允許自動完成 toosave 密碼**。 hello 組態，該設定不同於 hello 設定本教學課程中所述。
   > 
   > 
   
    ![請記住這個 toolook 在使用者設定。](./media/active-directory-saas-ie-group-policy/disable-auto-complete.png)
3. 以滑鼠右鍵按一下 hello 上方設定，然後選取**編輯**。
4. 在標題為 hello 視窗**開啟表單上的使用者名稱和密碼的 hello 自動完成功能**，選取**已停用**。
   
    ![選取 [停用]](./media/active-directory-saas-ie-group-policy/disable-passwords.png)
5. 按一下**確定**tooapply 這些變更並關閉 hello 視窗。

使用者將不再是無法 toostore 其認證，或使用自動完成 tooaccess 預存認證。 不過，此原則允許使用者 toocontinue toouse 對於其他類型的表單欄位，例如搜尋欄位自動完成。

> [!WARNING]
> 如果使用者已選擇 toostore 某些認證之後，會啟用此原則，此原則將*不*清除已儲存的 hello 認證。
> 
> 

## <a name="step-6-testing-hello-deployment"></a>步驟 6： 測試部署的 hello
如果 hello 擴充部署成功，請遵循下方 tooverify hello 步驟：

1. 如果您使用部署**電腦設定**，登入用戶端電腦屬於您在選取的 OU toohello[步驟 2： 建立群組原則物件 hello](#step-2-create-the-group-policy-object)。 如果您使用部署**使用者設定**，請確定 toosign 中的所屬 toothat OU 使用者的身分。
2. 可能需要一些符號集 hello 群組原則的變更與此機器 toofully 更新。 tooforce hello 更新中，開啟**命令提示字元**視窗並執行下列命令的 hello:`gpupdate /force`
3. 您必須重新啟動 hello 機器 hello 安裝 tootake 地方。 開機可能需要相當多的時間比平常 hello 延伸模組時安裝。
4. 重新開機之後，開啟 **Internet Explorer**。 Hello hello 視窗的右上角，按一下**工具**（hello 齒輪圖示），然後選取**管理附加元件**。
   
    ![移 tooTools > 管理附加元件](./media/active-directory-saas-ie-group-policy/manage-add-ons.png)
5. 在 hello**管理附加元件**視窗中，確認該 hello**存取面板延伸模組**已安裝且其**狀態**已經過設定**已啟用**.
   
    ![確認 存取面板延伸模組已安裝並啟用該 hello。](./media/active-directory-saas-ie-group-policy/verify-install.png)

## <a name="related-articles"></a>相關文章
* [Article Index for Application Management in Azure Active Directory (Azure Active Directory 中應用程式管理的文件索引)](active-directory-apps-index.md)
* [搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)
* [疑難排解 hello Internet explorer 的 存取面板延伸模組](active-directory-saas-ie-troubleshooting.md)

