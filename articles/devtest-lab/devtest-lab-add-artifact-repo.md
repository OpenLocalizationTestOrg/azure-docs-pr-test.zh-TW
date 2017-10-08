---
title: "aaaAdd Azure DevTest 實驗室中的 Git 儲存機制 tooa 實驗室 |Microsoft 文件"
description: "將適用於自訂構件來源的 GitHub 或 Visual Studio Team Services Git 儲存機制加入 Azure DevTest Labs"
services: devtest-lab,virtual-machines,visual-studio-online
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 01b459f7-eaf2-45a8-b4b5-2c0a821b33c8
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/11/2017
ms.author: tarcher
ms.openlocfilehash: e590559ffb2d497e39823e35c3f66974f42f13c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-git-repository-toostore-custom-artifacts-and-azure-resource-manager-templates"></a>加入 Git 儲存機制 toostore 自訂成品和 Azure 資源管理員範本

如果您想太[建立自訂的成品](devtest-lab-artifact-author.md)hello Vm 在實驗室中，或[使用 Azure Resource Manager 範本 toocreate 自訂測試環境](devtest-lab-create-environment-from-arm.md)，您也必須加入私用 Git 儲存機制 tooinclude您的小組所建立的 Azure Resource Manager 範本或 hello 成品。 hello 儲存機制可裝載於[GitHub](https://github.com)或在[Visual Studio Team Services (VSTS)](https://visualstudio.com)。

我們提供[構件的 Github 存放庫](https://github.com/Azure/azure-devtestlab/tree/master/Artifacts)，您可以為您的實驗室依原樣部署為自行自訂。 當您自訂或建立成品時，無法將其儲存在 hello 公用儲存機制中，您必須建立您自己的私用儲存機制。 

當您建立 VM 時，您可以儲存 hello Azure Resource Manager 範本，如果您想要，然後使用它來自訂稍後 tooeasily 建立多個 Vm。 您必須建立您自己的私用儲存機制 toostore 自訂的 Azure Resource Manager 範本。  

* 如何 toocreate GitHub 儲存機制中，請參閱的 toolearn [GitHub Bootcamp](https://help.github.com/categories/bootcamp/)。
* 如何 toocreate Team Services 專案使用 Git 儲存機制，請參閱的 toolearn[連接 tooVisual Studio Team Services](https://www.visualstudio.com/get-started/setup/connect-to-visual-studio-online)。

hello 下列螢幕擷取畫面顯示在 GitHub 中包含的成品儲存機制可能外觀的範例：  
![GitHub 構件儲存機制範例](./media/devtest-lab-add-repo/devtestlab-github-artifact-repo-home.png)

## <a name="get-hello-repository-information-and-credentials"></a>取得 hello 儲存機制資訊和認證
tooadd 儲存機制 tooyour 實驗室，您必須先取得特定資訊，以從您的儲存機制。 hello 下列各節將引導您完成取得這項資訊儲存機制裝載於 GitHub 和 Visual Studio Team Services。

### <a name="get-hello-github-repository-clone-url-and-personal-access-token"></a>取得 hello GitHub 儲存機制複製品 URL 和個人存取權杖
tooget hello GitHub 儲存機制複製品 URL 和個人存取權杖，請遵循下列步驟：

1. 瀏覽 toohello 首頁 hello GitHub 儲存機制包含 hello 成品或 Azure 資源管理員範本定義。
2. 選取 [複製或下載] 。
3. 選取 hello 按鈕 toocopy hello **HTTPS 複製 url** toohello 剪貼簿，並儲存供稍後使用 hello URL。
4. 在 GitHub，hello 右上角選取 hello 設定檔影像，然後選取**設定**。
5. 在 hello**個人設定**功能表靠左、 hello 選取**個人存取權杖**。
6. 選取 [產生新的權杖] 。
7. Hello 上**新的個人存取權杖**頁面上，輸入**語彙基元描述**，接受 hello 預設項目在 hello**選取範圍**，然後選擇 **產生語彙基元**。
8. 視需要更新版本，請儲存 hello 產生語彙基元。
9. 您現在可以關閉 GitHub。   
10. 繼續 toohello[連接您的實驗室 toohello 儲存機制](#connect-your-lab-to-the-repository)> 一節。

### <a name="get-hello-visual-studio-team-services-repository-clone-url-and-personal-access-token"></a>取得 hello Visual Studio Team Services 的儲存機制複製品 URL 和個人存取權杖
tooget hello Visual Studio Team Services 的儲存機制複製品 URL 和個人存取權杖，請遵循下列步驟：

1. 開啟 hello 首頁上的 team 集合 (例如， `https://contoso-web-team.visualstudio.com`)，然後選取您的專案。
2. 在 hello 專案首頁上，選取 **程式碼**。
3. tooview hello 複製 URL，hello 專案**程式碼**頁面上，選取**複製**。
4. 視需要稍後在本教學課程，請儲存 hello URL。
5. 選取 個人存取權杖，toocreate**我的設定檔**從 hello 使用者帳戶下拉式選單。
6. 在 hello 設定檔資訊 頁面上，選取 **安全性**。
7. 在 hello**安全性**索引標籤上，選取**新增**。
8. 在 hello**建立個人存取權杖**頁面：

   * 輸入**描述**hello 語彙基元。
   * 選取**180 天**從 hello **到期日**清單。
   * 選擇**可存取的所有帳戶**從 hello**帳戶**清單。
   * 選擇 hello**所有領域**選項。
   * 選擇 [建立權杖] 。
9. Hello 新語彙基元完成時，會出現在 hello**個人存取權杖**清單。 選取**Token 複製**，然後儲存供稍後使用 hello 語彙基元值。
10. 繼續 toohello[連接您的實驗室 toohello 儲存機制](#connect-your-lab-to-the-repository)> 一節。

## <a name="connect-your-lab-toohello-repository"></a>連接您的實驗室 toohello 儲存機制
1. 登入 toohello [Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=525040)。
2. 選取**更服務**，然後選取**DevTest Labs**從 hello 清單。
3. 從 hello 清單的實驗室中，選取 hello 所需的實驗室。   
4. 在 hello 左面板中，選取 **組態和原則**。
5. 在 hello 實驗室**組態和原則**區域中，選取**儲存機制**。
6. 在 hello**儲存機制**區域中，選取**+ 加**。

    ![[新增存放庫] 按鈕](./media/devtest-lab-add-repo/devtestlab-add-repo.png)
7. 在 hello 第二個**儲存機制**頁面上，指定下列資訊的 hello:

   * **名稱**-輸入 hello 儲存機制的名稱。
   * **Git 複製 Url** -輸入 hello Git HTTPS 複製 URL，您之前複製從 GitHub 或 Visual Studio Team Services。
   * **分支**-輸入 hello 分支 tooget 惡意程式碼定義。
   * **個人存取權杖**-輸入您稍早取得的 GitHub 或 Visual Studio Team Services hello 個人存取權杖。
   * **資料夾路徑**-輸入最少一個資料夾路徑相對 toohello 複製 URL，其中包含您成品或 Azure 資源管理員範本定義。 當指定子目錄，請確定 tooinclude hello 正斜線 hello 資料夾路徑中。

     ![存放庫區域](./media/devtest-lab-add-repo/devtestlab-repo-blade.png)
8. 選取 [ **儲存**]。

## <a name="next-steps"></a>後續步驟
建立私用 Git 儲存機制之後，您可以一或兩個 hello 下列程式碼，根據您的需求：
* 存放區您[自訂成品](devtest-lab-artifact-author.md)，而您可以使用更新版本的 toocreate 新 Vm。
* [使用 Azure Resource Manager 範本建立環境多部 VM 和 PaaS 資源](devtest-lab-create-environment-from-arm.md)然後將 hello 範本儲存在您的私用儲存機制。

當您建立 VM 時，您可以確認 hello 成品或範本加入 tooyour Git 儲存機制。 欄位屬性可立即在 hello 成品或範本的清單，以您指定 hello 來源的 hello 資料行所示的私用儲存機制的 hello 名稱中。 

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

### <a name="related-blog-posts"></a>相關部落格文章
* [如何 tootroubleshoot 失敗 Azure DevTest Labs 中的成品](devtest-lab-troubleshoot-artifact-failure.md)
* [加入 VM tooexisting Azure DevTest 實驗室中使用資源管理員範本的 AD 網域](http://www.visualstudiogeeks.com/blog/DevOps/Join-a-VM-to-existing-AD-domain-using-ARM-template-AzureDevTestLabs)
