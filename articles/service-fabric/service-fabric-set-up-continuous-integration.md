---
title: "設定連續整合 Azure microservices aaaSet |Microsoft 文件"
description: "概略了解 tooset 連續整合和部署 Service Fabric 應用程式使用 Visual Studio Team Services (VSTS)。"
services: service-fabric
documentationcenter: na
author: mthalman-msft
manager: timlt
editor: 
ms.assetid: 3e8c2290-9e7a-456a-9b2c-db44d1b3988d
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 12/06/2016
ms.author: mthalman;mikhegn
ms.openlocfilehash: 041e081f4a42f379394f2d21f07db4f6de045b24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-service-fabric-continuous-integration-and-deployment-with-visual-studio-team-services"></a>使用 Visual Studio Team Services 設定 Service Fabric 連續整合和部署
本文說明 hello 步驟 tooset 連續整合和 Azure Service Fabric 應用程式的部署使用 Visual Studio Team Services (VSTS)。

這份文件會反映 hello 目前程序，且預期的 toochange 經過一段時間。

## <a name="prerequisites"></a>必要條件
tooget 啟動，請遵循下列步驟：

1. 請確定您有存取 tooa Team Services 帳戶或[建立一個](https://www.visualstudio.com/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services)自己。
2. 請確定您有存取 tooa Team Services 的 team 專案或[建立一個](https://www.visualstudio.com/docs/setup-admin/create-team-project)自己。
3. 請確定您有 Service Fabric 叢集 toowhich 您可以部署應用程式，或建立一個使用 hello [Azure 入口網站](service-fabric-cluster-creation-via-portal.md)、 [Azure Resource Manager 範本](service-fabric-cluster-creation-via-arm.md)，或[Visual Studio](service-fabric-cluster-creation-via-visual-studio.md).
4. 確定您已經建立 Service Fabric 應用程式 (.sfproj) 專案。 您必須建立或升級 Service Fabric SDK 2.1 或更新版本的專案 （hello.sfproj 檔案應包含 ProjectVersion 屬性值的 1.1 版或更高）。

> [!NOTE]
> 自訂組建代理程式已不再需要。 Team Services 裝載的代理程式現在都預先安裝 Service Fabric 叢集管理軟體，可讓您直接從這些代理程式部署應用程式。
> 
> 

## <a name="configure-and-share-your-source-files"></a>設定和共用來源檔案
hello 第一件事您所要 toodo Team Services 中執行的 hello 部署程序用於準備發行設定檔。  hello 發行設定檔應該是您先前已備妥的設定的 tootarget hello 叢集：

1. 選擇您的應用程式專案內的發行設定檔的 toouse 連續整合工作流程。 請遵循 hello[發行指示](service-fabric-publish-app-remote-cluster.md)如何 toopublish 應用程式 tooa 遠端叢集。 實際上不需要 toopublish 您的應用程式透過。 您可以按一下 hello**儲存**中超 hello 發行對話方塊，一旦您已適當地設定項目。
2. 如果您想要升級的 Team Services 中，就會發生的每個部署您的應用程式 toobe，您會想 tooconfigure hello 發行設定檔 tooenable 升級。 在 hello 相同步驟 1 中發行用的對話方塊，請確定該 hello**升級 hello 應用程式**核取方塊。  深入了解 [設定其他升級設定](service-fabric-visualstudio-configure-upgrade.md)。 按一下 hello**儲存**超連結 toosave hello 設定 toohello 發行設定檔。
3. 請確定您已將變更儲存 toohello 發行設定檔，然後取消 hello 發行對話方塊。
4. 現在就開始太[共用您的應用程式專案的來源檔案](https://www.visualstudio.com/docs/setup-admin/team-services/connect-to-visual-studio-team-services#vs)使用 Team Services。 原始程式檔都可以存取 Team Services 之後，您就可以進入 toohello 產生組建的下一個步驟。 

## <a name="create-a-build-definition"></a>建立組建定義
Team Services 組建定義描述由一組循序執行的組建步驟所組成的工作流程。 hello 組建定義，您要建立 hello 目標是 tooproduce Service Fabric 應用程式封裝時和其他成品，可能是使用的 toodeploy hello 應用程式。 深入了解 Team Services [組建定義](https://www.visualstudio.com/docs/build/define/create)。

### <a name="create-a-definition-from-hello-build-template"></a>建立從 hello 建置範本的定義
1. 在 Visual Studio Team Services 中開啟您的小組專案。
2. 選取 hello**建置** 索引標籤。
3. 選取 hello 綠色 **+** 簽署 toocreate 新的組建定義。
4. 在 hello 開啟對話方塊中，選取  **Azure Service Fabric 應用程式**內 hello**建置**範本類別目錄。
5. 選取 [下一步] 。
6. 選取 hello 儲存機制與分支 Service Fabric 應用程式相關聯。
7. 選取您想 toouse hello 代理程式佇列。 支援裝載的代理程式。
8. 選取 [ **建立**]。
9. 儲存 hello 組建定義，並提供名稱。
10. hello 下列段落是 hello hello 範本產生的建置步驟的說明：

| 組建步驟 | 說明 |
| --- | --- |
| NuGet 還原 |還原 hello hello 方案的 NuGet 套件。 |
| 組建方案 \*.sln |建置 hello 整個方案。 |
| 組建方案 \*.sfproj |會產生 hello Service Fabric 應用程式套件，是使用的 toodeploy hello 應用程式。 hello 應用程式封裝位置是指定的 toobe hello 組建成品目錄內。 |
| 更新 Service Fabric 應用程式版本 |更新升級支援的 hello 應用程式套件的資訊清單檔案 tooallow 中所包含的 hello 版本值。 請參閱 hello[工作文件頁面](https://go.microsoft.com/fwlink/?LinkId=820529)如需詳細資訊。 |
| 複製檔案 |複製 hello 發行設定檔和應用程式參數檔案 toohello 組建的成品 toobe 所耗用的部署。 |
| 發行構件 |發行 hello 組建的成品。 可讓發行定義 tooconsume hello 組建的成品。 |

### <a name="verify-hello-default-set-of-tasks"></a>確認 hello 組預設的工作
1. 確認 hello**方案**輸入的欄位 hello **NuGet 還原**和**建置方案**建置步驟。  根據預設，這些建置步驟執行於 hello 相關聯的儲存機制中所包含的所有方案檔案。  如果您只想 hello 組建定義 toooperate 上其中一個這些方案檔，您需要 tooexplicitly 更新 hello 路徑 toothat 檔案。
2. 確認 hello**方案**輸入的欄位 hello**應用程式封裝**建置步驟。  根據預設，此建置步驟會假設只有一個 Service Fabric 應用程式專案 (.sfproj) 存在於 hello 儲存機制。  如果您在您的儲存機制中有多個這類檔案，並想 tootarget 只有一個此組建定義，您會需要 tooexplicitly 更新 hello 路徑 toothat 檔案。  如果您想的 toopackage 多個應用程式專案，在您的儲存機制中，您需要 toocreate 額外**Visual Studio 建置**hello 組建定義每個目標的應用程式專案中的步驟。  然後您也需要 tooupdate hello **MSBuild 引數**欄位的每個建置步驟，以便為每個唯一 hello 封裝位置。
3. 確認 hello hello 中定義的版本設定行為**更新 Service Fabric 應用程式版本**建置步驟。  根據預設，此建置步驟會將附加 hello 組建 tooall 版本中的數值 hello 應用程式封裝的資訊清單檔。 請參閱 hello[工作文件頁面](https://go.microsoft.com/fwlink/?LinkId=820529)如需詳細資訊。 這是適用於支援應用程式的升級，因為每個升級的部署需要從 hello 先前的部署不同的版本值。 如果您不打算 toouse 應用程式升級工作流程中，您可以考慮停用此建置步驟。 如果您打算 tooproduce 組建時，可以使用的 toooverwrite 現有的 Service Fabric 應用程式，它必須是停用。 如果 hello hello hello 組建產生的應用程式版本與 hello hello hello 叢集中的應用程式版本不相符，hello 部署將會失敗。
4. 如果您的方案包含.NET Core 專案，您必須確定您的組建定義包含可還原 hello 相依性的建置步驟：
   1. 選取 [新增組件步驟...] 。
   2. 找出 hello**命令列**hello 公用程式 索引標籤內工作，然後按一下其 新增 按鈕。
   3. Hello 工作輸入欄位，請使用下列值的 hello:
   4. 工具︰dotnet
   5. 引數︰restore
   6. 拖曳 hello 工作，讓它位於 hello 之後立即**NuGet 還原**步驟。
5. 儲存任何變更，您所做 toohello 組建定義。

### <a name="try-it"></a>試試看
選取**佇列組建**toomanually 啟動組建。 推送或簽入時也會觸發組建。 一旦您確認 hello 組建已順利執行，您就可以進入 toodefining 部署您的應用程式 tooa 叢集中的發行定義。

## <a name="create-a-release-definition"></a>建立發行定義
Team Services 發行定義描述由一組循序執行的工作所組成的工作流程。 hello hello 發行定義您所建立的目的是 tootake 應用程式封裝，並將其部署 tooa 叢集。 Hello 一起使用時，組建定義並發行定義可執行 hello 整個工作流程無法與來源檔案 tooending 與叢集中執行的應用程式啟動。 深入了解 Team Services [發行定義](https://www.visualstudio.com/docs/release/author-release-definition/more-release-definition)。

### <a name="create-a-definition-from-hello-release-template"></a>建立定義在 hello 發行範本
1. 在 Visual Studio Team Services 中開啟您的專案。
2. 選取 hello**發行** 索引標籤。
3. 選取 hello 綠色 **+** 登 toocreate 新的發行定義，然後選取**建立發行定義**hello 功能表中。
4. 在 hello 開啟對話方塊中，選取  **Azure Service Fabric 部署**內 hello**部署**範本類別目錄。
5. 選取 [下一步] 。
6. 選取要作為此發行定義的 hello 來源 toouse hello 組建定義。  hello 發行定義參考 hello 成品作業所產生的 hello 選取組建定義。
7. 檢查 hello**連續部署**核取方塊，如果您想 toohave Team Services 自動建立新的版本和部署 hello Service Fabric 應用程式組建完成時。
8. 選取您想 toouse hello 代理程式佇列。 支援裝載的代理程式。
9. 選取 [ **建立**]。
10. Hello hello hello 頁頂端的鉛筆圖示，即可編輯 hello 定義名稱。
11. 選取您的應用程式應該部署的 hello 叢集 toowhich 從 hello**叢集連線**hello 工作的輸入的欄位。 hello 叢集連線所提供，可讓 hello 部署工作 tooconnect toohello 叢集 hello 必要資訊。 如果您還沒有叢集連線為您的叢集，請選取 hello**管理**超連結下一步 toohello 欄位 tooadd 其中一個。 在開啟的 hello 頁面上，執行下列步驟的 hello:
    1. 選取**新的服務端點**，然後選取  **Azure Service Fabric** hello 功能表。
    2. 選取 hello 這個端點做為目標的 hello 叢集正在使用的驗證類型。
    3. 您連接的名稱定義在 hello**連接名稱**欄位。  一般而言，您可使用 hello 叢集的名稱。
    4. 定義 hello 用戶端連線的端點 URL 中 hello**叢集端點**欄位。  範例︰tcp://contoso.westus.cloudapp.azure.com:19000。
    5. 對於 Azure Active Directory 認證，請定義您想要在 hello toouse tooconnect toohello 叢集 hello 認證**Username**和**密碼**欄位。
    6. 對於以憑證為基礎的驗證，定義 hello Base64 編碼的 hello 用戶端憑證檔案，在 hello**用戶端憑證**欄位。  請參閱 hello 說明快顯視窗，該欄位有關的資訊 tooget 該值。  如果您的憑證是否受密碼保護，定義 hello 密碼 hello**密碼**欄位。
    7. 按一下 [確定] 確認變更。 之後瀏覽後 tooyour 發行定義中，按一下 hello 重新整理圖示上 hello**叢集連線**您剛才加入的欄位 toosee hello 端點。
12. 儲存 hello 發行定義。

> [!NOTE]
> Microsoft 帳戶 (例如，@hotmail.com 或 @outlook.com) 不支援 Azure Active Directory 驗證。
> 
> 

建立 hello 定義包含類型的一項工作**Service Fabric 應用程式部署**。 請參閱 hello[工作文件頁面](https://go.microsoft.com/fwlink/?LinkId=820528)如需有關這項工作。

### <a name="verify-hello-template-defaults"></a>確認 hello 範本的預設值
1. 確認 hello**發行設定檔**輸入的欄位 hello**部署 Service Fabric 應用程式**工作。 根據預設，此欄位會參考名為 Cloud.xml hello 組建成品中所包含的發行設定檔。 如果您想 tooreference 不同的發行設定檔或 hello 建置包含多個應用程式封裝中其成品,，您需要 tooupdate hello 路徑正確。
2. 確認 hello**應用程式封裝**輸入的欄位 hello**部署 Service Fabric 應用程式**工作。 根據預設，此欄位會參考 hello 組建定義範本中所使用的 hello 預設應用程式封裝路徑。  如果您已經修改 hello 預設應用程式封裝路徑中 hello 組建定義，您需要 tooupdate hello 路徑適當地這裡以及。

### <a name="try-it"></a>試試看
選取**建立發行**從 hello**釋放**按鈕功能表 toomanually 建立發行。 在開啟 hello 對話方塊中，選取 您希望 toobase hello 版本上，然後按一下的 hello 組建**建立**。 如果您啟用連續部署，版本將會自動建立相關聯的 hello 組建定義完成的組建。

## <a name="next-steps"></a>後續步驟
toolearn 更多關於 Service Fabric 應用程式，讀取下列文件的 hello 的連續整合：

* [Team Services 文件首頁](https://www.visualstudio.com/docs/overview)
* [Team Services 中的組建管理](https://www.visualstudio.com/docs/build/overview)
* [Team Services 中的發行管理](https://www.visualstudio.com/docs/release/overview)

