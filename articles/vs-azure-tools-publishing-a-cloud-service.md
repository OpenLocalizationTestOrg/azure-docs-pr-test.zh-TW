---
title: "雲端服務使用 hello Azure Tools aaaPublishing |Microsoft 文件"
description: "深入了解 toopublish Azure 雲端服務專案所使用的 Visual Studio 的方式。"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 1a07b6e4-3678-4cbf-b37e-4520b402a3d9
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 8/14/2017
ms.author: kraigb
ms.openlocfilehash: 31ede8308146de2bb128b768f23f64eb85bc7548
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="publishing-a-cloud-service-using-hello-azure-tools"></a>發行雲端服務使用 hello Azure Tools
使用 hello Azure Tools for Microsoft Visual Studio，您可以發行 Azure 應用程式直接從 Visual Studio。 Visual Studio 支援整合發行 tooeither hello 臨時或 hello 的雲端服務的實際執行環境。

您必須具有 Azure 訂用帳戶才可以發佈 Azure 應用程式。 您也必須設定雲端服務和儲存體帳戶 toobe 應用程式使用。 您可以設定這些在 hello [Azure 傳統入口網站](http://go.microsoft.com/fwlink/?LinkID=213885)。

> [!IMPORTANT]
> 當您發行時，您可以選取 hello 部署環境的雲端服務。 您也必須選取是使用的 toostore hello 應用程式封裝部署的儲存體帳戶。 部署之後，hello 應用程式封裝會移除從 hello 儲存體帳戶。
> 
> 

當您開發和測試 Azure 應用程式時，您可以為 web 角色以累加方式使用 Web Deploy toopublish 變更。 發行您的應用程式 tooa 部署環境之後，Web Deploy 可讓您直接 toohello 虛擬機器執行 hello web 角色部署的變更。 您沒有 toopackage，且發行整個 Azure 應用程式每次想 tooupdate hello 變更您 web 角色 tootest。 透過這種方式中的測試，而不等候 toohave 應用程式發行的 tooa 部署環境的 hello 雲端可以有您 web 角色的變更。

使用下列程序 toopublish hello 您的 Azure 應用程式和 web 角色 tooupdate 利用 Web 部署：

* 從 Visual Studio 發佈或封裝 Azure 應用程式
* 更新 web 角色一部分 hello 開發和測試週期

## <a name="publish-or-package-an-azure-application-from-visual-studio"></a>從 Visual Studio 發佈或封裝 Azure 應用程式
當您發行 Azure 應用程式時，您可以執行下列工作的 hello 的其中一個：

* 建立服務封裝： 您可以使用這個封裝和 hello 服務組態檔 toopublish 應用程式 tooa 部署環境的 hello [Azure 傳統入口網站](http://go.microsoft.com/fwlink/?LinkID=213885)。
* 發行 Azure 專案從 Visual Studio: toopublish 您的應用程式直接使用 tooAzure，hello 發行精靈。 如需相關資訊，請參閱 [發佈 Azure 應用程式精靈](vs-azure-tools-publish-azure-application-wizard.md)。

### <a name="toocreate-a-service-package-from-visual-studio"></a>toocreate 從 Visual Studio 服務套件
1. 當您準備好 toopublish 應用程式時，就會開啟 方案總管 中，開啟 hello hello 包含您的角色的 Azure 專案的捷徑功能表，然後選擇 發行。
2. toocreate 服務封裝，請遵循下列步驟：  
   
   1. Hello 快顯功能表上的 hello Azure 專案，選擇**封裝**。
   2. 在 hello**封裝 Azure 應用程式**對話方塊中，選擇要 toocreate hello 服務組態封裝，然後選擇 hello 組建組態。
   3. （選擇性） tooturn 遠端桌面 hello 雲端服務在發行後，選取 hello**啟用所有角色的遠端桌面**核取方塊，然後再選取**設定**tooconfigure 遠端桌面。 如果您想 toodebug 您的雲端服務在發行後，開啟遠端偵錯選取**啟用遠端偵錯工具的所有角色**。
      
      如需詳細資訊，請參閱 [搭配使用遠端桌面與 Azure 角色](vs-azure-tools-remote-desktop-roles.md)。
   4. toocreate hello 封裝中，選擇 hello**封裝**連結。
      
      檔案總管 中顯示新建立的套件 hello hello 檔案位置。 您可以複製此位置，好讓您可以使用它從 hello [Azure 傳統入口網站](http://go.microsoft.com/fwlink/?LinkID=213885)。
   5. toopublish 此封裝 tooa 部署環境中，您必須使用這個位置，因為當您建立雲端服務和部署此封裝 tooan 環境以 hello hello 封裝位置[Azure 傳統入口網站](http://go.microsoft.com/fwlink/?LinkID=213885)。
3. （選擇性） toocancel hello 部署程序，hello hello 活動記錄檔中的 hello 明細項目捷徑功能表上選擇**取消並移除**。 這會停止 hello 部署程序，並從 Azure 刪除 hello 部署環境。
   
   > [!NOTE]
   > tooremove 之後這個部署環境已部署，您必須使用 hello [Azure 傳統入口網站](http://go.microsoft.com/fwlink/?LinkID=213885)。
   > 
   > 
4. （選擇性）Visual Studio 啟動角色執行個體後，會自動顯示在 [hello hello 部署環境**雲端服務**在伺服器總管] 中的節點。 從這裡，您可以看到 hello hello 個別角色執行個體狀態。 請參閱[Cloud Explorer 以管理 Azure 資源](vs-azure-tools-resources-managing-with-cloud-explorer.md).hello 下列圖例顯示 hello 角色執行個體，仍在 hello Initializing 狀態時：
   
    ![VST_DeployComputeNode](./media/vs-azure-tools-publishing-a-cloud-service/IC744134.png)

## <a name="update-a-web-role-as-part-of-hello-development-and-testing-cycle"></a>更新 Web 角色一部分 hello 開發與測試週期
如果您的應用程式後端基礎結構很穩定，但 hello web 角色需要更頻繁的更新，您可以使用 Web Deploy tooupdate web 角色專案中。 當您不想 toorebuild 並重新部署 hello 後端背景工作角色，或如果您有多個 web 角色，而且您想 tooupdate hello web 角色的其中之一，這是很方便。

### <a name="requirements"></a>需求
以下是 hello 需求 toouse Web Deploy tooupdate web 角色：

* **用於開發和測試之用：** hello 變更直接 toohello 虛擬機器正在 hello web 角色。 如果此虛擬機器具有 toobe 回收，因為您已發行的 hello 原始封裝 hello 角色使用的 toorecreate hello 虛擬機器 hello 變更都會遺失。 您必須重新發行應用程式 tooget hello 最新變更 hello web 角色。
* **只能更新 Web 角色：** 無法更新背景工作角色。 此外，您無法更新 web role.cs 中的 hello RoleEntryPoint。
* **只能支援一個 Web 角色執行個體：** 所有 Web 角色在部署環境中都不能有多個執行個體。 不過，可支援多個各只有一個執行個體的 Web 角色。
* **您必須啟用遠端桌面連線：**這是必要的如此 hello 使用者和密碼 tooconnect toohello toodeploy hello 變更 toohello server 的虛擬機器執行網際網路資訊服務 (IIS) Web Deploy 才能使用。 此外，您可能需要 tooconnect toohello 虛擬機器 tooadd 這部虛擬機器上的受信任的憑證 tooIIS。 （這可確保 hello 使用 Web Deploy 的 iis 的遠端連線安全無虞。）

hello 下列程序假設您使用 hello**發行 Azure 應用程式**精靈。

### <a name="tooenable-web-deploy-when-you-publish-your-application"></a>tooEnable Web 部署當您發行您的應用程式
1. tooenable hello**啟用 Web Deploy**針對所有 web 角色的核取方塊，您必須先設定遠端桌面連線。 選取**啟用遠端桌面**所有角色和然後供應 hello 認證將會使用從遠端在 hello tooconnect**遠端桌面組態**出現方塊。 如需詳細資訊，請參閱 [搭配使用遠端桌面與 Azure 角色](vs-azure-tools-remote-desktop-roles.md) 。
2. Web Deploy tooenable 所有 hello 應用程式中的 web 角色選取**所有 web 角色啟用 Web 都 Deploy**。
   
    此時會出現黃色警告三角形。 Web Deploy 預設會使用不受信任的自我簽署憑證，在上傳機密資料時不建議使用此憑證。 如果您需要 toosecure 此程序之機密資料，您可以加入的 Web Deploy 連線使用 SSL 憑證 toobe。 此憑證需要 toobe 受信任的憑證。 如需有關資訊 toodo，請參閱 hello 節**tooMake Web 部署安全**本主題稍後。
3. 選擇**下一步**tooshow hello**摘要**畫面上，，然後選擇 **發行**toodeploy hello 雲端服務。
   
    hello 雲端服務會發行。 hello 虛擬機器建立具有以便 Web Deploy 可使用的 tooupdate，對 IIS 啟用遠端連線的 web 角色不重新發行。
   
   > [!NOTE]
   > 如果您有多個 web 角色設定的執行個體時，會出現警告訊息，指出每個 web 角色將會限制的 tooone 只能在已建立您的應用程式 toopublish 的 hello 封裝中的執行個體。 選取**確定**toocontinue。 Hello 需求 > 一節所述，您可以擁有超過一個 web 角色，但是每一個角色只有一個執行個體。
   > 
   > 

### <a name="tooupdate-your-web-role-by-using-web-deploy"></a>tooUpdate 您所使用的 Web Deploy 的 Web 角色
1. toouse Web Deploy，請針對任何 web 角色的程式碼變更 toohello 專案在 Visual Studio 中，您想 toopublish，然後以滑鼠右鍵按一下方案中的此專案節點並點太**發行**。 hello**發行 Web**  對話方塊隨即出現。
2. （選擇性）如果您新增受信任的 SSL 憑證 toouse 適用於 IIS 的遠端連線，您可以清除 hello**允許未受信任的憑證**核取方塊。 Tooadd Web Deploy 憑證 toomake 保護相關資訊，請參閱 hello 區段**tooMake Web 部署安全**本主題稍後。
3. Web Deploy toouse，hello 發行機制需要 hello 使用者名稱和您設定遠端桌面連線時您第一次發行 hello 封裝的密碼。
   
   1. 在**使用者名**，輸入 hello 使用者名稱。
   2. 在**密碼**，輸入 hello 密碼。
   3. （選擇性）如果您想 toosave 這個密碼，此設定檔中的，選擇**儲存密碼**。
4. toopublish hello 變更 tooyour web 角色中，選擇**發行**。
   
    hello 狀態列會顯示**發行啟動**。 Hello 發行完成後，**發行成功**隨即出現。 hello 變更現在已經在虛擬機器上的部署的 toohello web 角色。 現在您可以啟動 Azure 應用程式，在 hello Azure 環境 tootest 您的變更。

### <a name="toomake-web-deploy-secure"></a>Web 部署安全的 tooMake
1. Web Deploy 預設會使用不受信任的自我簽署憑證，在上傳機密資料時不建議使用此憑證。 如果您需要 toosecure 此程序之機密資料，您可以加入的 Web Deploy 連線使用 SSL 憑證 toobe。 此憑證需要 toobe 受信任的憑證，您從憑證授權單位 (CA) 取得。
   
    toomake Web Deploy 安全的每個 web 角色的每部虛擬機器，您必須上傳 hello 受信任的憑證，您的 web 部署 toohello 想 toouse [Azure 傳統入口網站](http://go.microsoft.com/fwlink/?LinkID=213885)。 這可確保該 hello 憑證加入 toohello 發行應用程式時，會將 hello web 角色建立的虛擬機器。
2. tooadd 信任 SSL 憑證 tooIIS toouse 遠端連接，請遵循下列步驟：
   
   1. tooconnect toohello 虛擬機器執行 hello web 角色中，選取 hello 中的 hello web 角色執行個體**Cloud Explorer**或**伺服器總管**，然後選擇 hello**使用連線遠端桌面**命令。 如需詳細步驟 tooconnect toohello 虛擬機器，請參閱[透過 Azure 角色使用遠端桌面](vs-azure-tools-remote-desktop-roles.md)。
      
      您的瀏覽器將會提示您 toodownload。RDP 檔案。
   2. tooadd SSL 憑證，開啟 hello 管理服務在 IIS 管理員中。 在 [IIS 管理員] 中，開啟 hello 啟用 SSL**繫結**hello 中的連結**動作**窗格。 hello**新增網站繫結** 對話方塊隨即出現。 選擇**新增**，然後在 hello 中選擇 HTTPS**類型**下拉式清單中。 在 hello **SSL 憑證**清單中，選擇 hello SSL 憑證已由 CA 簽署並上傳 toohello [Azure 傳統入口網站](http://go.microsoft.com/fwlink/?LinkID=213885)。 如需詳細資訊，請參閱[hello 管理服務設定連線設定](http://go.microsoft.com/fwlink/?LinkId=215824)。
      
      > [!NOTE]
      > 如果您新增受信任的 SSL 憑證，hello 黃色警告三角形不再出現在 hello**發行精靈**。
      > 
      > 

## <a name="include-files-in-hello-service-package"></a>在 hello 服務封裝中包含檔案
您可能需要 tooinclude 特定的檔案服務封裝中，使其 hello 建立角色的虛擬機器上。 例如，您可能會想 tooadd.exe 或.msi 檔案所使用的啟動指令碼 tooyour 服務封裝。 或者，您可能需要 tooadd web 角色或背景工作角色專案所需的組件。 它們必須是 tooinclude 檔案加入 toohello Azure 應用程式的方案。

### <a name="tooinclude-files-in-hello-service-package"></a>tooinclude hello 服務封裝中的檔案
1. tooadd 組件 tooa 服務封裝，使用下列步驟的 hello:
   
   1. 在**方案總管 中**遺漏 hello 參考組件的 hello 專案開啟 hello 專案節點。
   2. tooadd hello 組件 toohello 專案，開啟 hello hello 的捷徑功能表**參考**資料夾，然後選擇 **加入參考**。 hello 加入參考 對話方塊隨即出現。
   3. 選擇您想 tooadd，，然後選擇 [hello hello 參考**確定**] 按鈕。
      
      hello 參考就會加入 toohello 清單下 hello**參考**資料夾。
   4. 開啟 hello hello 您加入的組件的捷徑功能表並選擇 **屬性**。 hello**屬性** 視窗隨即出現。
      
      tooinclude hello 服務中的這個組件封裝，請在 hello**複製到本機清單**選擇**True**。
2. 在**方案總管 中**遺漏 hello 參考組件的 hello 專案開啟 hello 專案節點。
3. tooadd hello 組件 toohello 專案，開啟 hello hello 的捷徑功能表**參考**資料夾，然後選擇 **加入參考**。 hello**加入參考**對話方塊隨即出現。
4. 選擇您想 tooadd，，然後選擇 [hello hello 參考**確定**] 按鈕。
   
    hello 參考就會加入 toohello 清單下 hello**參考**資料夾。
5. 開啟 hello hello 您加入的組件的捷徑功能表並選擇 **屬性**。 hello 屬性 視窗隨即出現。
6. tooinclude hello 服務中的這個組件封裝，請在 hello**複製到本機**清單中，選擇**True**。
7. hello 服務封裝中的 tooinclude 檔案已加入 tooyour web 角色專案，開啟 hello hello 檔案的捷徑功能表，然後選擇**屬性**。 從 hello**屬性**視窗中，選擇**內容**從 hello**建置動作**清單方塊。
8. hello 服務封裝中的 tooinclude 檔案已加入 tooyour 背景工作角色專案，開啟 hello hello 檔案的捷徑功能表，然後選擇**屬性**。 從 hello**屬性**視窗中，選擇**更新時才複製**從 hello**複製 toooutput 目錄**清單方塊。

## <a name="next-steps"></a>後續步驟
請參閱深入了解 Visual Studio 中，從發行 tooAzure toolearn[發行 Azure 應用程式精靈](vs-azure-tools-publish-azure-application-wizard.md)。

