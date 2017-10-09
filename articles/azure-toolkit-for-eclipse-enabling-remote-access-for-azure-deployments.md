---
title: "aaaEnabling 在 Eclipse 的 Azure 部署的遠端存取權"
description: "了解 tooenable 遠端存取使用 hello Azure Toolkit for Eclipse 的 Azure 部署的方式。"
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: b6150006-9a7f-4d83-be18-d35ec780c7c5
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 00c2bf22c1f3ec792098f154f771c87506e87881
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="enabling-remote-access-for-azure-deployments-in-eclipse"></a>在 Eclipse 中啟用 Azure 部署的遠端存取
toohelp 疑難排解您的部署，您可能會啟用並使用裝載您部署遠端存取 tooconnect toohello 虛擬機器。 hello 遠端存取 」 功能會依賴 hello 遠端桌面通訊協定 (RDP)。 您已發行它 tooAzure，或如果您使用 Eclipse 與 Windows 作業系統，您就可以設定遠端存取，然後再發行 tooAzure 之後，您可以設定遠端存取您的部署。 請注意，您將需要遠端桌面用戶端與您在 Azure 中的順序 tooconnect tooyour 部署的虛擬機器的作業系統相容。

## <a name="how-tooenable-remote-access-before-you-deploy-tooazure"></a>如何才能 tooenable 遠端存取部署 tooAzure
> [!NOTE]
> tooenable 遠端存取部署應用程式 tooAzure 之前，您需要在 Windows 上執行 Eclipse toobe。
> 
> 

hello 下列影像顯示 hello**遠端存取**使用 tooenable 遠端存取內容對話方塊。

![][ic719494]

有兩種方式 toodisplay hello**遠端存取**屬性 對話方塊：

* 按一下 hello**進階**hello 中的連結**遠端存取**區段 hello**發行 tooAzure**對話方塊。

* 開啟 hello**屬性**的 Azure 專案 對話方塊。

當您建立新的 Azure 部署專案時，hello 專案不會預設啟用遠端存取。 不過，您可以輕鬆地啟用遠端存取指定 hello 使用者名稱和密碼在 hello**發行 tooAzure**對話方塊。 使用 X.509 憑證加密 hello 遠端存取密碼。 如果您未使用提供您自己的憑證，hello 加密依賴隨附 hello Azure Plugin for Eclipse 的自我簽署憑證。 此自我簽署的憑證是在 hello **cert**您的 Azure 專案的資料夾會儲存兩種形式的公開憑證檔案 (SampleRemoteAccessPublic.cer) 和做為個人資訊交換 (PFX) 憑證檔案 （SampleRemoteAccessPrivate.pfx)。 hello 後者包含 hello hello 憑證私密金鑰，而且有預設密碼**Password1**。 不過，由於此密碼是公用的知識，hello 預設憑證應只用於學習目的，不適用於生產環境部署。 因此以外的學習的目的，當您想 tooenabled 遠端工作階段為您的部署，您應該按一下 hello**進階**hello 中的連結**發行 tooAzure**對話方塊 toospecify 自己憑證。 請注意，您必須 tooupload hello PFX 版本 hello 憑證 tooyour 託管服務內 hello Azure 管理入口網站，讓 Azure 可以解密 hello 使用者密碼。

hello hello 教學課程的其餘部分會顯示 tooenable 遠端存取的 Azure 部署專案，開始建立停用遠端存取的方式。 基於本教學課程的目的，我們將建立一個新的自我簽署憑證，而其 .pfx 檔案將包含您選擇的密碼。 您也可以使用憑證授權單位所核發的憑證的 hello 選項。

## <a name="how-tooenable-remote-access-after-you-have-deployed-tooazure"></a>如何 tooenable 遠端存取之後，您已部署 tooAzure
tooenable 遠端存取部署 tooAzure，下列步驟使用 hello 之後：

1. 登入使用您的 Azure 帳戶的 hello Azure 管理入口網站

2. 在 [雲端服務] 清單中，選取您部署的雲端服務

3. 在 hello 雲端服務網頁上，按一下 hello**設定**連結

4. 在 hello hello 組態 頁面底部，按一下 hello**遠端**連結

5. Hello 快顯對話方塊出現時：
   
   * 指定角色 hello 您想 tooenable 遠端存取

   * 按一下 tooselect hello**啟用遠端桌面**核取方塊
   
   * 指定使用者名稱和密碼，您想要遠端存取 toouse
   
   * 選取 hello 憑證 toouse

6. 按一下 [檔案] &gt; [新增] &gt; [專案]  

您會看到一個訊息，指出您的組態變更正在進行，這可能需要幾分鐘的時間 toocomplete 中。 Hello 組態變更完成之後，請依照 hello 中的 hello 步驟**toolog 中的從遠端**本文中稍後的章節。

## <a name="how-tooenable-remote-access-in-your-package"></a>如何在封裝中的 tooenable 遠端存取
1. 在 Eclipse 的專案總管窗格中，於您的 Azure 專案上按一下滑鼠右鍵，並按一下 [內容] 。

