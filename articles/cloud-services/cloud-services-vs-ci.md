---
title: "aaaContinuous 傳遞的雲端服務，無需使用 Visual Studio Online |Microsoft 文件"
description: "深入了解如何 tooset 總持續傳遞 azure 的雲端應用程式而不儲存診斷儲存體金鑰 toohello 服務組態檔"
services: cloud-services
documentationcenter: 
author: cawa
manager: paulyuk
editor: 
ms.assetid: 148b2959-c5db-4e4a-a7e9-fccb252e7e8a
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 11/02/2016
ms.author: cawa
ms.openlocfilehash: dc87d049e46daf8b8a26ee4450ebd9b7910f287b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="securely-save-cloud-services-diagnostics-storage-key-and-setup-continuous-integration-and-deployment-tooazure-using-visual-studio-online"></a>Securely 儲存雲端服務診斷儲存體金鑰和設定連續整合及部署使用 Visual Studio Online 的 tooAzure
 Screen 鍵是常見的作法 tooopen 來源專案。 在組態檔中儲存應用程式密碼不再是安全的作法，因為從公用原始檔控制外洩的密碼會暴露安全性漏洞。 可能因為組建伺服器可能是因為不安全的檔案中的連續整合管線的純文字儲存密碼共用 hello 雲端環境上的資源。 本文說明 Visual Studio 和 Visual Studio Online 降低的方式 hello 安全性考量開發和持續整合程序期間。

## <a name="remove-diagnostics-storage-key-secret-in-project-configuration-file"></a>移除專案組態檔中的診斷儲存體金鑰密碼
雲端服務診斷擴充功能需要 Azure 儲存體來儲存診斷結果。 先前稱為 hello 儲存體連接字串 hello 雲端服務組態 (.cscfg) 檔中會指定，且無法檢查 toosource 控制項中。 Hello 最新的 Azure SDK 版本中，我們變更 hello 行為 tooonly 存放區部分連接字串 hello 金鑰語彙基元所取代。 hello 下列步驟說明 hello 新雲端服務工具的運作方式：

### <a name="1-open-hello-role-designer"></a>1.開啟 hello 角色設計工具
* 按兩下或在雲端服務角色 tooopen 角色設計工具上以滑鼠右鍵按一下

![開啟角色設計工具][0]

### <a name="2-under-diagnostics-section-a-new-check-box-dont-remove-storage-key-secret-from-project-is-added"></a>2.[診斷] 區段下會新增 [不要從專案移除儲存體金鑰密碼] 核取方塊
* 如果您使用 hello 本機儲存體模擬器，這個核取方塊會停用，因為沒有任何密碼 toomanage hello 本機連接字串，也就是 UseDevelopmentStorage = true。

![本機儲存體模擬器連接字串並不是密碼][1]

* 如果您要建立新專案，依預設不會選取此核取方塊。 這會導致 hello 儲存體金鑰 > 一節的 hello 選取儲存體連接字串語彙基元所取代。 hello hello 語彙基元的值將資料夾下找到 hello 目前使用者的 AppData 漫遊，例如： C:\Users\contosouser\AppData\Roaming\Microsoft\CloudService

> 請注意該 hello user\AppData 資料夾為存取控制的使用者登入，並且會被視為安全的地方 toostore 開發機密資料。
> 
> 

![儲存體金鑰會儲存在使用者設定檔資料夾下][2]

### <a name="3-select-a-diagnostics-storage-account"></a>3.選取診斷儲存體帳戶
* Hello 對話方塊啟動"…"hello，即可從選取的儲存體帳戶 按鈕。 請注意如何產生 hello 儲存體連接字串不會 hello 儲存體帳戶金鑰。
* 例如︰DefaultEndpointsProtocol=https;AccountName=contosostorage;AccountKey=$(*clouddiagstrg.key*)

### <a name="4----debugging-hello-project"></a>4.  Hello 專案進行偵錯
* 在 Visual Studio 中偵錯 F5 toostart。 所有項目應該使用相同 hello 與之前的方式。
  ![在本機開始偵錯][3]

### <a name="5-publish-project-from-visual-studio"></a>5.從 Visual Studio 發佈專案
* 啟動 hello 發行對話方塊，並繼續進行登入指示 toopublish hello applicaion tooAzure。

### <a name="6-additional-information"></a>6.其他資訊
> 注意： hello 角色設計工具中的 hello 設定面板會保持原狀現在。 如果您想要診斷 toouse hello 密碼管理功能，請移 toohello 組態 索引標籤。
> 
> 

![新增設定][4]

> 注意： 如果啟用，hello Application Insights 金鑰會儲存為純文字。 hello 金鑰只會使用上傳內容，因此任何機密資料將不會受到危害的風險。
> 
> 

## <a name="build-and-publish-a-cloud-services-project-using-visual-studio-online-task-templates"></a>使用 Visual Studio Online 工作範本來建置及發佈雲端服務專案
* hello 下列步驟說明如何 toosetup 連續整合的雲端服務專案使用 Visual Studio online 工作：
  ### <a name="1----obtain-a-vso-account"></a>1.  取得 VSO 帳戶
