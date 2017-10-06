---
title: "aaaVisual Studio Azure 資源群組專案 |Microsoft 文件"
description: "使用 Visual Studio toocreate Azure 資源群組專案並將部署 hello 資源 tooAzure。"
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 4bd084c8-0842-4a10-8460-080c6a085bec
ms.service: azure-resource-manager
ms.devlang: multiple
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/10/2017
ms.author: tomfitz
ms.openlocfilehash: 672c1e71fb809b3b547f0fad30240d45de1ba923
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="creating-and-deploying-azure-resource-groups-through-visual-studio"></a>透過 Visual Studio 建立與部署 Azure 資源群組
與 Visual Studio 和 hello [Azure SDK](https://azure.microsoft.com/downloads/)，您可以建立您的基礎結構和程式碼 tooAzure 會將部署的專案。 例如，您可以定義 hello web 主機、 網站和資料庫應用程式和部署該基礎結構，以及 hello 程式碼。 或者，您可以定義虛擬機器、虛擬網路和儲存體帳戶，並且部署該基礎結構以及在虛擬機器上執行的指令碼。 hello **Azure 資源群組**部署專案可讓您 toodeploy 單一、 可重複執行作業中的所有所需的 hello 資源。 如需部署與管理資源的詳細資訊，請參閱 [Azure Resource Manager 概觀](resource-group-overview.md)。

Azure 資源群組專案包含 Azure 資源管理員 JSON 範本，其中定義部署 tooAzure hello 資源。 toolearn 有關 hello 元素 hello 資源管理員範本，請參閱[撰寫 Azure 資源管理員範本](resource-group-authoring-templates.md)。 Visual Studio 可讓您 tooedit 這些範本，並提供工具，可簡化範本使用。

在本文中，您將會部署 Web 應用程式和 SQL Database。 不過，hello 步驟 hello 是幾乎相同的任何類型的資源。 您可以輕鬆地部署虛擬機器和其相關的資源。 Visual Studio 針對部署常見案例提供許多不同的入門範本。

本文說明 Visual Studio 2017。 如果您使用 Visual Studio 2015 Update 2 和 Microsoft Azure SDK for.NET 2.9 或 Visual Studio 2013 與 Azure SDK 2.9 中，您的體驗主要是 hello 相同。 您可以使用 hello Azure SDK 2.6 或更新版本的版本不過，您的經驗 hello 使用者介面的可能不同於本文中所顯示的 hello 使用者介面。 我們強烈建議您安裝新版 hello hello [Azure SDK](https://azure.microsoft.com/downloads/)啟動 hello 步驟之前。 

## <a name="create-azure-resource-group-project"></a>建立 Azure 資源群組專案
在此程序中，您會利用 **Web 應用程式 + SQL** 範本建立 Azure 資源群組專案。

1. 在 Visual Studio 中，選擇 [檔案]、[新增專案]，再選擇 [C#] 或 [Visual Basic]。 然後選擇 [雲端]，再選擇 [Azure 資源群組] 專案。
   
    ![雲端部署專案](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/create-project.png)
2. 選擇 hello 範本的 toodeploy tooAzure 資源管理員。 請注意，有許多不同的選項根據 hello 輸入專案的您希望 toodeploy。 本文中，選擇 hello **Web 應用程式 + SQL**範本。
   
    ![選擇範本](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/select-project.png)
   
    您挑選的 hello 範本，只要開始;您可以加入和移除資源 toofulfill 您的案例。
   
   > [!NOTE]
   > Visual Studio 會在線上擷取一份可用範本清單。 hello 清單可能會變更。
   > 
   > 
   
    Visual Studio 建立 hello web 應用程式和 SQL database 的資源群組部署專案。
3. toosee 您建立的內容，查看在 hello hello 部署專案中的節點。
   
    ![顯示節點](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-items.png)
   
    因為我們選擇 hello Web 應用程式 + SQL 範本，此範例中，您會看見 hello 下列檔案： 
   
   | 檔案名稱 | 說明 |
   | --- | --- |
   | Deploy-AzureResourceGroup.ps1 |PowerShell 命令 toodeploy tooAzure 資源管理員會叫用 PowerShell 指令碼。<br />**請注意**Visual Studio 會使用此 PowerShell 指令碼 toodeploy 您的範本。 任何您所做變更影響在 Visual Studio 中的部署，因此請謹慎的 toothis 指令碼。 |
   | WebSiteSQLDatabase.json |定義您要部署 tooAzure，hello 基礎結構和 hello 參數，您可以在部署期間提供的 hello Resource Manager 範本。 它也會定義 hello hello 資源，因此資源管理員部署的 hello 正確的順序中的 hello 資源之間的相依性。 |
   | WebSiteSQLDatabase.parameters.json |包含 hello 範本所需值的參數檔案。 您要傳入參數值 toocustomize 每個部署。 |
   
    所有資源群組部署專案都包含這些基本檔案。 其他專案可能包含其他檔案 toosupport 其他功能。

## <a name="customize-hello-resource-manager-template"></a>自訂 hello Resource Manager 範本
您可以修改描述您想要 toodeploy hello 資源的 hello JSON 範本，以自訂部署專案。 JSON 代表 JavaScript 物件標記法，而且會與簡單 toowork 的序列化的資料格式。 hello JSON 檔案會使用您在每個檔案的 hello 頂端所參考的結構描述。 如果您想 toounderstand hello 結構描述，您可以下載並進行分析。 hello 結構描述會定義哪些項目都有效，hello 類型及格式的欄位，hello 可能值的列舉值，依此類推。 toolearn 有關 hello 元素 hello 資源管理員範本，請參閱[撰寫 Azure 資源管理員範本](resource-group-authoring-templates.md)。

toowork 您在範本上，開啟**WebSiteSQLDatabase.json**。

hello Visual Studio 編輯器提供工具 tooassist 您編輯 hello Resource Manager 範本。 hello **JSON 大綱**視窗可讓您的範本中定義的簡單 toosee hello 項目。

![顯示 JSON 大綱](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-json-outline.png)

Hello 大綱 中選取任一 hello 項目會將您帶 toothat hello 範本的一部分，並反白顯示對應 JSON 的 hello。

![瀏覽 JSON](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/navigate-json.png)

您可以將資源加入其中一個選取的 hello**加入資源**hello 頂端的 hello [JSON 大綱] 視窗，或以滑鼠右鍵按一下按鈕，在**資源**，然後選取**加入新資源**.

![新增資源](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-resource.png)

在本教學課程中，選取 [儲存體帳戶]  並提供它的名稱。 提供的名稱不能超過 11 個字元，而且只包含數字和小寫字母。

![加入儲存體](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-storage.png)

請注意，不只加入 hello 資源，但也 hello 的參數輸入儲存體帳戶和 hello hello 儲存體帳戶名稱的變數。

![顯示大綱](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-new-items.png)

hello **storageType**參數是預先定義允許的類型和預設類型。 您可以保留這些值，或針對您的案例進行編輯。 如果您不要的任何人 toodeploy **Premium_LRS**儲存體帳戶，透過這個範本中，會將它移除 hello 允許的類型。 

```json
"storageType": {
  "type": "string",
  "defaultValue": "Standard_LRS",
  "allowedValues": [
    "Standard_LRS",
    "Standard_ZRS",
    "Standard_GRS",
    "Standard_RAGRS"
  ]
}
```

Visual Studio 也提供編輯 hello 範本時，就可以使用 intellisense toohelp 您了解哪些屬性。 例如，您的應用程式服務方案的 tooedit hello 屬性瀏覽 toohello **HostingPlan**資源，並新增值 hello**屬性**。 請注意該 intellisense 會顯示 hello 可用的值，並提供該值的描述。

![顯示 intellisense](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-intellisense.png)

您可以設定**numberOfWorkers** too1。

```json
"properties": {
  "name": "[parameters('hostingPlanName')]",
  "numberOfWorkers": 1
}
```

## <a name="deploy-hello-resource-group-project-tooazure"></a>部署 hello 資源群組專案 tooAzure
您會 toodeploy 現在準備好您的專案。 當您部署 Azure 資源群組專案時，您將它部署 tooan Azure 資源群組。 hello 資源群組是共用常見的生命週期資源的邏輯群組。

1. Hello hello 部署專案節點的捷徑功能表，選擇 **部署** > **新增**。
   
    ![部署，新的部署功能表項目](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/deploy.png)
   
    hello**部署 tooResource 群組** 對話方塊隨即出現。
   
    ![部署 tooResource 群組對話方塊](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-deployment.png)
2. 在 hello**資源群組**下拉式方塊中，選擇現有的資源群組，或另外新建一個。 toocreate 資源群組中，開啟 hello**資源群組**下拉式清單方塊，然後選擇**新建**。
   
    ![部署 tooResource 群組對話方塊](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/create-new-group.png)
   
    hello**建立資源群組** 對話方塊隨即出現。 為您的群組的名稱和位置，然後選取 hello**建立** 按鈕。
   
    ![[建立資源群組] 對話方塊](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/create-resource-group.png)
3. 編輯 hello 部署的 hello 參數選取 hello**編輯參數** 按鈕。
   
    ![[編輯參數] 按鈕](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/edit-parameters.png)
4. 提供 hello 空參數的值，然後選取 hello**儲存** 按鈕。 hello 空參數**hostingPlanName**， **administratorLogin**， **administratorLoginPassword**，和**databaseName**。
   
    **hostingPlanName**指定名稱，以 hello [App Service 方案](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)toocreate。 
   
    **administratorLogin**指定 hello hello SQL Server 系統管理員的使用者名稱。 請勿使用常見的系統管理員名稱，例如 **sa** 或 **admin**。 
   
    hello **administratorLoginPassword**指定 SQL Server 系統管理員的密碼。 hello**以 hello 參數檔案中的純文字儲存密碼**選項不安全; 因此，請勿選取此選項。 由於 hello 密碼不會儲存為純文字，您必須 tooprovide 這個密碼一次在部署期間。 
   
    **databaseName**指定 hello 資料庫 toocreate 的名稱。 
   
    ![[編輯參數] 對話方塊](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/provide-parameters.png)
5. 選擇 hello**部署**按鈕 toodeploy hello 專案 tooAzure。 PowerShell 主控台開啟 hello Visual Studio 執行個體的外部。 在 hello PowerShell 主控台中出現提示時輸入 hello SQL Server 系統管理員密碼。 **PowerShell 主控台可能會隱藏在其他項目後面或 hello 工作列中的最小化。** 尋找此主控台，並選取該 tooprovide hello 密碼。
   
   > [!NOTE]
   > Visual Studio 可能會要求您 tooinstall hello Azure PowerShell cmdlet。 您需要 hello Azure PowerShell cmdlet toosuccessfully 部署資源群組。 如果出現提示，請予以安裝。
   > 
   > 
6. hello 部署可能需要幾分鐘的時間。 在 hello**輸出**windows 中，您看到 hello 部署的 hello 狀態。 Hello 部署完成時，hello 最後一則訊息表示成功的部署與類似的項目：
   
        ... 
        18:00:58 - Successfully deployed template 'websitesqldatabase.json' tooresource group 'DemoSiteGroup'.
7. 在瀏覽器中，開啟 hello [Azure 入口網站](https://portal.azure.com/)並登入 tooyour 帳戶。 toosee hello 資源群組中，選取**資源群組**與您部署的 hello 資源群組。
   
    ![選取群組](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/select-group.png)
8. 您會看到部署的 hello 的所有資源。 請注意 hello 儲存體帳戶不是完全加入該資源時，指定您的 hello 名稱。 hello 儲存體帳戶必須是唯一的。 hello 範本會自動加入字串的字元 toohello 名稱提供 tooprovide 唯一的名稱。 
   
    ![顯示資源](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-deployed-resources.png)
9. 如果您進行變更，而且想 tooredeploy 您的專案，請從 hello 的 Azure 資源群組專案的捷徑功能表選擇 hello 現有的資源群組。 Hello 快顯功能表上，選擇**部署**，然後選擇您所部署的 hello 資源群組。
   
    ![已部署 Azure 資源群組](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/redeploy.png)

## <a name="deploy-code-with-your-infrastructure"></a>以您的基礎結構部署程式碼
此時，您應用程式部署 hello 基礎結構，但沒有實際程式碼與 hello 專案部署。 本文將說明如何 toodeploy web 應用程式和 SQL Database 資料表在部署期間。 如果您要部署虛擬機器，而不是 web 應用程式，您要 toorun hello 做為部署的一部分的電腦上的某些程式碼。 hello 程序部署 web 應用程式的程式碼，或將虛擬機器設定為幾乎 hello 相同。

1. 加入專案 tooyour Visual Studio 方案。 Hello 方案上按一下滑鼠右鍵，然後選取**新增** > **新專案**。
   
    ![新增專案](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-project.png)
2. 新增 **ASP.NET Web 應用程式**。 
   
    ![加入 Web 應用程式](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-app.png)
3. 選取 **MVC**。
   
    ![選取 MVC](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/select-mvc.png)
4. Visual Studio 會建立您的 web 應用程式之後，您會看到 hello 方案中的這兩個專案。
   
    ![顯示專案](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-projects.png)
5. 現在，您必須確定您的資源群組專案可感知 hello 新專案的 toomake。 返回 tooyour 資源群組專案 (AzureResourceGroup1)。 以滑鼠右鍵按一下 [參考]，然後選取 [新增參考]。
   
    ![加入參考](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-new-reference.png)
6. 選取您建立的 hello web 應用程式專案。
   
    ![加入參考](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-reference.png)
   
    藉由加入參考，將會連結 hello web 應用程式專案 toohello 資源群組專案，並自動設定三個索引鍵屬性。 您會看到這些屬性在 hello**屬性**hello 參考的視窗。
   
      ![查看參考](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/see-reference.png)
   
    hello 屬性如下：
   
   * hello**其他屬性**包含預備位置，而被排除 toohello Azure 儲存體 hello web 部署套件。 請注意 hello 資料夾 (ExampleApp) 和檔案 (package.zip)。 您需要 tooknow 這些值因為您提供為參數來部署 hello 應用程式。 
   * hello**包含檔案路徑**包含 hello 路徑建立 hello 封裝的位置。 hello**包含目標**包含執行部署的 hello 命令。 
   * hello 預設值是**建置。封裝**可讓 hello 部署 toobuild，並建立 web 部署套件 (package.zip)。  
     
     您不需要的發行設定檔為 hello 部署從 hello 屬性 toocreate hello 封裝取得 hello 所需的資訊。
7. 返回 tooWebSiteSQLDatabase.json，並加入資源 toohello 範本。
   
    ![新增資源](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-resource-2.png)
8. 這次請選取 [Web Deploy for Web Apps] 。 
   
    ![加入 Web 部署](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-web-deploy.png)
9. 重新部署您的資源群組專案 toohello 資源群組。 這次還有一些新的參數。 您不需要 tooprovide 值**_artifactsLocation**或**_artifactsLocationSasToken**因為 Visual Studio 會自動產生這些值。 不過，您必須 tooset hello 資料夾和檔案名稱 toohello 路徑包含 hello 部署封裝 (顯示為**ExampleAppPackageFolder**和**ExampleAppPackageFileName** hello 下列映像中). 提供您已看到，稍早在 hello 值 hello 參考屬性 (**ExampleApp**和**package.zip**)。
   
    ![加入 Web 部署](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/set-new-parameters.png)
   
    Hello**成品儲存體帳戶**，選取 hello 與此資源群組部署的其中一個。
10. Hello 部署完成之後，請在 hello 入口網站中選取您 web 應用程式。 選取 hello URL toobrowse toohello 站台。
    
     ![瀏覽網站](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/browse-site.png)
11. 請注意您已成功部署 hello 預設 ASP.NET 應用程式。
    
     ![顯示已部署的應用程式](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-deployed-app.png)

## <a name="next-steps"></a>後續步驟
* toolearn 關於管理您的資源，透過 hello 入口網站，請參閱[使用 hello Azure 入口網站 toomanage 您的 Azure 資源](resource-group-portal.md)。
* toolearn 進一步了解範本，請參閱[撰寫 Azure 資源管理員範本](resource-group-authoring-templates.md)。

