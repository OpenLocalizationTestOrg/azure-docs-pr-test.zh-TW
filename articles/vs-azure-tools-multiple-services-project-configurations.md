---
title: "aaaConfiguring Azure 專案使用多個服務組態 |Microsoft 文件"
description: "了解如何 tooconfigure Azure 雲端服務專案的變更 hello ServiceDefinition.csdef 和 ServiceConfiguration.cscfg 檔案。"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: a4fb79ed-384f-4183-9f74-5cac257206b9
ms.service: multiple
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: 14222266093eb876db0ac9ce8d3d17a04c65d1a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-your-azure-project-using-multiple-service-configurations"></a>使用多個服務組態設定 Azure 專案
Azure 雲端服務專案包含兩個組態檔：ServiceDefinition.csdef 和 ServiceConfiguration.cscfg。 這些檔案會隨附於 Azure 雲端服務應用程式並部署 tooAzure。

* hello **ServiceDefinition.csdef**檔案包含 hello hello Azure 環境針對 hello 應用程式需求的雲端服務，包括包含哪些角色所需的中繼資料。 此檔案也包含套用 tooall 執行個體的組態設定。 可以讀取這些組態設定，在執行階段使用 hello Azure 服務裝載執行階段 API。 當您的服務在 Azure 中執行時，無法更新此檔案。
* hello **ServiceConfiguration.cscfg**檔案 hello hello 服務定義檔中定義的組態設定的設定值，並指定每個角色執行個體 toorun 的 hello 數目。 當您的雲端服務在 Azure 中執行時，可以更新此檔案。

hello Azure Tools for Microsoft Visual Studio 提供您可以使用這些檔案中儲存的 tooset 組態設定的屬性頁。 tooaccess hello 屬性頁中，連按兩下 方案總管 中的 hello Azure 雲端服務專案底下的 hello 角色參照或以滑鼠右鍵按一下 hello 角色參考並選擇 **屬性**hello 遵循圖所示。

![VS_Solution_Explorer_Roles_Properties](./media/vs-azure-tools-multiple-services-project-configurations/IC784076.png)