2. 在 hello**屬性** 對話方塊中，展開  **Azure**在 hello 左側窗格中按一下**遠端存取**。

3. 在 [hello**遠端存取**] 對話方塊中，確定**啟用所有角色 tooaccept 遠端桌面連線使用這些登入認證**已核取。

4. 指定 hello 遠端桌面連線的使用者名稱。

5. 指定並確認 hello hello 使用者密碼。 當您進行 「 遠端桌面 」 連線時，將使用 hello 的使用者名稱和密碼值在此對話方塊中設定。 (請注意，這個密碼不同於您的 PFX 密碼)。

6. 指定 hello hello 使用者帳戶到期日。

7. 按一下**新增**toocreate 新的自我簽署憑證。 (或者，您可以選取憑證，從您的工作區或檔案系統，透過 hello**工作區**或**FileSystem**分別，但基於本教學課程中我們將建立新的按鈕憑證。）

   * 在 [hello**新憑證**] 對話方塊中，指定並確認您會使用 PFX 檔案的 hello 密碼。

   * 接受提供的 hello 值**名稱 (CN)**，或使用自訂名稱。

   * 指定要在其中儲存 hello 新的憑證，.cer 格式的 hello 路徑和檔案名稱。 此步驟和 hello 下一個步驟中，您可以使用 hello **cert**的 Azure 專案，但您的資料夾是免費 toochoose 另一個位置。 基於本教學課程的目的，我們將使用 **c:\mycert\mycert.cer**。 (建立 hello **c:\mycert**先前 tooproceeding 資料夾或使用現有的資料夾，視。)

   * 指定要儲存 hello 新憑證和私密金鑰，.pfx 格式的 hello 路徑和檔案名稱。 基於本教學課程的目的，我們將使用 **c:\mycert\mycert.pfx**。 您**新憑證**對話方塊看起來類似 toohello 下列 (更新 hello 資料夾路徑，如果您未使用**c:\mycert**):
     
      ![][ic712275]

   * 按一下**確定**tooclose hello**新憑證**對話方塊。

8. 您**遠端存取**對話方塊看起來類似 toohello 下列：</p>
   
   ![][ic719495]

9. 按一下**確定**tooclose hello**遠端存取**對話方塊。

重建您的應用程式，以 hello 建置部署 toocloud 的集合。

## <a name="toolog-in-remotely"></a>在 toolog 遠端
角色執行個體準備就緒之後，您可以從遠端登入 toohello 則裝載應用程式的虛擬機器中。

* 如果在 Windows 和您選取的 hello 上使用 Eclipse**上的啟動遠端桌面部署**選項在您部署 tooAzure，您會看到的遠端桌面連線登入畫面啟動您的部署時。 當系統提示您輸入 hello 使用者名稱和密碼時，輸入您為 hello 遠端使用者指定的 hello 值，且將無法 toolog 中。

* 中的另一個方式 toolog 遠端是透過 hello <a href="http://go.microsoft.com/fwlink/?LinkID=512959">Azure 管理入口網站</a>:
  
  * Hello 內**雲端服務**檢視 hello Azure 管理入口網站中，按一下您的雲端服務中，按一下**執行個體**，按一下 [特定的執行個體，然後按一下hello**連接**] 按鈕。 hello**連接**按鈕會顯示為 hello 命令列中的 hello 下列：
    
      ![][ic659273]

  * 按一下 hello 之後**連接** 按鈕，您將會提示的 tooopen RDP 檔案。 開啟 hello 檔案，並依照 hello 提示。 (您可能也儲存此檔案 tooyour 本機電腦，然後執行 hello 檔案按兩下 tooremote 記錄 tooyour 中虛擬機器，而不需要 toofirst 移 hello 管理入口網站。)

  * 當系統提示您輸入 hello 使用者名稱和密碼時，輸入您為 hello 遠端使用者指定的 hello 值，且將無法 toolog 中。

> [!NOTE]
> 如果您是在非 Windows 作業系統上，您需要 toouse 遠端桌面用戶端與作業系統相容，並遵循 hello 步驟 tooconfigure 與 hello 您下載的 RDP 檔案中的 hello 設定該用戶端。
> 
> 

## <a name="see-also"></a>另請參閱
[適用於 Eclipse 的 Azure 工具組][Azure Toolkit for Eclipse]

[在 Eclipse 中為 Azure 建立 Hello World 應用程式][Creating a Hello World Application for Azure in Eclipse]

[安裝 Azure Toolkit for Eclipse hello][Installing hello Azure Toolkit for Eclipse] 

如需有關使用 Azure 與 Java 的詳細資訊，請參閱 hello [Azure Java 開發人員中心][Azure Java Developer Center]。

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic712275]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic712275.png
[ic719495]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic719495.png
[ic719494]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic719494.png
[ic659273]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic659273.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690951.aspx -->
