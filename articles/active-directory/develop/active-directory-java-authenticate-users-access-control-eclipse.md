---
title: "aaaHow toouse 存取控制 (Java) |Microsoft 文件"
description: "深入了解如何使用 toodevelop 並用來控制存取 Java 在 Azure 中的。"
services: active-directory
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 247dfd59-0221-4193-97ec-4f3ebe01d3c7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.custom: aaddev
ms.openlocfilehash: cbbce3b1a05eabf3b86a8cb91db1bde92dbb8960
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooauthenticate-web-users-with-azure-access-control-service-using-eclipse"></a>如何 tooAuthenticate Eclipse 向 Azure 存取控制服務使用的 Web 使用者
本指南將說明如何 toouse hello 內 hello Azure Toolkit for Eclipse 的 Azure 存取控制服務 (ACS)。 如需有關 ACS 的詳細資訊，請參閱 hello[後續步驟](#next_steps)> 一節。

> [!NOTE]
> hello Azure 存取服務控制篩選是 community technology preview。 由於是發行前軟體，Microsoft 尚未提供正式支援。
> 
> 

## <a name="what-is-acs"></a>什麼是 ACS？
大部分開發人員都不是身分識別專家，因而通常不想花時間為其應用程式和服務開發驗證與授權機制。 ACS 是一項 Azure 服務可讓您輕鬆地驗證使用者需要 tooaccess web 應用程式和服務而不需要您的程式碼 toofactor 複雜驗證邏輯。

下列功能的 hello 可在 ACS 中：

* 與 Windows Identity Foundation (WIF) 整合。
* 支援熱門的 Web 身分識別提供者 (IP)，包括 Windows Live ID、Google、Yahoo! 和 Facebook。
* 支援 Active Directory Federation Services (AD FS) 2.0。
* 開放式資料通訊協定 (OData) 為基礎的管理服務，提供以程式設計方式存取 tooACS 設定。
* 管理入口網站，可讓系統管理存取權 toohello ACS 設定。

如需 ACS 的詳細資訊，請參閱[存取控制服務 2.0][Access Control Service 2.0]。

## <a name="concepts"></a>概念
Azure ACS 是建置在 hello 主體的宣告式身分識別-一致的方法 toocreating 驗證機制在內部部署執行的應用程式或 hello 雲端中。 宣告式身分識別提供應用程式和服務 tooacquire 識別所需的資訊在其他組織中，並在 hello 網際網路上其組織內部的使用者相關的常見方式。

本指南中的 toocomplete hello 工作，您應該了解下列概念的 hello:

**用戶端**-hello 這個如何 tooguide 內容中，這是正在嘗試 toogain 存取 tooyour web 應用程式的瀏覽器。

**信賴憑證者的合作對象 (RP) 應用程式**-RP 應用程式是網站或驗證 tooone 外部授權單位會將委派的服務。 在識別術語中，我們稱該 hello RP 信任該授權單位。 本指南說明如何 tooconfigure 您應用程式 tootrust ACS。

**權杖** - 權杖指的是一種安全性資料集合，通常會在順利驗證使用者時發出。 它包含一組*宣告*，hello 屬性驗證的使用者。 宣告可以代表使用者的名稱、使用者所屬角色的識別碼，或使用者的年紀等等。 通常以數位方式簽署權杖，這表示它永遠都能來源後 tooits 發行者和其內容無法進行竄改。 使用者獲得存取 tooa RP 應用程式出示有效的語彙基元 hello RP 應用程式信任授權單位所核發。

**身分識別提供者 (IP)** - IP 是負責驗證使用者身分識別並簽發安全性權杖的授權單位。 雖然特殊的服務呼叫安全性權杖服務 (STS)，被實作 hello 實際工作的發行語彙基元。 典型的 IP 範例包括 Windows Live ID、Facebook、商業使用者存放庫 (如 Active Directory) 等等。
設定的 tootrust IP ACS 時，將會接受 hello 系統，並驗證該 IP 所發出的權杖。 ACS 可以信任多個 Ip，這表示當您的應用程式信任 ACS 時，您可以立即提供您的應用程式 tooall hello 已驗證的使用者從所有 hello 代替您信任該 ACS 的 Ip。

**同盟提供者 (FP)** - IP 直接有使用者的資料，並會使用其認證來驗證他們，以及簽發關於其身分的宣告。 同盟提供者 (FP) 是不同種類的授權單位：不是直接驗證使用者，而是擔任一個 RP 與一個或多個 IP 之間的媒介和代理驗證。 IP 和 FP 都會簽發安全性權杖，因此它們都會使用 Security Token Services (STS)。 ACS 是一種 FP。

**ACS 規則引擎**-從受信任的 Ip tootokens 使用的 tootransform 連入權杖是供 hello RP toobe 編寫到簡單的表單中的 hello 邏輯宣告轉換規則。 ACS 以規則引擎為其特色，仔細套用您對 RP 所指定的任何轉換邏輯。

**ACS 命名空間** - 命名空間是您用於組織設定之 ACS 的最上層分割區。 命名空間保留一份您信任的 Ip，hello RP 應用程式想 tooserve，您預期的 hello 規則 hello 規則引擎 tooprocess 連入權杖，依此類推。 命名空間公開各種不同的端點將會由 hello 應用程式和開發人員 tooget ACS tooperform 其函式。

hello 如下圖所示 ACS 驗證與 web 應用程式的運作方式：

![ACS flow diagram][acs_flow]

1. hello 用戶端 （在這個案例中為瀏覽器） 向 hello RP 要求的頁面。
2. Hello 要求未經驗證，因為 hello RP 重新導向 hello 使用者 toohello 授權單位信任，也就是 ACS。 hello ACS，針對這個 RP 所指定的 Ip hello 選擇顯示 hello 使用者。 hello 使用者選取 hello 適當的 IP。
3. hello 用戶端 toohello IP 驗證 頁面上，瀏覽，並提示 hello 使用者 toolog 上。
4. Hello 用戶端驗證 （例如，輸入認證的 hello 身分識別） 之後，hello IP 簽發安全性權杖。
5. 發出安全性權杖後, hello IP 將重新導向 hello 用戶端 tooACS 並且 hello 用戶端會傳送 hello 安全性權杖發給 hello IP tooACS。
6. ACS 驗證 hello hello IP，輸入 hello 識別此權杖中宣告成 hello ACS 規則引擎、 計算 hello 輸出身分識別宣告，以及發出新的安全性權杖，其中包含這些輸出宣告所發出的安全性權杖。
7. ACS 會重新導向 hello 用戶端 toohello RP。 hello 用戶端傳送嗨 ACS toohello RP 所簽發新安全性權杖。 hello RP 驗證 hello hello ACS 所簽發的安全性權杖的簽章，會驗證此語彙基元中的 hello 宣告，並傳回原始要求的 hello 頁面。

## <a name="prerequisites"></a>必要條件
本指南中的 toocomplete hello 工作，您將需要 hello 下列：

* Java Developer Kit (JDK) 1.6 版或更新版本。
* Eclipse IDE for Java EE Developers (Indigo 或更新版本)。 這可透過 <http://www.eclipse.org/downloads/> 下載。 
* Java 型 Web 伺服器或應用程式伺服器的散發套件，例如 Apache Tomcat、GlassFish、JBoss Application Server 或 Jetty。
* Azure 訂用帳戶，可從 <http://www.microsoft.com/windowsazure/offers/> 取得。
* hello Azure Toolkit for Eclipse，2014 年 4 月版或更新版本。 如需詳細資訊，請參閱[安裝 hello Azure Toolkit for Eclipse](http://msdn.microsoft.com/library/windowsazure/hh690946.aspx)。
* 您的應用程式與 X.509 憑證 toouse。 您需要此憑證同時具有公開憑證 (.cer) 和 個人資訊交換 (.PFX) 格式。 (本教學課程稍後將描述建立此憑證的選項)。
* 熟悉 hello Azure 計算模擬器和部署技術討論[在 Eclipse 中建立 Azure 的 Hello World 應用程式](http://msdn.microsoft.com/library/windowsazure/hh690944.aspx)。

## <a name="create-an-acs-namespace"></a>建立 ACS 命名空間
toobegin 使用存取控制服務 (ACS)，在 Azure 中，您必須建立 ACS 命名空間。 hello 命名空間提供唯一的範圍，從您的應用程式內的 ACS 資源定址。

1. 登入 hello [Azure 管理入口網站][Azure Management Portal]。
2. 按一下 [Active Directory] 。 
3. toocreate 新的存取控制命名空間中，按一下**新增**，按一下 **應用程式服務**，按一下 **存取控制**，然後按一下**快速建立**. 
4. 輸入 hello 命名空間的名稱。 Azure 會確認該 hello 名稱是唯一的。
5. 選取 hello 區域中的 hello 使用命名空間。 Hello 獲得最佳效能，會使用您部署您的應用程式的 hello 區域。
6. 如果您有多個訂閱，選取要 toouse hello ACS 命名空間的 hello 訂用帳戶。
7. 按一下 [建立] 。

Azure 會建立並啟動 hello 命名空間。 等候 hello 新命名空間的 hello 狀態**Active**才能繼續。 

## <a name="add-identity-providers"></a>新增身分識別提供者
在這項工作，您可以加入 Ip toouse 與 RP 應用程式進行驗證。 針對示範用途，此工作會顯示 tooadd Windows Live IP，但您可以使用任何 hello hello ACS 管理入口網站中列出的 Ip。

1. 在 hello [Azure 管理入口網站][Azure Management Portal]，按一下  **Active Directory**選取存取控制命名空間，然後按一下**管理**。 hello ACS 管理入口網站隨即開啟。
2. 在 hello hello ACS 管理入口網站的左側瀏覽窗格中按一下**身分識別提供者**。
3. 依預設會啟用 Windows Live ID，而且無法刪除。 基於本教學課程的目的，只會使用 Windows Live ID。 此畫面，不過，是其中您可以加入其他 Ip 時，依序按一下 hello**新增** 按鈕。

現在已啟用 Windows Live ID 作為 ACS 命名空間的 IP。 接下來，您可以指定您的 Java web 應用程式 (toobe 稍後建立) 為 RP。

## <a name="add-a-relying-party-application"></a>新增信賴憑證者應用程式
在這項工作，請設定 ACS toorecognize Java web 應用程式為有效的 RP 應用程式。

1. 在 hello ACS 管理入口網站中，按一下 **信賴憑證者合作對象應用程式**。
2. 在 hello**信賴憑證者的合作對象應用程式**頁面上，按一下**新增**。
3. 在 hello**新增信賴憑證者應用程式**頁面上，執行下列 hello:
   
   1. 在**名稱**，hello RP hello 型別名稱。 基於本教學課程的目的，輸入 **Azure Web App**。
   2. 在 [模式] 中，選取 [手動輸入設定]。
   3. 在**領域**，適用於類型 hello URI toowhich hello 安全性 ACS 所簽發權杖。 針對此工作，輸入 **http://localhost:8080/**。
      ![Relying party realm for use in compute emulator][relying_party_realm_emulator]
   4. 在**傳回 URL，**類型 hello URL toowhich ACS 傳回 hello 安全性權杖。 針對此工作，輸入 **http://localhost:8080/MyACSHelloWorld/index.jsp**
      ![要在計算模擬器中使用的信賴憑證者傳回 URL][relying_party_return_url_emulator]
   5. 接受 hello hello 其餘 hello 欄位中的預設值。
4. 按一下 [儲存] 。

您現在已成功設定您的 Java web 應用程式在 hello Azure 計算模擬器中執行時 (在 http://localhost:8080/< /) toobe RP ACS 命名空間中。 接下來，建立 hello 規則，ACS 會使用 hello RP 的 tooprocess 宣告。

## <a name="create-rules"></a>建立規則
在這項工作，您會定義如何將宣告傳遞 Ip tooyour RP 從磁碟機的 hello 規則。 Hello 本指南的目的，我們將只設定 ACS toocopy hello 輸入的宣告類型和值直接在 hello 輸出權杖中，而不需要篩選，或修改它們。

1. 在 hello ACS 管理入口網站主頁面上，按一下 **規則群組**。
2. 在 hello**規則群組**頁面上，按一下**Azure Web 應用程式的預設規則群組**。
3. 在 hello**編輯規則群組**頁面上，按一下**產生**。
4. 在 hello**產生規則： Azure Web 應用程式的預設規則群組**頁面上，確定已核取 Windows Live ID，然後按一下**產生**。    
5. 在 hello**編輯規則群組**頁面上，按一下**儲存**。

## <a name="upload-a-certificate-tooyour-acs-namespace"></a>上傳憑證 tooyour ACS 命名空間
在這項工作，您上傳。將會使用的 toosign 權杖要求您的 ACS 命名空間所建立的 PFX 憑證。

1. 在 hello ACS 管理入口網站主頁面上，按一下 **憑證和金鑰**。
2. 在 hello**憑證和金鑰**頁面上，按一下**新增**上方**權杖簽署**。
3. 在 hello**新增權杖簽署憑證或金鑰**頁面：
   1. 在 hello**用於**區段中，按一下**信賴憑證者的合作對象應用程式**選取**Azure Web 應用程式**（此您先前設定做為應用程式信賴憑證者的合作對象的 hello 名稱）。
   2. 在 hello**類型**區段中，選取**X.509 憑證**。
   3. 在 hello**憑證**區段、 按一下 hello 瀏覽按鈕並瀏覽您想 toouse toohello X.509 憑證檔案。 這將為 .PFX 檔案。 選取 hello 檔案中，按一下**開啟**，然後輸入 hello 憑證密碼在 hello**密碼**文字方塊。 請注意，基於測試目的，您可能使用自我簽署憑證。 toocreate 自我簽署的憑證，使用 hello**新增**按鈕在 hello **ACS 篩選器程式庫**對話方塊 （稍後會說明），或使用 hello **encutil.exe** hello從公用程式[專案網站][ project website]的 hello Azure for Java 的入門套件。
   4. 確定已核取 [設為主要]。 您**新增權杖簽署憑證或金鑰**頁碼看起來類似 toohello 下列。
       ![新增權杖簽署憑證][add_token_signing_cert]
   5. 按一下**儲存**toosave 您設定及關閉 hello**新增權杖簽署憑證或金鑰**頁面。

接著，檢閱，您將需要 tooconfigure 您的 Java web 應用程式 toouse ACS hello 應用程式整合頁面上，並複製 hello URI 中的 hello 資訊。

## <a name="review-hello-application-integration-page"></a>檢閱 hello 應用程式整合頁面上
您可以找到所有 hello 資訊與 hello 程式碼需要 tooconfigure 您 Java web 應用程式 (hello RP 應用程式) toowork 與 ACS 在 hello 的 hello ACS 管理入口網站的應用程式整合頁面上。 設定 Java Web 應用程式進行結盟驗證時，您將需要此資訊。

1. 在 hello ACS 管理入口網站中，按一下 **應用程式整合**。  
2. 在 hello**應用程式整合**頁面上，按一下**登入頁面**。
3. 在 hello**登入頁面整合**頁面上，按一下**Azure Web 應用程式**。

在 hello**登入頁面整合： Azure Web 應用程式**頁面中所列的 hello URL**選項 1： 連結 tooan ACS 裝載登入頁面**將 Java web 應用程式中使用。 當您新增 hello Azure 存取控制服務篩選文件庫 tooyour Java 應用程式時，您將需要此值。

## <a name="create-a-java-web-application"></a>建立 Java Web 應用程式
1. 在 Eclipse 中，在 hello 功能表按一下**檔案**，按一下 **新增**，然後按一下**動態 Web 專案**。 (如果您沒有看到**動態 Web 專案**列為可用的專案，按一下後**檔案**，**新增**，請勿然後 hello 遵循： 按一下**檔案**，按一下**新增**，按一下 **專案**，依序展開**Web**，按一下**動態 Web 專案**，然後按一下**接下來**。)本教學課程的目的而言，專案的名稱，hello **MyACSHelloWorld**。 (請確定您使用此名稱，在本教學課程的後續步驟預期名為 MyACSHelloWorld 您 WAR 檔案 toobe)。 您的畫面會出現類似 toohello 下列：
   
    ![Create a Hello World project for ACS exampple][create_acs_hello_world]
   
    按一下 [完成] 。
2. 在 Eclipse 的專案總管檢視內，展開 **MyACSHelloWorld**。 在 WebContent 上按一下滑鼠右鍵、按一下 新增，然後按一下JSP 檔案。
3. 在 hello**新增 JSP 檔案**對話方塊中，名稱 hello 檔**index.jsp**。 請注意 hello 父資料夾為 MyACSHelloWorld/WebContent，hello 下列所示：
   
    ![Add a JSP file for ACS example][add_jsp_file_acs]
   
    按一下 [下一步] 。
4. 在 hello**選取 JSP 範本**對話方塊中，選取**新增 JSP 檔案 (html)**按一下**完成**。
5. Hello index.jsp 檔案開啟時在 Eclipse 中，增益集文字 toodisplay **ACS 您好 ！** 在現有的 hello`<body>`項目。 您已更新`<body>`內容應該會出現如下所示 hello:
   
        <body>
          <b><% out.println("Hello ACS World!"); %></b>
        </body>
   
    儲存 index.jsp。

## <a name="add-hello-acs-filter-library-tooyour-application"></a>新增 hello ACS 篩選器程式庫 tooyour 應用程式
1. 在 Eclipse 的 Project Explorer \(專案總管) 中，於 **MyACSHelloWorld** 上按一下滑鼠右鍵、按一下 Build Path \(組建路徑)，然後按一下Configure Build Path \(設定組建路徑)。
2. 在 hello **Java 組建路徑** 對話方塊中，按一下 hello**文件庫** 索引標籤。
3. 按一下 [新增程式庫] 。
4. 按一下 [Azure Access Control Services Filter (by MS Open Tech)] \(Azure 存取控制服務篩選器 (MS Open Tech 提供))，然後按 [Next] \(下一步)。 hello **Azure 存取控制服務篩選** 對話方塊隨即出現。  (hello**位置**欄位可能會有不同的路徑，根據您用來安裝 Eclipse 中，而且 hello 版本號碼可能會不同，視軟體更新。)
   
    ![Add ACS Filter library][add_acs_filter_lib]
5. 使用瀏覽器開啟 toohello**登入頁面整合**頁面 hello 管理入口網站中，複製 hello URL 列在 hello**選項 1： 連結 tooan ACS 裝載登入頁面**欄位，並將它貼到 hello **ACS 驗證端點**hello Eclipse 對話方塊的欄位。
6. 使用瀏覽器開啟 toohello**編輯信賴憑證者應用程式**頁面 hello 管理入口網站中，複製 hello URL 列在 hello**領域**欄位，並將它貼到 hello**信賴憑證者的合作對象領域** hello Eclipse 對話方塊的欄位。
7. Hello 內**安全性**hello Eclipse 對話方塊的區段，如果您想 toouse 現有的憑證，按一下**瀏覽**，瀏覽 toohello 憑證 toouse、 選取它，然後按一下**開啟**。 或者，如果您想 toocreate 新的憑證，請按一下**新增**toodisplay hello**新憑證** 對話方塊中，然後指定 hello 密碼、 hello.cer 檔案名稱，以及新的 hello 的 hello.pfx 檔案的名稱憑證。
8. 請檢查**hello WAR 檔案中的內嵌 hello 憑證**。 以這種方式內嵌 hello 憑證包含在您的部署，而不需要您 toomanually 加入它做為元件。 (如果改為您必須從您的 WAR 檔案外部儲存您的憑證，則您無法為角色元件加入 hello 憑證，並取消核取**hello WAR 檔案中的內嵌 hello 憑證**。)
9. [選用] 將 [Require HTTPS connections]  維持核取狀態。 如果您設定此選項時，您將需要 tooaccess 使用 hello HTTPS 通訊協定的應用程式。 如果您不想 toorequire HTTPS 連線，取消核取此選項。
10. 部署 toohello 計算模擬器中，您**Azure ACS 篩選**設定看起來類似 toohello 下列。
    
    ![部署 toohello azure ACS 篩選設定計算模擬器][add_acs_filter_lib_emulator]
11. 按一下 [完成] 。
12. 當呈現一個對話方塊，描述將建立 web.xml 檔案時，請按一下 [是]  。
13. 按一下**確定**tooclose hello **Java 組建路徑**對話方塊。

## <a name="deploy-toohello-compute-emulator"></a>部署 toohello 計算模擬器
1. 在 Eclipse 的 Project Explorer \(專案總管) 中，於 MyACSHelloWorld 上按一下滑鼠右鍵、按一下 Azure，然後按一下Package for Azure \(適用於 Azure 的套件)。
2. 針對 [Project name] \(專案名稱) 輸入 **MyAzureACSProject**，然後按 [Next] \(下一步)。
3. 選取 JDK 和應用程式伺服器。 (這些步驟會在 hello 詳細說明[在 Eclipse 中建立 Azure 的 Hello World 應用程式](http://msdn.microsoft.com/library/windowsazure/hh690944.aspx)教學課程)。
4. 按一下 [完成] 。
5. 按一下 hello**在 Azure 模擬器中執行** 按鈕。
6. Hello 計算模擬器中啟動您的 Java web 應用程式之後，請關閉您的瀏覽器的所有執行個體 （使任何目前的瀏覽器工作階段不會干擾您的 ACS 登入測試）。
7. 在瀏覽器中開啟 <http://localhost:8080/MyACSHelloWorld/> 來執行應用程式 (或如果您已核取 [Require HTTPS connections] \(需要 HTTPS 連線)，則請開啟 <https://localhost:8080/MyACSHelloWorld/>)。 應該提示您輸入 Windows Live ID 登入，則您應該採取 toohello 信賴憑證者的合作對象應用程式指定的傳回 URL。
8. 當您完成檢視您的應用程式時，按一下 [hello**重設 Azure 模擬器**] 按鈕。

## <a name="deploy-tooazure"></a>部署 tooAzure
toodeploy tooAzure，您將需要您的 ACS 命名空間 toochange hello 信賴憑證者合作對象領域和傳回 URL。

1. Hello Azure 管理入口網站中，在 hello 內**編輯信賴憑證者應用程式**頁面上，修改**領域**toobe hello URL，您已部署的站台。 取代**範例**您指定為您的部署的 hello DNS 名稱。
   
    ![Relying party realm for use in production][relying_party_realm_production]
2. 修改**傳回 URL** toobe hello URL 的應用程式。 取代**範例**您指定為您的部署的 hello DNS 名稱。
   
    ![Relying party return URL for use in production][relying_party_return_url_production]
3. 按一下**儲存**toosave 您更新信賴憑證者合作對象領域和傳回 URL 會變更。
4. 保留 hello**登入頁面整合**頁面在您的瀏覽器中開啟，您必須從它 toocopy 很快。
5. 在 Eclipse 的 Project Explorer \(專案總管) 中，於 **MyACSHelloWorld** 上按一下滑鼠右鍵、按一下 Build Path \(組建路徑)，然後按一下Configure Build Path \(設定組建路徑)。
6. 按一下 hello**文件庫**索引標籤上，按一下  **Azure 存取控制服務篩選**，然後按一下**編輯**。
7. 使用瀏覽器開啟 toohello**登入頁面整合**頁面 hello 管理入口網站中，複製 hello URL 列在 hello**選項 1： 連結 tooan ACS 裝載登入頁面**欄位，並將它貼到 hello **ACS 驗證端點**hello Eclipse 對話方塊的欄位。
8. 使用瀏覽器開啟 toohello**編輯信賴憑證者應用程式**頁面 hello 管理入口網站中，複製 hello URL 列在 hello**領域**欄位，並將它貼到 hello**信賴憑證者的合作對象領域** hello Eclipse 對話方塊的欄位。
9. Hello 內**安全性**hello Eclipse 對話方塊的區段，如果您想 toouse 現有的憑證，按一下**瀏覽**，瀏覽 toohello 憑證 toouse、 選取它，然後按一下**開啟**。 或者，如果您想 toocreate 新的憑證，請按一下**新增**toodisplay hello**新憑證** 對話方塊中，然後指定 hello 密碼、 hello.cer 檔案名稱，以及新的 hello 的 hello.pfx 檔案的名稱憑證。
10. 保留**hello WAR 檔案中的內嵌 hello 憑證**核取，假設您想要 tooembed hello 憑證 hello WAR 檔案中的。
11. [選用] 將 [Require HTTPS connections]  維持核取狀態。 如果您設定此選項時，您將需要 tooaccess 使用 hello HTTPS 通訊協定的應用程式。 如果您不想 toorequire HTTPS 連線，取消核取此選項。
12. 部署 tooAzure，為您的 Azure ACS 篩選設定看起來類似 toohello 下列。
    
    ![Azure ACS Filter settings for a production deployment][add_acs_filter_lib_production]
13. 按一下**完成**tooclose hello**編輯文件庫**對話方塊。
14. 按一下**確定**tooclose hello**屬性 MyACSHelloWorld**對話方塊。
15. 在 Eclipse 中，按一下 [hello**發行 tooAzure 雲端**] 按鈕。 回應 toohello 提示出現時，為 「 hello 中完成類似**toodeploy 應用程式 tooAzure**區段 hello[在 Eclipse 中建立 Azure 的 Hello World 應用程式](http://msdn.microsoft.com/library/windowsazure/hh690944.aspx)主題。 

之後已部署 web 應用程式，關閉任何開啟的瀏覽器工作階段中，執行 web 應用程式，而且您應該會提示您使用 Windows Live ID 認證，後面接著傳送 toohello toosign 傳回信賴憑證者的合作對象應用程式的 URL。

當您完成使用 ACS Hello World 應用程式，請記住 toodelete hello 部署 (您可以了解如何 toodelete hello 中的部署[在 Eclipse 中建立 Azure 的 Hello World 應用程式](http://msdn.microsoft.com/library/windowsazure/hh690944.aspx)主題)。

## <a name="next_steps"></a>接續步驟
Hello 安全性聲明標記語言 (SAML) ACS tooyour 應用程式所傳回的檢查，請參閱[tooview SAML hello Azure 存取控制服務所傳回的方式][How tooview SAML returned by hello Azure Access Control Service]。 toofurther 瀏覽 ACS 的功能和 tooexperiment 更趨精密完美的情況，請參閱[Access Control Service 2.0][Access Control Service 2.0]。

此外，此範例使用 hello **hello WAR 檔案中的內嵌 hello 憑證**選項。 此選項可讓簡單 toodeploy hello 憑證。 如果改為您想 tookeep 簽章憑證與 WAR 檔案不同，您可以使用下列技巧 hello:

1. 在 hello**安全性**hello 區段**Azure 存取控制服務篩選**對話方塊中，輸入**${env。JAVA_HOME}/mycert.cer**並取消核取**hello WAR 檔案中的內嵌 hello 憑證**。 (如果憑證檔案名稱不同，請調整 mycert.cer。)按一下**完成**tooclose hello 對話方塊。
2. 複製 hello 憑證，為您的部署中的元件： 在 Eclipse 的專案總管] 中，依序展開**MyAzureACSProject**，以滑鼠右鍵按一下**WorkerRole1**，按一下 [**屬性**依序展開**Azure 角色**，然後按一下**元件**。
3. 按一下 [新增] 。
4. 在 hello**加入元件**對話方塊：
   
   1. 在 hello**匯入**> 一節：
      1. 使用 hello**檔案**想 toouse 按鈕 toonavigate toohello 憑證。 
      2. 針對 [Method] \(方法)，選取 [copy] \(複製)。
   2. 如**身分名稱**，hello 文字方塊中按一下，然後接受 hello 預設名稱。
   3. 在 hello**部署**> 一節：
      1. 針對 [Method] \(方法)，選取 [copy] \(複製)。
      2. 如**toodirectory**，型別**%java_home**。
   4. 您**加入元件**對話方塊看起來類似 toohello 下列。
      
       ![Add certificate component][add_cert_component]
   5. 按一下 [確定] 。

此時，您的憑證將併入部署中。 請注意，不論您在 hello WAR 檔案中內嵌 hello 憑證還是將其新增為元件 tooyour 部署，您需要 tooupload hello 憑證 tooyour 命名空間 hello 中所述[上傳憑證 tooyour ACS 命名空間][ Upload a certificate tooyour ACS namespace] > 一節。

[What is ACS?]: #what-is
[Concepts]: #concepts
[Prerequisites]: #pre
[Create a Java web application]: #create-java-app
[Create an ACS Namespace]: #create-namespace
[Add Identity Providers]: #add-IP
[Add a Relying Party Application]: #add-RP
[Create Rules]: #create-rules
[Upload a certificate tooyour ACS namespace]: #upload-certificate
[Review hello Application Integration Page]: #review-app-int
[Configure Trust between ACS and Your ASP.NET Web Application]: #config-trust
[Add hello ACS Filter library tooyour application]: #add_acs_filter_library
[Deploy toohello compute emulator]: #deploy_compute_emulator
[Deploy tooAzure]: #deploy_azure
[Next steps]: #next_steps
[project website]: http://wastarterkit4java.codeplex.com/releases/view/61026
[How tooview SAML returned by hello Azure Access Control Service]: active-directory-java-view-saml-returned-by-access-control.md
[Access Control Service 2.0]: http://go.microsoft.com/fwlink/?LinkID=212360
[Windows Identity Foundation]: http://www.microsoft.com/download/en/details.aspx?id=17331
[Windows Identity Foundation SDK]: http://www.microsoft.com/download/en/details.aspx?id=4451
[Azure Management Portal]: https://manage.windowsazure.com
[acs_flow]: ./media/active-directory-java-authenticate-users-access-control-eclipse/ACSFlow.png

<!-- Eclipse-specific -->
[add_acs_filter_lib]: ./media/active-directory-java-authenticate-users-access-control-eclipse/AddACSFilterLibrary.png
[add_acs_filter_lib_emulator]: ./media/active-directory-java-authenticate-users-access-control-eclipse/AddACSFilterLibraryEmulator.png
[add_acs_filter_lib_production]: ./media/active-directory-java-authenticate-users-access-control-eclipse/AddACSFilterLibraryProduction.png

[relying_party_realm_emulator]: ./media/active-directory-java-authenticate-users-access-control-eclipse/RelyingPartyRealmEmulator.png
[relying_party_return_url_emulator]: ./media/active-directory-java-authenticate-users-access-control-eclipse/RelyingPartyReturnURLEmulator.png
[relying_party_realm_production]: ./media/active-directory-java-authenticate-users-access-control-eclipse/RelyingPartyRealmProduction.png
[relying_party_return_url_production]: ./media/active-directory-java-authenticate-users-access-control-eclipse/RelyingPartyReturnURLProduction.png
[add_cert_component]: ./media/active-directory-java-authenticate-users-access-control-eclipse/AddCertificateComponent.png
[add_jsp_file_acs]: ./media/active-directory-java-authenticate-users-access-control-eclipse/AddJSPFileACS.png
[create_acs_hello_world]: ./media/active-directory-java-authenticate-users-access-control-eclipse/CreateACSHelloWorld.png
[add_token_signing_cert]: ./media/active-directory-java-authenticate-users-access-control-eclipse/AddTokenSigningCertificate.png