如需 hello 基礎 hello 服務定義和服務組態檔結構描述資訊，請參閱 hello[結構描述參考](https://msdn.microsoft.com/library/azure/dd179398.aspx)。 如需服務組態的詳細資訊，請參閱[tooConfigure 雲端服務如何](cloud-services/cloud-services-how-to-configure.md)。

## <a name="configuring-role-properties"></a>設定角色屬性
雖然有一些差異，hello 下列各節將指出，很類似，web 角色和背景工作角色的 hello 屬性頁。

從 hello**快取**頁面上，您可以設定 hello Azure 快取服務。

### <a name="configuration-page"></a>組態頁面
在 [hello**組態**] 頁面上，您可以設定這些屬性：

**Instances**

設定 hello**執行個體**計數屬性 toohello 的 hello 服務都應該執行此角色的執行個體。

設定 hello **VM 大小**屬性太**超小型**，**小**，**媒體**，**大**，或**超大型**。  如需詳細資訊，請參閱 [雲端服務的大小](cloud-services/cloud-services-sizes-specs.md)。

**啟動動作** (僅限 Web 角色)

設定此屬性 toospecify 您開始偵錯時，Visual Studio 應該啟動網頁瀏覽器 hello HTTP 端點或 hello HTTPS 端點，或兩者。

hello HTTPS 端點選項是您已為您的角色定義 HTTPS 端點時，才可以使用。 您可以定義 HTTPS 端點上 hello**端點**屬性頁。

如果您已經加入 HTTPS 端點，依預設，會啟用 hello HTTPS 端點選項，Visual Studio 在您開始偵錯時，除了 HTTP 端點的 tooa 瀏覽器，將會啟動此端點的瀏覽器。 這是假設兩個啟動選項都已啟用。

**診斷**

根據預設，會啟用 hello Web 角色的診斷。 hello Azure 雲端服務專案和儲存體帳戶設定 toouse hello 本機儲存體模擬器。 當您準備好 toodeploy tooAzure 時，您可以選取 hello 產生器 按鈕 (**...**) tooupdate hello 儲存體帳戶 toouse hello 雲端中的 Azure 儲存體。 您可以視需要或自動排程的間隔來傳送 hello 診斷資料 toohello 儲存體帳戶。 如需 Azure 診斷的詳細資訊，請參閱 [在 Azure 雲端服務和虛擬機器中啟用診斷](cloud-services/cloud-services-dotnet-diagnostics.md)。

## <a name="settings-page"></a>設定頁面
在 [hello**設定**] 頁面上，您可以加入您的服務組態設定。 組態設定是名稱-值組。 Hello 角色中執行的程式碼可以讀取您的組態設定，在執行階段使用提供的 hello 類別 hello 值[Azure Managed 程式庫](http://go.microsoft.com/fwlink?LinkID=171026)。 具體來說，hello [GetConfigurationSettingValue](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.getconfigurationsettingvalue.aspx)方法會傳回具名的組態設定，在執行階段 hello 值。

### <a name="configuring-a-connection-string-tooa-storage-account"></a>設定連接字串 tooa 儲存體帳戶
連接字串會是 hello 儲存體模擬器或 Azure 儲存體帳戶提供連接和驗證資訊的組態設定。 每當您的程式碼必須存取 Azure 儲存體服務資料 – 也就是 blob、 佇列或資料表的資料 – 從角色中執行的程式碼，您必須 toodefine 該儲存體帳戶的連接字串。

點 tooan Azure 儲存體帳戶的連接字串必須使用定義的格式。 如需有關資訊 toocreate 的連接字串，請參閱[設定 Azure 儲存體連接字串](storage/common/storage-configure-connection-string.md)。

當您準備好 tootest 自己的服務與 hello Azure 儲存體服務，或當您準備 toodeploy 您雲端服務 tooAzure，您可以變更的任何連接字串 toopoint tooyour Azure 儲存體帳戶的 hello 值。 選取 ([…])，選取 [輸入儲存體帳戶認證]。 輸入您的帳戶資訊，包含您的帳戶名稱和帳戶金鑰。 在 hello**儲存體帳戶連接字串**對話方塊中，您還可以指出是否要 toouse hello 預設的 HTTPS 端點 （hello 預設選項）、 hello 預設 HTTP 端點或自訂端點。 您可能會決定 toouse 自訂端點當您註冊您的服務的自訂網域名稱中所述[設定 Azure 儲存體帳戶中的 blob 資料的自訂網域名稱](storage/blobs/storage-custom-domain-name.md)。

> [!IMPORTANT]
> 部署您的服務之前，您必須修改您的連接字串 toopoint tooan Azure 儲存體帳戶。 這可能會導致您的角色不 toostart toodo 失敗，或透過 toocycle hello 初始化、 忙碌和停止狀態。
> 
> 

## <a name="endpoints-page"></a>端點頁面
背景工作角色可以有任意數目的 HTTP、HTTPS 或 TCP 端點。 端點可以是輸入的端點，也就是可用 tooexternal 用戶端或內部端點，也就是執行 hello 服務中的可用 tooother 角色。

* toomake HTTP 端點可用 tooexternal 用戶端和網頁瀏覽器中，變更 hello 端點型別 tooinput，並指定名稱和公用連接埠號碼。
* toomake HTTPS 端點提供 tooexternal 用戶端和網頁瀏覽器中，變更 hello 端點類型太**輸入**，並指定名稱、 公用連接埠編號，以及管理憑證的名稱。
  
    請注意，您可以指定管理憑證之前，您必須定義 hello 憑證上 hello**憑證**屬性頁。
* toomake 供 hello 的雲端服務中的其他角色的內部存取端點變更 hello 端點型別 toointernal，以及指定名稱和可能的私用連接埠，這個端點。

## <a name="local-storage-page"></a>本機儲存體頁面
您可以使用 hello**本機儲存體**屬性頁面 tooreserve 其中一個或多個角色的本機儲存體資源。 本機儲存體資源是在 hello hello Azure 虛擬機器檔案系統中的預留的目錄中執行的角色執行個體。

## <a name="certificates-page"></a>憑證頁面
在 [hello**憑證**] 頁面上，您可以將憑證與您的角色。 您將可以使用的 tooconfigure hello 上的 HTTPS 端點的 hello 憑證**端點**屬性頁。

hello**憑證**屬性頁加入您的憑證 tooyour 服務組態的相關資訊。 請注意，您的憑證不隨附於您的服務;您必須將憑證上傳分別透過 hello tooAzure [Azure 傳統入口網站](http://go.microsoft.com/fwlink/?LinkID=213885)。

tooassociate 與角色，憑證提供 hello 憑證的名稱。 Hello 上設定 HTTPS 端點時，會使用此名稱 toorefer toohello 憑證**端點**屬性頁。 接下來，指定是否 hello 憑證存放區是**本機**或**目前使用者**和 hello hello 存放區的名稱。 最後，請輸入 hello 憑證的指紋。 如果 hello 憑證位在 hello 目前使用者 \ 個人 (My) 存放區，您可以藉由從填入的清單中選取 hello 憑證輸入 hello 憑證的指紋。 如果它位於其他任何位置，請以手動方式輸入 hello 指紋值。

當您將憑證從 hello 憑證存放區時，所有中繼憑證會自動加入 toohello 為您的組態設定。 這些中繼憑證必須也先上傳 tooAzure 順序 toocorrectly 中的設定 ssl 服務。

將與您的服務產生關聯的任何管理憑證在 hello 雲端中執行時，才套用 tooyour 服務。 當 hello 本機開發環境中執行您的服務時，它會使用標準的憑證，由 hello 計算模擬器所管理。

## <a name="configuring-hello-azure-cloud-service-project"></a>設定 hello Azure 雲端服務專案
tooconfigure 套用 tooan 整個 Azure 雲端服務專案的設定，您第一次開啟該專案節點，hello 捷徑功能表，然後您選擇屬性 tooopen 其屬性頁。 hello 下表顯示這些屬性頁。

| 屬性頁面 | 說明 |
| --- | --- |
| 應用程式 |從這個頁面上，您可以顯示 hello 這個雲端服務專案所使用的 Azure Tools 版本的相關資訊，而且可以升級 toohello hello 工具目前版本。 |
| 建置事件 |在此頁面，您可以設定建置前和建置後事件。 |
| 開發 |您可以從這個頁面上，指定組建組態指令及執行任何建置後事件的 hello 條件。 |
| Web |從這個頁面上，您可以設定與相關 toohello web 伺服器的設定。 |