* [建立 Visual Studio Online 帳戶][ Create Visual Studio Online account]如果您還沒有任何
* [建立 team 專案][ Create team project]在您的 Visual Studio online 帳戶

### <a name="2----setup-source-control-in-visual-studio"></a>2.  在 Visual Studio 中設定原始檔控制
* 連接 tooa team 專案

![Tooteam 專案連接][5]

![若要選取的 team 專案 tooconnect][6]

* 加入您專案的 toosource 控制項

![將專案 toosource 控制項][7]

![對應專案 tooa 原始檔控制資料夾][8]

* 從 Team Explorer 簽入您的專案

![簽入 toosource 控制專案][9]

### <a name="3----configure-build-process"></a>3.  設定建置流程
* 瀏覽 tooyour team 專案並加入新的建置流程範本

![新增組建][10]

* 選取建置工作

![新增建置工作][11]

![選取 Visual Studio 建置工作範本][12]

* 編輯建置工作輸入。 請自訂 hello 組建必須根據 tooyour 參數

![設定建置工作][13]

`/t:Publish /p:TargetProfile=$(targetProfile) /p:DebugType=None /p:SkipInvalidConfigurations=true /p:OutputPath=bin\ /p:PublishDir="$(build.artifactstagingdirectory)\\"`

* 設定組建變數

![設定組建變數][14]

* 新增工作 tooupload 組建置放

![選擇發佈組建置放工作][15]

![設定發佈組建置放工作][16]

* 執行 hello 組建

![將新組建排入佇列][17]

![檢視組建摘要][18]

* hello 建置成功時，您會看到結果類似 toobelow

![建置結果][19]

### <a name="4----configure-release-process"></a>4.  設定發行程序
* 建立新版本

![建立新版本][20]

* 選取 hello Azure 雲端服務部署工作

![選取 Azure 雲端服務部署工作][21]

* Hello 儲存體帳戶金鑰不會檢查 toosource 控制項中，我們需要 toospecify hello 祕密金鑰設定診斷延伸。 展開 hello**建立新服務的進階選項**區段，並編輯 hello**診斷儲存體帳戶金鑰**參數的輸入。 在多行程式中的 hello 格式的機碼值組會採用此輸入**[RoleName]:$(StorageAccountKey)**

> 附註： 如果您的診斷儲存體帳戶是在 hello 與您要在其中發行 hello 雲端服務應用程式相同的訂閱，您不需要 tooenter hello 金鑰 hello 部署工作輸入; 中hello 部署就會從您的訂用帳戶以程式設計方式取得 hello 儲存體資訊
> 
> 

![設定雲端服務部署工作][22]

* 使用密碼建立變數 toosave 儲存體金鑰。 按一下右邊 hello hello hello 鎖定圖示的 做為密碼變數 toomask 變數輸入

![在密碼建置變數中儲存儲存體金鑰][23]

* 建立發行和部署專案 tooAzure

![建立新版本][24]

## <a name="next-steps"></a>後續步驟
toolearn 進一步了解 Azure 雲端服務，設定診斷延伸模組，請參閱[使用 PowerShell 的 Azure 雲端服務中啟用診斷][Enable diagnostics in Azure Cloud Services using PowerShell]

[Create Visual Studio Online account]:https://www.visualstudio.com/team-services/
[Create team project]: https://www.visualstudio.com/it-it/docs/setup-admin/team-services/connect-to-visual-studio-team-services
[Enable diagnostics in Azure Cloud Services using PowerShell]:https://azure.microsoft.com/en-us/documentation/articles/cloud-services-diagnostics-powershell/

[0]: ./media/cloud-services-vs-ci/vs-01.png
[1]: ./media/cloud-services-vs-ci/vs-02.png
[2]: ./media/cloud-services-vs-ci/file-01.png
[3]: ./media/cloud-services-vs-ci/vs-03.png
[4]: ./media/cloud-services-vs-ci/vs-04.png
[5]: ./media/cloud-services-vs-ci/vs-05.png
[6]: ./media/cloud-services-vs-ci/vs-06.png
[7]: ./media/cloud-services-vs-ci/vs-07.png
[8]: ./media/cloud-services-vs-ci/vs-08.png
[9]: ./media/cloud-services-vs-ci/vs-09.png
[10]: ./media/cloud-services-vs-ci/vso-01.png
[11]: ./media/cloud-services-vs-ci/vso-02.png
[12]: ./media/cloud-services-vs-ci/vso-03.png
[13]: ./media/cloud-services-vs-ci/vso-04.png
[14]: ./media/cloud-services-vs-ci/vso-05.png
[15]: ./media/cloud-services-vs-ci/vso-06.png
[16]: ./media/cloud-services-vs-ci/vso-07.png
[17]: ./media/cloud-services-vs-ci/vso-08.png
[18]: ./media/cloud-services-vs-ci/vso-09.png
[19]: ./media/cloud-services-vs-ci/vso-10.png
[20]: ./media/cloud-services-vs-ci/vso-11.png
[21]: ./media/cloud-services-vs-ci/vso-12.png
[22]: ./media/cloud-services-vs-ci/vso-13.png
[23]: ./media/cloud-services-vs-ci/vso-14.png
[24]: ./media/cloud-services-vs-ci/vso-15.png
