---
title: "教學課程： 以 hello Azure 入口網站 DevOps |Microsoft 文件"
description: "深入了解 hello hello Azure 入口網站中的各種 DevOps 工作流程。"
services: azure-portal
documentationcenter: 
author: mlearned
manager: douge
editor: mlearned
ms.assetid: 4f1c5bc1-c732-4d35-b5df-0fd68e547d38
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 06/05/2016
ms.author: mlearned
ms.openlocfilehash: 4c32dbbd4e4b1c3809ef4b01e1496e350183ebde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-devops-with-hello-azure-portal"></a>教學課程： DevOps hello Azure 入口網站
hello Azure 平台是完整的彈性 DevOps 工作流程。 在此教學課程中，您將學會如何 hello Azure 入口網站 toodevelop，tooleverage hello 功能測試、 部署、 疑難排解、 監視和管理執行中應用程式。 本教學課程著重於 hello 下列：

1. 建立 Web 應用程式並啟用連續部署
2. 開發和測試應用程式
3. 監視和針對應用程式進行疑難排解
4. 一般應用程式管理工作

## <a name="creating-a-web-app-and-enabling-continuous-deployment"></a>建立 Web 應用程式並啟用連續部署
建立 Web 應用程式與[Azure App Service](https://azure.microsoft.com/services/app-service/)，會使用在本教學課程的 hello 其餘部分。 一開始，您將會進行從原始程式碼儲存機制到執行中 Azure 環境的連續部署。

1. 登入 hello Azure 入口網站
2. 選擇**應用程式服務** &gt; **新增圖示**和輸入的名稱、 選擇您的訂用帳戶，以及為 hello hello 服務容器中建立新的資源群組 tooserve。
   
   資源群組可讓您 toomanage hello 的解決方案，例如計費、 部署及監視所有以透過單一群組的各個層面[Azure Resource Manager](../azure-resource-manager/resource-group-overview.md)。
   
   ![image1][image1]
3. 幾分鐘後，您的 App Service 便會建立。 請花幾分鐘的時間 tooexplore hello hello 服務的各種功能表選項 hello 入口網站中。
   
   ![image2][image2]    
4. 按一下 hello URL。 請注意 hello 各種不同的工具和儲存機制的可用選項。 您也可以使用 hello 語言和您選擇，包括.NET、 Java 和 Ruby 的架構。
   
   ![image3][image3]    
5. hello Azure 入口網站可讓持續部署簡單的程序，包括只有一些簡單的步驟。 在 hello Azure 入口網站，選取 從 hello 您剛才建立的應用程式服務的 hello 圖示的 設定。
   
   ![image4][image4]
   
   從 hello 刀鋒視窗中開啟 hello 右上，捲動 toohello 發行 > 一節。
   
   ![image5][image5]
6. 接著，設定某些設定 tooenable 的連續部署 hello 應用程式。 按一下 部署來源，然後按一下選擇來源。 請注意 hello 各種選項，您的儲存機制來源。
   
   ![image6][image6]
7. 在此範例中，請選擇 [GitHub]。 選擇性地選擇您所選擇的 hello 儲存機制，並設定 hello 授權認證。
   
   ![image7][image7]
8. 之後授權 tooyour 儲存機制，然後您可以選擇的專案及您想 toodeploy 的分支。 下面列出幾個虛構的範例。
   
   ![image8][image8]
9. 在選擇專案和分支之後，按一下 [確定]。 您應該開始 toosee 通知的部署。
   
   ![image9][image9]
10. 瀏覽 Azure 以建立 toointegrate hello 原始檔控制儲存機制後 tooGitHub toosee hello webhook。 hello Azure 入口網站可讓整合與 GitHub 只有一些簡單的步驟。
    
    ![image10][image10]
11. toodemonstrate 連續部署，您快速加入一些內容 toohello 儲存機制。 如需簡單範例中，加入範例文字檔案 tooa GitHub 儲存機制。 您是免費 toouse.NET、 Ruby、 Python 或其他類型的應用程式與應用程式服務。 感覺可用 tooadd 文字檔案時，ASP.NET MVC、 Java 或 Ruby 應用程式 toohello 儲存機制的選擇。
    
    ![image11][image11]
12. 認可之後變更 tooyour 儲存機制，您會看到新的部署起始 hello 入口網站的通知區域中。 如果看不到快速變更認可 tooyour 儲存機制之後，請按一下 同步處理。
    
    ![image12][image12]
13. 此時，如果您再試一次，並載入 hello 應用程式服務的 hello 頁面，您可能會收到 403 錯誤。 在此範例中，是因為沒有任何一般預設文件的安裝 hello 頁面，例如 index.htm 或 default.html 檔案。 您可以快速補救這種情況以 hello tooling hello Azure 入口網站中。  在 hello Azure 入口網站中選擇 設定&gt;應用程式設定。
    
     ![image13][image13]
14. 隨即會開啟 [應用程式設定] 的刀鋒視窗。 輸入 hello 頁面 」 SamplePage.html"hello 名稱，然後按一下 [儲存]。 需要幾分鐘的時間 tooexplore hello 其他設定。
    
    ![Image14][image14]
15. 選擇性地重新整理您的瀏覽器 URL tooensure 您看到 hello 預期的變更。 在此情況下，還有一些簡單的文字現在填入 hello 頁面。 每個額外的變更 toohello 儲存機制可能會導致新的自動部署。
    
    ![Image15][image15]
    
    啟用以 hello Azure 入口網站的連續部署是簡單的體驗。 您也可以建置更複雜的發行管線，並使用現有的原始檔控制和持續整合系統 toodeploy tooAzure，例如運用自動化的建置和發行管理系統的許多其他技術。

## <a name="develop-and-test-an-app"></a>開發和測試應用程式
接下來，進行一些變更 toohello 程式碼基底和這些變更，快速部署。 您也會設定一些效能測試 hello Web 應用程式。

1. Hello Azure 入口網站中從 hello 瀏覽窗格中，選擇應用程式服務，並找出您的應用程式服務。
   
   ![Image16][image16]
2. 按一下 [工具]
   
   ![Image17][image17]
3. 請注意 hello 開發工具 底下。 有數種有用的工具這裡可讓我們 toowork 與應用程式而不需離開 hello Azure 入口網站。 按一下 [主控台]。
   
   ![Image18][image18]
4. 在 hello 主控台視窗中，您可以為您的應用程式發出即時命令。 型別 hello dir 命令並按 enter 鍵。 請注意，需要較高權限的命令不會運作。
   
   ![Image19][image19]
5. 移回 toohello 開發類別目錄，然後選擇 Visual Studio Online。 注意：Visual Studio Online 現已更名為 Visual Studio Team Services。
   
   ![Image20][image20]
6. 開啟您的應用程式的 hello 瀏覽器中編輯體驗。
   
   ![Image21][image21]
7. 隨即會為應用程式安裝 Web 擴充功能。 擴充功能快速且輕鬆地新增功能 tooapps 在 Azure 中。 請注意一些 hello hello 以下螢幕擷取畫面中，您可以使用其他擴充功能類型。
   
   ![Image22][image22]
8. 一旦 hello Visual Studio Online 擴充功能安裝，請按一下 移至。
   
   ![Image23][image23]
9. 在瀏覽器索引標籤隨即開啟，您會看到直接在 hello 瀏覽器中的開發 IDE。 請注意 hello 經驗以下是在 Chrome 中。
   
   ![Image24][image24]
10. 您可以執行數個活動，例如編輯檔案、 新增檔案和資料夾，以及下載 hello 即時網站內容。 使快速編輯 toohello SamplePage.html 檔案。
    
    ![Image25][image25]
11. 在幾分鐘後，會自動儲存 hello 變更。 如果您瀏覽後 toohello 頁面，您可以看到 hello 變更。 請記住，這類即時編輯很可能不適用於生產環境。 不過，hello 工具讓您可以非常輕易 toomake 快速變更的開發人員和測試環境。
    
    ![image26][image26]
    
    ![image27][image27]
12. 移回 toohello 工具刀鋒視窗然後 hello 開發在分類底下，按一下 效能測試。
    
    ![Image28][image28]
13. 您需要 tooset team services 帳戶。 如需詳細資訊，請參閱此處︰ [建立 Team Services 帳戶](https://www.visualstudio.com/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services)
14. 按一下新 toocreate 效能測試。
    
    ![Image29][image29]
    
    設定 hello 各種值，然後按一下 執行於 hello 下方 hello 對話方塊 tooinitiate 效能測試的測試。
    
    ![Image30][image30]
    
    ![Image31][image31]
15. 一旦 hello 測試便會開始執行，您可以監視 hello 狀態。
    
    ![Image32][image32]
    
    一旦 hello 測試完成時，按一下即可在 hello 結果顯示更多詳細資料。
    
    ![Image33][image33]
16. 在此範例中，您會建立小型測試回合，因此沒有有限的資料 tooanalyze，但是您可以查看各種度量，以及重新執行您的測試從這個檢視。 建立、 執行和分析簡單的程序的 web 效能測試，可讓 hello Azure 入口網站。 hello 以下螢幕擷取畫面顯示 hello 效能資料。
    
    ![Image34][image34]
    
    ![Image35][image35]
    
    ![Image36][image36]

## <a name="monitoring-and-troubleshooting-an-app"></a>監視和針對應用程式進行疑難排解
Azure 提供許多用來監視和針對執行中應用程式進行疑難排解的功能。

1. 在我們的 Web 應用程式的 hello Azure 入口網站中選擇 [工具]。
   
   ![Image37][image37]
2. Hello 疑難排解類別 下方，注意到 hello 各種選擇的執行中應用程式中使用工具 tootroubleshoot 潛在問題。 您可以執行監視即時 HTTP 流量、啟用自我修復、檢視記錄檔等等的作業。
   
   ![Image38][image38]
3. 選擇網站度量 tooquickly get 某些 HTTP 代碼的檢視。
   
   ![image39][image39]
4. 選擇 [診斷即服務]。 選擇 [應用程式類型]，然後選擇 [執行]。
   
   ![image40][image40]
   
   隨即會開始收集。
   
   ![image41][image41]
5. 您可以選擇 hello 適當記錄 toodiagnose 潛在問題。 您需要 tooenable 記錄 toosee，例如 HTTP 記錄檔中的所有 hello 可用資料的選項。
   
   ![image42][image42]
   
   您可以下載並分析 DebugDiag hello 記憶體傾印檔案，即可分析報表 toohelp 尋找潛在問題。
   
   ![image43][image43]
6. tooview 更多資料，您需要 tooenable 額外的記錄功能。 在 hello Azure 入口網站，瀏覽 toohello Web 應用程式並選擇 [設定]。
   
   ![image44][image44]
7. 向下捲動 toohello 功能類別目錄，然後選擇 診斷記錄檔。
   
      ![image45][image45]
8. 請注意 hello 記錄的各種選項。 開啟 [Web 伺服器記錄]，並按一下 [儲存]。
   
   ![image46][image46]
9. 移回 toohello hello 應用程式的工具區域並選擇 診斷 做為服務，然後按一下 執行 toorerun hello 資料收集。
   
   ![image47][image47]
10. 啟用 hello HTTP 記錄設定，您現在會看到針對 HTTP 記錄檔中收集的資料。
    
    ![image48][image48]
11. 按一下 hello HTML 檔案記錄檔，您就可以產生豐富的瀏覽器為基礎的報表做進一步調查。
    
    ![image49][image49]
12. 移回 toohello 工具 > 一節中的 hello 應用程式的 hello Azure 入口網站。 捲動 toohello 工具 > 一節，並選擇處理序總管。
    
    ![image50][image50]
13. 藉由選擇處理序總管，您即可檢視執行中處理序的詳細資料。 通知低於您可以切入到處理程序，然後即使清除來自 hello Azure 入口網站的所有處理程序。
    
    ![image51][image51]
    
    ![image52][image52]
14. Hello 左移回 toohello 設定 刀鋒視窗。 按一下 [新增支援要求]。
    
    ![image53][image53]
15. Hello 刀鋒視窗上 hello 右中，從您可以填寫 hello 問題的詳細、 輸入人員連絡資訊，且即使上傳診斷資料。 hello Azure 入口網站可讓您使用 Microsoft 支援順暢的體驗。
    
    ![image54][image54]
    
    ![image55][image55]
    
    hello Azure 入口網站可協助提供功能強大且熟悉的工具體驗 toohelp 監視和疑難排解執行的應用程式。 您也是可以 tootake 動作快速執行工作，例如回收處理程序、 啟用和停用各種資料集合，以及甚至整合與 Microsoft 專業人員支援。

## <a name="general-application-management"></a>一般應用程式管理
當管理應用程式時，您通常需要 tooperform 各式各樣的活動，例如設定的備份策略、 實作和管理身分識別提供者，以及設定以角色為基礎的存取控制。 與 hello 其他 DevOps 體驗，如 hello Azure 平台整合直接在 hello 入口網站，這些工作。

1. 保持的 tooensure hello Web 應用程式安全，防止資料遺失您需要 tooconfigure 備份。 瀏覽 toohello 設定 Web 應用程式 區域。
   
   ![image56][image56]
2. 在 hello 刀鋒視窗上 hello 右中，捲動 toohello 功能類別。
   
    ![image57][image57]
3. 選擇的備份。hello 右邊會開啟刀鋒視窗。
   
   ![image58][image58]
4. 按一下 設定，從上 hello 右 hello 刀鋒視窗中選擇儲存體帳戶。
   
   ![image59][image59]
5. 現在建立，並選擇您的備份儲存體容器 toohold。 按一下 建立在 hello hello 刀鋒視窗的底部。 然後，選取 hello 容器。
   
   ![image60][image60]
6. 一旦您已選擇 hello 容器，您可以設定排程，以及安裝備份為您的資料庫。 此案例中，按一下儲存圖示 hello。
   
    ![image61][image61]
7. 儲存之後，請備份捲動 hello 左側後 toohello 刀鋒視窗。 按一下 立即備份 tooback hello 應用程式。
   
    ![image62][image62]
8. 幾分鐘後，您便會看到建立了備份。 請注意 hello 立即還原 hello 螢幕擷取畫面下方的選項。
   
    ![image63][image63]
9. 按一下 立即還原，並檢查 hello 選項 toohello 刀鋒視窗上 hello 右。 您可以選擇適當的備份和輕鬆還原 tooan 先前狀態在必要時。 hello Azure 入口網站有幫助我們 hello 應用程式的簡單的災害復原策略，輕鬆啟用。
   
    ![image64][image64]
10. 移回 toohello 設定 刀鋒視窗左側 hello，並在 功能，並選擇 驗證/授權。
    
     ![image65][image65]
11. 在上 hello 右 hello 刀鋒視窗中選擇應用程式服務驗證。 請注意 hello 各種選項，您可以使用常用的提供者設定。
    
     ![image66][image66]
12. 選擇您所選擇的 hello 提供者，並注意 hello hello 範圍選項。 您可以提供應用程式識別碼和應用程式密碼，以及快速啟用 hello 應用程式的 Facebook 驗證。 hello Azure 入口網站啟用驗證做為應用程式的周全的解決方案。
    
     ![image67][image67]
13. 移回 toohello 設定 刀鋒視窗，然後選擇使用者 hello 資源管理類別之下。
    
     ![image68][image68]
14. 在上 hello 右 hello 刀鋒視窗中檢查 hello 新增角色和使用者的各種選項。 hello Azure 入口網站可讓您輕鬆地 hello 應用程式，控制 RBAC （角色型存取控制）。
    
     ![image69][image69]

## <a name="summary"></a>摘要
本教學課程所示範一些 hello 電源以 hello Azure 平台快速啟用 web 應用程式中的連續部署，執行各種開發和測試活動、 監視與疑難排解即時應用程式，以及最後管理金鑰例如災害復原、 識別和以角色為基礎的存取控制策略。 hello Azure 平台可讓這些 DevOps 工作流程中，整合式的體驗，可有效率地在 hello 工作的內容中。

## <a name="next-steps"></a>後續步驟
* Azure 資源管理員是很重要的 hello Azure 平台上啟用 DevOps。  toolearn 更造訪[Azure 資源管理員概觀](../azure-resource-manager/resource-group-overview.md)。
* 關於 Azure App Service 部署，請瀏覽的 toolearn[部署您的應用程式 tooAzure 應用程式服務](../app-service-web/web-sites-deploy.md)

[image1]: ./media/tutorial-azureportal-devops/image1.png
[image2]: ./media/tutorial-azureportal-devops/image2.png
[image3]: ./media/tutorial-azureportal-devops/image3.png
[image4]: ./media/tutorial-azureportal-devops/image4.png
[image5]: ./media/tutorial-azureportal-devops/image5.png
[image6]: ./media/tutorial-azureportal-devops/image6.png
[image7]: ./media/tutorial-azureportal-devops/image7.png
[image8]: ./media/tutorial-azureportal-devops/image8.png
[image9]: ./media/tutorial-azureportal-devops/image9.png
[image10]: ./media/tutorial-azureportal-devops/image10.png
[image11]: ./media/tutorial-azureportal-devops/image11.png
[image12]: ./media/tutorial-azureportal-devops/image12.png
[image13]: ./media/tutorial-azureportal-devops/image13.png
[image14]: ./media/tutorial-azureportal-devops/image14.png
[image15]: ./media/tutorial-azureportal-devops/image15.png
[image16]: ./media/tutorial-azureportal-devops/image16.png
[image17]: ./media/tutorial-azureportal-devops/image17.png
[image18]: ./media/tutorial-azureportal-devops/image18.png
[image19]: ./media/tutorial-azureportal-devops/image19.png
[image20]: ./media/tutorial-azureportal-devops/image20.png
[image21]: ./media/tutorial-azureportal-devops/image21.png
[image22]: ./media/tutorial-azureportal-devops/image22.png
[image23]: ./media/tutorial-azureportal-devops/image23.png
[image24]: ./media/tutorial-azureportal-devops/image24.png
[image25]: ./media/tutorial-azureportal-devops/image25.png
[image26]: ./media/tutorial-azureportal-devops/image26.png
[image27]: ./media/tutorial-azureportal-devops/image27.png
[image28]: ./media/tutorial-azureportal-devops/image28.png
[image29]: ./media/tutorial-azureportal-devops/image29.png
[image30]: ./media/tutorial-azureportal-devops/image30.png
[image31]: ./media/tutorial-azureportal-devops/image31.png
[image32]: ./media/tutorial-azureportal-devops/image32.png
[image33]: ./media/tutorial-azureportal-devops/image33.png
[image34]: ./media/tutorial-azureportal-devops/image34.png
[image35]: ./media/tutorial-azureportal-devops/image35.png
[image36]: ./media/tutorial-azureportal-devops/image36.png
[image37]: ./media/tutorial-azureportal-devops/image37.png
[image38]: ./media/tutorial-azureportal-devops/image38.png
[image39]: ./media/tutorial-azureportal-devops/image39.png
[image40]: ./media/tutorial-azureportal-devops/image40.png
[image41]: ./media/tutorial-azureportal-devops/image41.png
[image42]: ./media/tutorial-azureportal-devops/image42.png
[image43]: ./media/tutorial-azureportal-devops/image43.png
[image44]: ./media/tutorial-azureportal-devops/image44.png
[image45]: ./media/tutorial-azureportal-devops/image45.png
[image46]: ./media/tutorial-azureportal-devops/image46.png
[image47]: ./media/tutorial-azureportal-devops/image47.png
[image48]: ./media/tutorial-azureportal-devops/image48.png
[image49]: ./media/tutorial-azureportal-devops/image49.png
[image50]: ./media/tutorial-azureportal-devops/image50.png
[image51]: ./media/tutorial-azureportal-devops/image51.png
[image52]: ./media/tutorial-azureportal-devops/image52.png
[image53]: ./media/tutorial-azureportal-devops/image53.png
[image54]: ./media/tutorial-azureportal-devops/image54.png
[image55]: ./media/tutorial-azureportal-devops/image55.png
[image56]: ./media/tutorial-azureportal-devops/image56.png
[image57]: ./media/tutorial-azureportal-devops/image57.png
[image58]: ./media/tutorial-azureportal-devops/image58.png
[image59]: ./media/tutorial-azureportal-devops/image59.png
[image60]: ./media/tutorial-azureportal-devops/image60.png
[image61]: ./media/tutorial-azureportal-devops/image61.png
[image62]: ./media/tutorial-azureportal-devops/image62.png
[image63]: ./media/tutorial-azureportal-devops/image63.png
[image64]: ./media/tutorial-azureportal-devops/image64.png
[image65]: ./media/tutorial-azureportal-devops/image65.png
[image66]: ./media/tutorial-azureportal-devops/image66.png
[image67]: ./media/tutorial-azureportal-devops/image67.png
[image68]: ./media/tutorial-azureportal-devops/image68.png
[image69]: ./media/tutorial-azureportal-devops/image69.png
