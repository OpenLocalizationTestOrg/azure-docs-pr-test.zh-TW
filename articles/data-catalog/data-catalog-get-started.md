---
title: "以資料目錄啟動 aaaGet |Microsoft 文件"
description: "端對端教學課程呈現 hello 案例和功能的 Azure 資料目錄。"
documentationcenter: 
services: data-catalog
author: steelanddata
manager: jhubbard
editor: 
tags: 
ms.assetid: 03332872-8d84-44a0-8a78-04fd30e14b18
ms.service: data-catalog
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/03/2017
ms.author: spelluru
ms.openlocfilehash: 7652918b5a8254f5cff9e32d77b1fd3e1bf59d59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-catalog"></a>開始使用 Azure 資料目錄
Azure 資料目錄是受到完整管理的雲端服務，可作為企業資料資產的註冊系統和探索系統。 如需詳細的概觀，請參閱 [什麼是 Azure 資料目錄](data-catalog-what-is-data-catalog.md)。

本教學課程可協助您開始使用 Azure 資料目錄。 您執行下列程序，在此教學課程中的 hello:

| 程序 | 說明 |
|:--- |:--- |
| [佈建資料目錄](#provision-data-catalog) |在此程序中，您會佈建或設定 Azure 資料目錄。 只有當 hello 類別目錄具有尚未設定之前，您可以執行此步驟。 即使您有多個與 Azure 帳戶相關聯的訂用帳戶，每個組織仍只能有一個資料目錄 (Microsoft Azure Active Directory 網域)。 |
| [註冊資料資產](#register-data-assets) |在此程序，透過 hello 資料目錄註冊 hello AdventureWorks2014 範例資料庫中的資料資產。 註冊是解壓縮金鑰結構化中繼資料，例如名稱、 類型和位置 hello 資料來源，並複製該中繼資料 toohello 目錄 hello 程序。 hello 資料來源和資料資產保留位置，但是 hello 中繼資料由 hello 目錄 toomake 他們更輕鬆地探索及可了解。 |
| [探索資料資產](#discover-data-assets) |在此程序，您可以使用 hello Azure 資料目錄入口網站 toodiscover 資料資產 hello 上一個步驟中註冊。 資料來源已向 Azure 資料目錄之後，它的中繼資料是以編製索引 hello 服務，讓使用者可以輕鬆地搜尋 hello 所需的資料。 |
| [註解資料資產](#annotate-data-assets) |在此程序，您提供註解 （例如描述、 標記、 文件或專家資訊） 的 hello 資料資產。 此資訊補充 hello hello 資料來源，從擷取的中繼資料和 toomake hello 資料來源的更多容易了解 toomore 人。 |
| [連接 toodata 資產](#connect-to-data-assets) |在此程序中，您會在整合式用戶端工具 (例如 Excel 和 SQL Server Data Tools) 和非整合式工具 (SQL Server Management Studio) 中開啟資料資產。 |
| [管理資料資產](#manage-data-assets) |在此程序中，您會設定資料資產的安全性。 資料目錄並不會提供使用者存取 toohello 資料本身。 hello hello 資料來源的擁有者可以控制資料存取。 <br/><br/> 您可以使用資料目錄探索資料來源和檢視 hello**中繼資料**相關 toohello 來源 hello 目錄中註冊。 可能的情況下，不過，其中資料來源應該是可見的唯一 toospecific 使用者或特定群組的 toomembers。 針對這些案例，您可以使用資料目錄註冊的資料資產中的 hello 資產您擁有 hello 類別目錄和控制項 hello 可視性 tootake 擁有權。 |
| [移除資料資產](#remove-data-assets) |在此程序，您學會如何從 tooremove 資料資產 hello 資料目錄。 |

## <a name="tutorial-prerequisites"></a>教學課程的必要條件
### <a name="azure-subscription"></a>Azure 訂閱
tooset 安裝 Azure 資料目錄，您必須是 hello 擁有者或共同擁有者的 Azure 訂用帳戶。

Azure 訂用帳戶可協助您組織存取 toocloud 服務資源，例如 Azure 資料目錄。 它們也可協助您控制如何根據資源使用量產生報告、計費及付費。 每一個訂用帳戶可以有不同的計費和付款設定，因此，依照部門、專案、區域辦事處等，您可以有不同的訂用帳戶和不同的計劃。 每個雲端服務所屬 tooa 訂用帳戶，並需要 toohave 訂用帳戶，才能安裝 Azure 資料目錄設定。 詳細資訊，請參閱 toolearn[管理帳戶、 訂用帳戶及管理角色](../active-directory/active-directory-how-subscriptions-associated-directory.md)。

如果您沒有訂用帳戶，則只需要幾分鐘的時間就可以建立免費試用帳戶。 請參閱 [免費試用](https://azure.microsoft.com/pricing/free-trial/) 以取得詳細資訊。

### <a name="azure-active-directory"></a>Azure Active Directory
tooset 安裝 Azure 資料目錄，您必須登入 Azure Active Directory (Azure AD) 使用者帳戶。 您必須是 hello 擁有者或共同擁有者的 Azure 訂用帳戶。  

Azure AD 會提供簡單的方法，以您的商務 toomanage 識別和存取，在 hello 雲端和內部部署。 您可以使用單一工作或學校帳戶 toosign tooany 雲端或內部部署 web 應用程式。 Azure 資料目錄會使用 Azure AD tooauthenticate 登入。 詳細資訊，請參閱 toolearn[什麼是 Azure Active Directory](../active-directory/active-directory-whatis.md)。

### <a name="azure-active-directory-policy-configuration"></a>Azure Active Directory 原則組態
其中您可以登入 toohello Azure 資料目錄入口網站，但當您嘗試 toosign toohello 資料來源註冊工具中的，您可能會遇到的情況，您會遇到錯誤訊息，讓您無法登入。 要在 hello 公司網路，或當您從外部 hello 公司網路連線時，可能會發生這個錯誤。

hello 註冊工具會使用*表單驗證*toovalidate 使用者登入對 Azure Active Directory。 成功登入時，Azure Active Directory 系統管理員必須啟用表單驗證在 hello*通用驗證原則*。

Hello 通用驗證原則，您可以啟用個別驗證內部網路和外部網路連線，hello 下列影像所示。 如果要連線的 hello 網路不啟用表單驗證，可能會發生登入錯誤。

 ![Azure Active Directory 全域驗證原則](./media/data-catalog-prerequisites/global-auth-policy.png)

如需詳細資訊，請參閱 [設定驗證原則](https://technet.microsoft.com/library/dn486781.aspx)。

## <a name="provision-data-catalog"></a>佈建資料目錄
每個組織只能佈建一個資料目錄 (Azure Active Directory 網域)。 因此，如果 hello 擁有者或隸屬 toothis Azure Active Directory 網域的 Azure 訂用帳戶的共同擁有者已經建立類別目錄，就能 toocreate 類別目錄再次即使您有多個 Azure 訂用帳戶。 tootest 是否已建立您的 Azure Active Directory 網域中的使用者資料目錄進行 toohello [Azure 資料目錄首頁](http://azuredatacatalog.com)並確認您是否看見 hello 類別目錄。 如果已經為您建立目錄，請略過下列程序，然後移至 toohello 下一節的 hello。    

1. 移 toohello[資料目錄服務] 頁面](https://azure.microsoft.com/services/data-catalog)按一下**開始**。
   
    ![Azure 資料目錄--行銷登陸頁面](media/data-catalog-get-started/data-catalog-marketing-landing-page.png)
2. 使用 hello 擁有者或共同擁有者的 Azure 訂用帳戶的使用者帳戶登入。 您會看到下列頁面，在登入後的 hello。
   
    ![Azure 資料目錄--佈建資料目錄](media/data-catalog-get-started/data-catalog-create-azure-data-catalog.png)
3. 指定**名稱**hello 資料類別目錄，hello**訂用帳戶**toouse，並將這些 hello**位置**hello 類別目錄。
4. 展開 [價格]，並選取 Azure 資料目錄的**版本** (免費或標準)。
    ![Azure 資料目錄--選取版本](media/data-catalog-get-started/data-catalog-create-catalog-select-edition.png)
5. 展開**目錄使用者**按一下**新增**tooadd hello 資料目錄使用者。 您會自動加入 toothis 群組。
    ![Azure 資料目錄--使用者](media/data-catalog-get-started/data-catalog-add-catalog-user.png)
6. 展開**目錄系統管理員**按一下**新增**tooadd hello 資料目錄的其他系統管理員。 您會自動加入 toothis 群組。
    ![Azure 資料目錄--系統管理員](media/data-catalog-get-started/data-catalog-add-catalog-admins.png)
7. 按一下**建立類別目錄**toocreate hello 資料目錄，為您的組織。 在建立後，您會看到 hello 資料目錄的 hello 首頁。
    ![Azure 資料目錄--已建立](media/data-catalog-get-started/data-catalog-created.png)    

### <a name="find-a-data-catalog-in-hello-azure-portal"></a>在 [hello Azure 入口網站中尋找資料目錄
1. 個別索引標籤上 hello 網頁瀏覽器中，或在個別的網頁瀏覽器視窗，請移 toohello [Azure 入口網站](https://portal.azure.com)和登入的 hello 相同的帳戶，您使用的 toocreate hello 資料目錄 hello 上一個步驟中。
2. 依序選取 [瀏覽]，然後按一下 [資料目錄]。
   
    ![Azure 資料目錄-瀏覽 Azure](media/data-catalog-get-started/data-catalog-browse-azure-portal.png)看到 hello 目錄您所建立的資料。
   
    ![Azure 資料目錄--檢視清單中的目錄](media/data-catalog-get-started/data-catalog-azure-portal-show-catalog.png)
3. 按一下您所建立的 hello 類別目錄。 您會看到 hello**資料目錄**hello 入口網站中的刀鋒視窗。
   
   ![Azure 資料目錄--入口網站中的刀鋒視窗 ](media/data-catalog-get-started/data-catalog-blade-azure-portal.png)
4. 您可以檢視 hello 資料目錄的屬性並加以更新。 例如，按一下**定價層**和 hello 版本變更。
   
    ![Azure 資料目錄--定價層](media/data-catalog-get-started/data-catalog-change-pricing-tier.png)

### <a name="adventure-works-sample-database"></a>Adventure Works 範例資料庫
在本教學課程中，您的 SQL Server Database Engine，hello hello AdventureWorks2014 範例資料庫中註冊資料資產 （資料表），但如果您想使用 toowork 熟悉且相關 tooyour 角色的資料，您可以使用任何支援的資料來源。 如需支援的資料來源清單，請參閱 [支援的資料來源](data-catalog-dsr.md)。

### <a name="install-hello-adventure-works-2014-oltp-database"></a>安裝 hello Adventure Works 2014 OLTP 資料庫
hello Adventure Works 資料庫支援家虛構自行車製造商 (Adventure Works Cycles)，其中包含產品、 銷售和購買的標準線上交易處理案例。 在本教學課程中，您會在 Azure 資料目錄中註冊產品資訊。

tooinstall hello Adventure Works 範例資料庫：

1. 下載 CodePlex 上的 [Adventure Works 2014 Full Database Backup.zip](https://msftdbprodsamples.codeplex.com/downloads/get/880661) 。
2. toorestore hello 資料庫上您的電腦，請依照下列中的 hello 指示[使用 SQL Server Management Studio 還原資料庫備份](http://msdn.microsoft.com/library/ms177429.aspx)，或依照下列步驟：
   1. 開啟 SQL Server Management Studio 並連接 toohello SQL Server Database Engine。
   2. 以滑鼠右鍵按一下 [資料庫]，然後按一下 [還原資料庫]。
   3. 在下**Restore Database**，按一下 hello**裝置**選項**來源**按一下**瀏覽**。
   4. 在 [選取備份裝置] 之下，按一下 [新增]。
   5. 您擁有 hello 移 toohello 資料夾**AdventureWorks2014.bak**檔案、 選取 hello 檔案，然後按一下**確定**tooclose hello**尋找備份檔案**] 對話方塊。
   6. 按一下**確定**tooclose hello**選取備份裝置**] 對話方塊。    
   7. 按一下**確定**tooclose hello **Restore Database** ] 對話方塊。

您現在可以使用 Azure 資料目錄註冊 hello Adventure Works 範例資料庫中的資料資產。

## <a name="register-data-assets"></a>註冊資料資產
在此練習中，您可以使用 hello 註冊工具 tooregister 資料資產 hello Adventure Works 資料庫中的與 hello 類別目錄。 註冊是 hello 資料來源和 hello 資產、 包含從擷取索引鍵的結構化中繼資料，例如名稱、 類型和位置，並複製該中繼資料 toohello 目錄 hello 程序。 hello 資料來源和資料資產保留位置，但是 hello 中繼資料由 hello 目錄 toomake 他們更輕鬆地探索及可了解。

### <a name="register-a-data-source"></a>註冊資料來源
1. 移 toohello [Azure 資料目錄首頁](http://azuredatacatalog.com)按一下**發行資料**。
   
   ![Azure 資料目錄--發佈資料按鈕](media/data-catalog-get-started/data-catalog-publish-data.png)
2. 按一下**啟動應用程式**toodownload、 安裝和執行的 hello 註冊工具，在您的電腦上。
   
   ![Azure 資料目錄--啟動按鈕](media/data-catalog-get-started/data-catalog-launch-application.png)
3. 在 [hello ** 褖畫惎**頁面上，按一下**登入**並輸入您的認證。     
   
    ![Azure 資料目錄--歡迎使用頁面](media/data-catalog-get-started/data-catalog-welcome-dialog.png)
4. 在 [hello **Microsoft Azure 資料目錄**頁面上，按一下**SQL Server**和**下一步**。
   
    ![Azure 資料目錄--資料來源](media/data-catalog-get-started/data-catalog-data-sources.png)
5. 輸入 hello SQL Server 的連接屬性**AdventureWorks2014** （請參閱下列範例中的 hello） 按一下**連接**。
   
   ![Azure 資料目錄--SQL Server 連線設定](media/data-catalog-get-started/data-catalog-sql-server-connection.png)
6. 註冊資料資產的 hello 中繼資料。 此範例中，在您註冊**生產/產品**hello AdventureWorks 生產命名空間中的物件：
   
   1. 在 hello**伺服器階層**樹狀目錄中，展開 [ **AdventureWorks2014**按一下**生產**。
   2. 按住 CTRL 鍵並按一下滑鼠，選取 [Product]、[ProductCategory]、[ProductDescription] 和 [ProductPhoto]。
   3. 按一下 hello**移動選取的箭頭**(**>**)。 這個動作會將所有選取的物件移至 hello**註冊物件 toobe**清單。
      
      ![Azure 資料目錄教學課程--瀏覽並選取物件](media/data-catalog-get-started/data-catalog-server-hierarchy.png)
   4. 選取**包括預覽**tooinclude hello 資料的快照集預覽。 hello 快照集包含每個資料表中，從 too20 記錄，它會複製到 hello 類別目錄。
   5. 選取**包含資料設定檔**tooinclude hello 資料設定檔的 hello 物件統計資料的快照集 (例如： 資料行的資料列數目的最小、 最大和平均值)。
   6. 在 [hello**將標記加入**欄位中，輸入**adventure 的運作方式，循環**。 此動作會新增這些資料資產的搜尋標籤。 標記是 toohelp 使用者尋找已註冊的資料來源的好方法。
   7. 指定 hello 名稱**專家**（選擇性） 此資料。
      
      ![Azure 資料目錄教學課程--物件 toobe 註冊](media/data-catalog-get-started/data-catalog-objects-register.png)
   8. 按一下 [註冊] 。 Azure 資料目錄會註冊您選取的物件。 在此練習中，會註冊從 Adventure Works hello 選取物件。 hello 註冊工具會從 hello 資料資產中擷取中繼資料，並將該資料複製到 hello Azure 資料目錄服務。 hello 資料仍會保留它目前位於何處，而且仍在 hello hello 系統管理員控制與 hello 目前系統的原則。
      
      ![Azure 資料目錄--已註冊的物件](media/data-catalog-get-started/data-catalog-registered-objects.png)
   9. 您已註冊的資料來源物件中，按一下 [toosee**檢視入口網站**。 在 [hello Azure 資料目錄入口網站中，確認您看到所有四個資料表和 hello hello 方格檢視中的資料庫。
      
      ![Hello Azure 資料目錄入口網站中的物件 ](media/data-catalog-get-started/data-catalog-view-portal.png)

在此練習中，您會註冊 hello Adventure Works 範例資料庫中的物件，讓他們可以輕鬆地找到使用者整個組織。 在 [hello 下一個練習中，您學會 toodiscover 註冊資料資產的方式。

## <a name="discover-data-assets"></a>探索資料資產
在 Azure 資料目錄探索資料會使用兩種主要機制：搜尋和篩選。

搜尋是設計的 toobe 直覺式且功能強大。 根據預設，搜尋詞彙會比對 hello 類別目錄，包括使用者提供的註解中的任何內容。

篩選設計 toocomplement 搜尋。 您可以選取特定的特性，例如專家、 資料來源類型、 物件類型和標記 tooview 相符的資料資產和 tooconstrain 搜尋結果 toomatching 資產。

藉由使用搜尋和篩選的組合，您可以快速瀏覽 hello 已經向 Azure 資料目錄 toodiscover hello 資料資產您需要的資料來源。

在此練習中，您可以使用您在上一個練習中 hello 註冊 hello Azure 資料目錄入口網站 toodiscover 資料資產。 如需搜尋語法的詳細資料，請參閱 [資料目錄搜尋語法參考](https://msdn.microsoft.com/library/azure/mt267594.aspx) 。

下列是用來探索 hello 目錄中的資料資產的一些範例。  

### <a name="discover-data-assets-with-basic-search"></a>利用基本搜尋探索資料資產
基本搜尋可協助您使用一或多個搜尋字詞搜尋目錄。 結果是任何比對任何屬性與一或多個指定的 hello 詞彙的資產。

1. 按一下**首頁**hello Azure 資料目錄入口網站中。 如果您關閉 hello 網頁瀏覽器，請移至 toohello [Azure 資料目錄首頁](https://www.azuredatacatalog.com)。
2. 在 [hello] 搜尋方塊中，輸入`cycles`按**ENTER**。
   
    ![Azure 資料目錄--基本文字搜尋](media/data-catalog-get-started/data-catalog-basic-text-search.png)
3. 確認您看到所有四個資料表和 hello (AdventureWorks2014 資料庫） hello 結果中。 您可以切換**格線檢視**和**清單檢視**按鈕，即可在 [hello] 工具列上 hello 下列影像所示。 請注意該 hello 搜尋關鍵字，會反白顯示 hello 搜尋結果中因為 hello**反白顯示**選項**ON**。 您也可以指定 hello 數目**每頁搜尋結果**搜尋結果中。
   
    ![Azure 資料目錄--基本文字搜尋結果](media/data-catalog-get-started/data-catalog-basic-text-search-results.png)
   
    hello**搜尋**面板是上剩餘的 hello 與 hello**屬性**] 面板就會在右邊的 hello。 在 [hello**搜尋**面板中，您可以變更搜尋準則，篩選結果。 hello**屬性**面板會顯示 hello 方格或清單中的所選物件的屬性。
4. 按一下**產品**hello 搜尋結果中。 按一下 hello**預覽**，**資料行**，**資料設定檔**，和**文件**索引標籤，或按一下 hello 箭號 tooexpand hello 下方窗格。  
   
    ![Azure 資料目錄--底部窗格](media/data-catalog-get-started/data-catalog-data-asset-preview.png)
   
    在 [hello**預覽**索引標籤上，將看見 hello hello 資料預覽**產品**資料表。  
5. 按一下 hello**資料行**toofind 資料行的詳細資料索引標籤上 (例如**名稱**和**資料型別**) hello 資料資產中。
6. 按一下 hello**資料設定檔**toosee hello 程式碼剖析資料的索引標籤 (例如： 數字的資料列、 資料或資料行中的最小值的大小) hello 資料資產中。
7. 使用篩選 hello 結果**篩選**hello 左側。 例如，按一下**資料表**的**物件型別**，而且您看到只有 hello 四個資料表不 hello 資料庫。
   
    ![Azure 資料目錄--篩選搜尋結果](media/data-catalog-get-started/data-catalog-filter-search-results.png)

### <a name="discover-data-assets-with-property-scoping"></a>利用屬性範圍探索資料資產
指定屬性的範圍可協助您探索會 hello 與比對 hello 搜尋詞彙的資料資產的屬性。

1. 清除 hello**資料表**下篩選**物件型別**中**篩選**。  
2. 在 [hello] 搜尋方塊中，輸入`tags:cycles`按**ENTER**。 請參閱[資料類別目錄搜尋語法參考](https://msdn.microsoft.com/library/azure/mt267594.aspx)針對所有 hello 搜尋 hello 資料目錄，您可以使用的屬性。
3. 確認您看到所有四個資料表和 hello (AdventureWorks2014 資料庫） hello 結果中。  
   
    ![資料目錄--屬性範圍搜尋結果](media/data-catalog-get-started/data-catalog-property-scoping-results.png)

### <a name="save-hello-search"></a>儲存 hello 搜尋
1. 在 [hello**搜尋**hello 窗格**目前搜尋**區段中輸入 hello 搜尋的名稱，然後按一下**儲存**。
   
    ![Azure 資料目錄--儲存搜尋](media/data-catalog-get-started/data-catalog-save-search.png)
2. 確認該 hello 儲存搜尋會顯示在**已儲存的搜尋**。
   
    ![Azure 資料目錄--已儲存的搜尋](media/data-catalog-get-started/data-catalog-saved-search.png)
3. 選取其中一個 hello hello 儲存搜尋，您可以採取的動作 (**重新命名**，**刪除**，**儲存為預設值**搜尋)。
   
    ![Azure 資料目錄--已儲存的搜尋選項](media/data-catalog-get-started/data-catalog-saved-search-options.png)

### <a name="boolean-operators"></a>布林運算子
您可以使用布林運算子來擴大或縮小搜尋範圍。

1. 在 [hello] 搜尋方塊中，輸入`tags:cycles AND objectType:table`，然後按**ENTER**。
2. 確認您看到只有資料表 （非 hello 資料庫） hello 結果中。  
   
    ![Azure 資料目錄--搜尋中的布林運算子](media/data-catalog-get-started/data-catalog-search-boolean-operator.png)

### <a name="grouping-with-parentheses"></a>使用括號分組
藉由加上括弧分組，您可以分組 hello 查詢 tooachieve 邏輯隔離，特別是以及布林運算子的部分。

1. 在 [hello] 搜尋方塊中，輸入`name:product AND (tags:cycles AND objectType:table)`按**ENTER**。
2. 確認您看到只有 hello**產品**hello 搜尋結果中的資料表。
   
    ![Azure 資料目錄--群組搜尋](media/data-catalog-get-started/data-catalog-grouping-search.png)   

### <a name="comparison-operators"></a>比較運算子
使用比較運算子，您可以針對具有數值和日期資料類型的屬性使用比較而非相等。

1. 在 [hello] 搜尋方塊中，輸入`lastRegisteredTime:>"06/09/2016"`。
2. 清除 hello**資料表**下篩選**物件型別**。
3. 按 **ENTER**鍵。
4. 確認您看到 hello**產品**， **ProductCategory**， **ProductDescription**，和**ProductPhoto**資料表和 hello您的搜尋結果中註冊 AdventureWorks2014 資料庫。
   
    ![Azure 資料目錄--比較搜尋結果](media/data-catalog-get-started/data-catalog-comparison-operator-results.png)

請參閱[如何 toodiscover 資料資產](data-catalog-how-to-discover.md)的探索資料資產的詳細資訊和[資料類別目錄搜尋語法參考](https://msdn.microsoft.com/library/azure/mt267594.aspx)搜尋語法。

## <a name="annotate-data-assets"></a>註解資料資產
在此練習中，您可以使用 hello Azure 資料目錄入口網站 tooannotate （加入資訊，例如描述、 標記或專家） 您先前已登錄在 hello 目錄中的資料資產。 hello 註解補充和增強 hello 註冊時擷取自 hello 資料來源的結構化中繼資料和更容易 toodiscover 讓 hello 資料資產，並了解。

在此練習中，您會註解單一資料資產 (ProductPhoto)。 您加入的易記名稱和描述 toohello ProductPhoto 資料資產。  

1. 移 toohello [Azure 資料目錄首頁](https://www.azuredatacatalog.com)並搜尋與`tags:cycles`toofind hello 資料資產，而您已經註冊。  
2. 按一下搜尋結果中的 **ProductPhoto** 。  
3. 輸入**產品映像**如**易記名稱**和**產品相片的行銷資料當中**hello**描述**。
   
    ![Azure 資料目錄--產品圖片描述](media/data-catalog-get-started/data-catalog-productphoto-description.png)
   
    hello**描述**可協助其他人探索和了解 toouse hello 原因和方式選取的資料資產。 您也可以新增更多的標記，並檢視資料行。 現在您可以嘗試使用 hello 描述性中繼資料的搜尋和篩選 toodiscover 資料資產加入 toohello 類別目錄。

您也可以執行 hello 遵循此頁面上：

* 新增 hello 資料資產的專家。 按一下**新增**在 hello**專家**區域。
* 將標記加入 hello 資料集層級。 按一下**新增**在 hello**標記**區域。 標記可以是使用者標記或詞彙標記。 hello 標準版本的資料類別目錄包含商務字彙可協助定義中央商務分類的類別目錄管理員。 目錄使用者接著可以為資料資產加上詞彙註解。 如需詳細資訊，請參閱[向上 tooset 來控管標記所 hello 的商務字彙](data-catalog-how-to-business-glossary.md)
* 將標記加入 hello 資料行層級。 按一下**新增**下**標記**想 tooannotate hello 資料行。
* 新增描述 hello 資料行層級。 輸入資料行的 [描述]  。 您也可以檢視從 hello 資料來源擷取的 hello 描述中繼資料。
* 新增**要求存取**toorequest 存取 toohello 資料資產的方式會顯示使用者的資訊。
  
    ![Azure 資料目錄--新增標記、描述](media/data-catalog-get-started/data-catalog-add-tags-experts-descriptions.png)
* 選擇 hello**文件**索引標籤並提供文件以 hello 資料資產。 您可以使用 Azure 資料目錄文件，您的資料類別目錄做為內容儲存機制 toocreate 完成旁白資料資產。
  
    ![Azure 資料目錄--文件索引標籤](media/data-catalog-get-started/data-catalog-documentation.png)

您也可以新增註解 toomultiple 資料資產。 例如，您可以選取所有您已註冊的 hello 資料資產，並指定它們的專家。

![Azure 資料目錄--註解多個資料資產](media/data-catalog-get-started/data-catalog-multi-select-annotate.png)

Azure 資料目錄支援擠徵方法 tooannotations。 任何資料目錄使用者可以加入標記 （使用者或詞彙） 描述，以及其他中繼資料，以便該檢視方塊擷取和使用 tooother 使用者，可以有任何具有資料資產和其使用檢視方塊的使用者。

請參閱[如何 tooannotate 資料資產](data-catalog-how-to-annotate.md)的註解的資料資產的詳細資訊。

## <a name="connect-toodata-assets"></a>連接 toodata 資產
在本練習中，您會使用連線資訊，在整合式用戶端工具 (Excel) 和非整合式工具 (SQL Server Management Studio) 中開啟資料資產。

> [!NOTE]
> 請務必 tooremember，Azure 資料目錄不會讓您存取 toohello 實際的資料來源，它只是讓更方便您 toodiscover 且容易了解。 當您連接 tooa 資料來源時，hello 您選擇的使用您的 Windows 認證或提示您輸入認證，視用戶端應用程式。 如果您先前尚未獲得存取 toohello 資料來源，您會需要 toobe 授與存取權，才能連線。
> 
> 

### <a name="connect-tooa-data-asset-from-excel"></a>從 Excel 連接 tooa 資料資產
1. 選取搜尋結果中的 **Product** 。 按一下**開啟於**hello 工具列，並按一下上**Excel**。
   
    ![Azure 資料目錄-連接 toodata 資產](media/data-catalog-get-started/data-catalog-connect1.png)
2. 按一下**開啟**hello 下載快顯視窗中。 這項體驗可能會根據 hello 瀏覽器而有所不同。
   
    ![Azure 資料目錄--下載 Excel 連線檔案](media/data-catalog-get-started/data-catalog-download-open.png)
3. 在 [hello **Microsoft Excel 安全性注意事項**視窗中，按一下 [**啟用**。
   
    ![Azure 資料目錄--Excel 安全性快顯視窗](media/data-catalog-get-started/data-catalog-excel-security-popup.png)
4. 在 hello 保留 hello 預設**匯入資料**對話方塊，按一下**確定**。
   
    ![Azure 資料目錄--Excel 匯入資料](media/data-catalog-get-started/data-catalog-excel-import-data.png)
5. 在 Excel 中 hello 資料來源檢視。
   
    ![Azure 資料目錄--Excel 中的產品資料表](media/data-catalog-get-started/data-catalog-connect2.png)

在此練習中，您可以連接 toodata 使用 Azure 資料目錄所探索到的資產。 Hello Azure 資料目錄入口網站，您可以直接使用連接 hello 用戶端應用程式整合至 hello**中開啟**功能表。 您也可以連接與您選擇使用 hello 連接位置資訊 hello 資產中繼資料中包含任何應用程式。 例如，您可以使用 SQL Server Management Studio tooconnect toohello AdventureWorks2014 資料庫 tooaccess hello 資料在本教學課程中註冊的 hello 資料資產。

1. 開啟 **SQL Server Management Studio**。
2. 在 [hello**連接 tooServer**對話方塊方塊中，輸入 hello hello 伺服器名稱**屬性**hello Azure 資料目錄入口網站中的窗格。
3. 使用適當的驗證和認證 tooaccess hello 資料資產。 如果您沒有存取權，使用 hello 資訊**要求存取**欄位 tooget 它。
   
    ![Azure 資料目錄--要求存取](media/data-catalog-get-started/data-catalog-request-access.png)

按一下**檢視連接字串**tooview 和複製 ADF.NET、 ODBC 和 OLEDB 連接字串 toohello 剪貼簿用於您的應用程式。

## <a name="manage-data-assets"></a>管理資料資產
在此步驟中，您會看到如何 tooset 了資料資產的安全性。 資料目錄並不會提供使用者存取 toohello 資料本身。 hello hello 資料來源的擁有者可以控制資料存取。

您可以使用資料目錄 toodiscover 資料來源以及 tooview hello 中繼資料相關的 hello 目錄中註冊的 toohello 來源。 可能的情況下，不過，資料來源只應該儲存可見 toospecific 使用者或特定群組的 toomembers。 針對這些案例，您可以使用資料目錄 tootake 擁有 hello 目錄中註冊的資料資產和您擁有 hello 資產的 toothen 控制 hello 可見性。

> [!NOTE]
> 在這個練習中所述的 hello 管理功能僅適用於 hello 標準版本的 Azure 資料目錄，不在 hello 免費版本。
> 在 Azure 資料目錄中，您可以使用的資料資產的擁有權、 新增共同擁有者 toodata 資產，並設定的資料資產的 hello 可見性。
> 
> 

### <a name="take-ownership-of-data-assets-and-restrict-visibility"></a>取得資料資產的擁有權及限制可見性
1. 移 toohello [Azure 資料目錄首頁](https://www.azuredatacatalog.com)。 在 [hello**搜尋**文字方塊中，輸入`tags:cycles`按**ENTER**。
2. 按一下 hello 結果清單中的項目，然後按一下**Take Ownership** hello 工具列上。
3. 在 [hello**管理**hello 區段**屬性**] 面板中，按一下 [ **Take Ownership**。
   
    ![Azure 資料目錄--取得擁有權](media/data-catalog-get-started/data-catalog-take-ownership.png)
4. toorestrict 可見性，選擇**擁有者與這些使用者**在 hello**可視性**區段，然後按一下**新增**。 輸入使用者電子郵件地址中 hello 文字的方塊，然後按**ENTER**。
   
    ![Azure 資料目錄--限制存取](media/data-catalog-get-started/data-catalog-ownership.png)

## <a name="remove-data-assets"></a>移除資料資產
在此練習中，您可以使用 hello Azure 資料目錄入口網站 tooremove 預覽資料，從已註冊的資料資產，並從 hello 類別目錄中刪除資料資產。

在 Azure 資料目錄中，您可以刪除個別資產或多個資產。

1. 移 toohello [Azure 資料目錄首頁](https://www.azuredatacatalog.com)。
2. 在 [hello**搜尋**文字方塊中，輸入`tags:cycles`按一下**ENTER**。
3. Hello 結果清單中選取項目，然後按一下**刪除**hello 工具列 hello 下列影像所示：
   
    ![Azure 資料目錄--刪除資料格項目](media/data-catalog-get-started/data-catalog-delete-grid-item.png)
   
    如果您使用 hello 清單檢視，hello 核取方塊會是 hello 項目的 toohello 左邊 hello 下列影像所示：
   
    ![Azure 資料目錄--刪除清單項目](media/data-catalog-get-started/data-catalog-delete-list-item.png)
   
    您也可以選擇多個資料資產，並刪除 hello 下列影像所示：
   
    ![Azure 資料目錄--刪除多個資料資產](media/data-catalog-get-started/data-catalog-delete-assets.png)

> [!NOTE]
> hello hello 目錄的預設行為是 tooallow 任何使用者 tooregister 任何資料來源與 tooallow 任何使用者 toodelete 尚未註冊任何資料資產。 包含在 hello 標準版本的 Azure 資料目錄中的 hello 管理功能提供其他選項取得擁有權的資產，限制誰可以探索資產，以及限制可以刪除資產。
> 
> 

## <a name="summary"></a>摘要
在本教學課程中，您已瀏覽 Azure 資料目錄的基本功能，包括註冊、註解、探索和管理企業資料資產。 既然您已經完成 hello 教學課程，就開始 tooget 啟動。 註冊您和小組依賴，hello 資料來源，並邀請同事 toouse hello 類別目錄，您可以立即開始。

## <a name="references"></a>參考
* [如何 tooregister 資料資產](data-catalog-how-to-register.md)
* [如何 toodiscover 資料資產](data-catalog-how-to-discover.md)
* [如何 tooannotate 資料資產](data-catalog-how-to-annotate.md)
* [如何 toodocument 資料資產](data-catalog-how-to-documentation.md)
* [如何 tooconnect toodata 資產](data-catalog-how-to-connect.md)
* [如何 toomanage 資料資產](data-catalog-how-to-manage.md)

