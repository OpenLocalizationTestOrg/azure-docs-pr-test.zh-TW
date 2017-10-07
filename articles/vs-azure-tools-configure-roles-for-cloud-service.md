---
title: "aaaConfigure hello 角色的 Azure 雲端服務與 Visual Studio |Microsoft 文件"
description: "深入了解如何 tooset 安裝及設定 Azure 雲端服務使用 Visual Studio 的角色。"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: d397ef87-64e5-401a-aad5-7f83f1022e16
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 03/21/2017
ms.author: kraigb
ms.openlocfilehash: d3c62eb57040ebe987787e73b17b468bb82122bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-cloud-service-roles-with-visual-studio"></a>使用 Visual Studio 設定 Azure 雲端服務角色
Azure 雲端服務可以有一或多個背景工作角色或 web 角色。 每個角色，您需要該角色的設定方式的 toodefine 與也設定該角色的執行方式。 進一步了解雲端服務中的角色 toolearn 看到 hello 視訊[簡介 tooAzure 雲端服務](https://channel9.msdn.com/Series/Windows-Azure-Cloud-Services-Tutorials/Introduction-to-Windows-Azure-Cloud-Services)。 

為雲端服務的 hello 資訊會儲存在 hello 下列檔案：

- **ServiceDefinition.csdef** -hello 服務定義檔定義您的雲端服務，包括所需的角色、 端點和虛擬機器大小的 hello 執行階段設定。 不會儲存在 hello 資料`ServiceDefinition.csdef`角色正在執行時，可以變更。
- **ServiceConfiguration.cscfg** -hello 服務組態檔會設定執行多少個角色執行個體，並為角色定義 hello hello 設定值。 hello 資料儲存在`ServiceConfiguration.cscfg`角色正在執行時，可以變更。

toostore 不同值的 hello 設定該角色的執行方式的控制項，則您可以定義多個服務組態。 您可以將不同的服務組態用於每個部署環境。 比方說，您可以在本機服務組態設定儲存體帳戶連接字串 toouse hello 本機 Azure 儲存體模擬器，並在 hello 雲端中建立另一個服務組態 toouse Azure 儲存體。

當您在 Visual Studio 中建立 Azure 雲端服務時，則兩個服務組態會自動建立，並且加入 tooyour Azure 專案：

- `ServiceConfiguration.Cloud.cscfg`
- `ServiceConfiguration.Local.cscfg`

## <a name="configure-an-azure-cloud-service"></a>設定 Azure 雲端服務
Hello 步驟中所示，您可以在 Visual Studio 設定 Azure 雲端服務從方案總管:

1. 在 Visual Studio 中建立或開啟 Azure 雲端服務專案。

1. 在**方案總管 中**、 hello 專案上按一下滑鼠右鍵，然後從 hello 內容功能表中，選取**屬性**。
   
    ![方案總管專案操作功能表](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-project-context-menu.png)

1. 在 hello 專案屬性頁面上，選取 hello**開發** 索引標籤。 

    ![專案屬性頁面- 開發索引標籤](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-development-tab.png)

1. 在 hello**服務組態**清單中，選取 hello 想 tooedit hello 服務組態名稱。 (如果您想 toomake 變更 tooall hello 服務組態，為這個角色，請選取**所有組態**。)
   
    > [!IMPORTANT]
    > 如果您選擇特定服務組態，某些屬性會停用，因為它們只能針對所有組態設定。 tooedit 這些屬性，您必須選取**所有組態**。
    > 
    > 
   
    ![Azure 雲端服務的服務組態清單](./media/vs-azure-tools-configure-roles-for-cloud-service/cloud-service-service-configuration-property.png)

## <a name="change-hello-number-of-role-instances"></a>變更角色執行個體的 hello 數目
tooimprove hello 雲端服務的效能，您可以變更角色的執行，使用者或特定角色的預期的 hello 負載的 hello 數目為基礎的執行個體的 hello 數目。 不同的虛擬機器角色的每個執行個體執行時所建立 hello 雲端服務在 Azure 中。 這會影響這個雲端服務的 hello 部署的 hello 計費。 如需計費的詳細資訊，請參閱[了解 Microsoft Azure 帳單](billing/billing-understand-your-bill.md)。

1. 在 Visual Studio 中建立或開啟 Azure 雲端服務專案。

1. 在**方案總管 中**，展開 hello 專案節點。 在 hello**角色**節點、 以滑鼠右鍵按一下您想 tooupdate，並從 hello 內容功能表中，選取 hello 角色**屬性**。

    ![方案總管 Azure 角色操作功能表](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-azure-role-context-menu.png)

1. 選取 hello**組態** 索引標籤。

    ![組態索引標籤](./media/vs-azure-tools-configure-roles-for-cloud-service/role-configuration-properties-page.png)

1. 在 hello**服務組態**清單中，您想 tooupdate 選取 hello 服務組態。
   
    ![服務組態清單](./media/vs-azure-tools-configure-roles-for-cloud-service/role-configuration-properties-page-select-configuration.png)

1. 在 hello**執行個體計數**文字方塊中，輸入您要此角色 toostart 的執行個體的 hello 數目。 當您發行 hello 雲端服務 tooAzure 個別的虛擬機器執行每個執行個體。

    ![更新 hello 執行個體計數](./media/vs-azure-tools-configure-roles-for-cloud-service/role-configuration-properties-page-instance-count.png)

1. Hello Visual Studio 中，從工具列上，選取**儲存**。

## <a name="manage-connection-strings-for-storage-accounts"></a>管理儲存體帳戶的連接字串
您可以新增、移除或修改服務組態的連接字串。 例如，針對具有 `UseDevelopmentStorage=true`值的本機服務組態，您可能想要本機連接字串。 您也可以 tooconfigure 在 Azure 中使用的儲存體帳戶的雲端服務組態。

> [!WARNING]
> 當您輸入的儲存體帳戶連接字串的 hello Azure 儲存體帳戶金鑰資訊時，這項資訊儲存在本機 hello 服務組態檔中。 不過，這項資訊目前不會儲存為加密文字。
> 
> 

每個服務組態使用不同的值，執行不在您的雲端服務中有 toouse 不同的連接字串或您發行您的雲端服務 tooAzure 時修改程式碼。 您可以使用相同的名稱，針對您的程式碼和 hello 值中的 hello 的連接字串是不同，根據您選取當您建置您的雲端服務，或將它發行的 hello 服務組態的 hello。

1. 在 Visual Studio 中建立或開啟 Azure 雲端服務專案。

1. 在**方案總管 中**，展開 hello 專案節點。 在 hello**角色**節點、 以滑鼠右鍵按一下您想 tooupdate，並從 hello 內容功能表中，選取 hello 角色**屬性**。

    ![方案總管 Azure 角色操作功能表](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-azure-role-context-menu.png)

1. 選取 hello**設定** 索引標籤。

    ![[設定] 索引標籤](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab.png)

1. 在 hello**服務組態**清單中，您想 tooupdate 選取 hello 服務組態。

    ![服務組態](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-select-configuration.png)

1. tooadd 連接字串中，選取**加入設定**。

    ![新增連接字串](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-add-setting.png)

1. 一旦 hello 新設定已新增 toohello 清單，更新 hello 清單中的 hello 列 hello 必要資訊。

    ![New connection string](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-add-setting-new-setting.png)

    - **名稱**-輸入您要的連接字串 hello toouse hello 名稱。
    - **型別**-選取**連接字串**hello 下拉式清單中。
    - **值**-您可以直接在 hello 輸入 hello 連接字串**值**資料格或選取 hello hello 中的省略符號 （...） toowork**建立儲存體連接字串**對話方塊。  

1. 在 hello**建立儲存體連接字串**對話方塊中，選取一個選項，如**使用連接**。 然後依照您所選取的 hello 選項 hello 指示：

    - **Microsoft Azure 儲存體模擬器**-如果您選取此選項，因為它們會套用只 tooAzure，會停用 hello hello 對話方塊上的其餘設定。 選取 [確定] 。
    - **您的訂用帳戶**-如果您選取此選項，使用 hello 下拉式清單 tooeither 選取和登入 Microsoft 帳戶，或新增 Microsoft 帳戶。 選取 Azure 訂用帳戶和儲存體帳戶。 選取 [確定] 。
    - **手動輸入的認證**-輸入 hello 儲存體帳戶名稱，並請 hello 主要或次要金鑰。 選取 **[連線]** 的 (在大部分情況下建議適用 HTTPS)。選取 [確定] 。

1. toodelete 連接字串中，選取 hello 連接字串，然後選取**移除設定**。

1. Hello Visual Studio 中，從工具列上，選取**儲存**。

## <a name="programmatically-access-a-connection-string"></a>以程式設計方式存取連接字串

hello 下列步驟顯示如何 tooprogrammatically 存取使用 C# 的連接字串。

1. 新增 hello 下列使用指示詞 tooa C# 檔案將 toouse hello 設定：

    ```csharp
    using Microsoft.WindowsAzure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.ServiceRuntime;
    ```

1. hello 下列程式碼說明如何的範例 tooaccess 連接字串。 取代 hello &lt;ConnectionStringName > 預留位置 hello 適當的值。 

    ```csharp
    // Setup hello connection tooAzure Storage
    var storageAccount = CloudStorageAccount.Parse(RoleEnvironment.GetConfigurationSettingValue("<ConnectionStringName>"));
    ```

## <a name="add-custom-settings-toouse-in-your-azure-cloud-service"></a>在 Azure 雲端服務中加入自訂設定 toouse
Hello 服務組態檔中的自訂設定可讓您加入的名稱及針對特定服務的組態字串的值。 您可以選擇您的雲端服務所讀取的 hello 值中的功能 hello 設定以及程式碼中使用此值 toocontrol hello 邏輯這個設定 tooconfigure toouse。 您可以變更這些服務組態值，而不需要 toorebuild 服務封裝，或您的雲端服務正在執行。 您的程式碼可以檢查設定變更時的通知。 請參閱 [RoleEnvironment.Changing 事件](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changing.aspx)。

您可以新增、移除或修改服務組態的自訂設定。 針對不同的服務組態，您可能會想要這些連接字串的不同值。

每個服務組態使用不同的值，請勿不在您的雲端服務中有 toouse 不同的字串或當您發行您的雲端服務 tooAzure 時修改程式碼。 您可以使用相同的名稱，您的程式碼和 hello 值中的 hello 字串是不同，根據您選取當您建置您的雲端服務，或將它發行的 hello 服務組態的 hello。

1. 在 Visual Studio 中建立或開啟 Azure 雲端服務專案。

1. 在**方案總管 中**，展開 hello 專案節點。 在 hello**角色**節點、 以滑鼠右鍵按一下您想 tooupdate，並從 hello 內容功能表中，選取 hello 角色**屬性**。

    ![方案總管 Azure 角色操作功能表](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-azure-role-context-menu.png)

1. 選取 hello**設定** 索引標籤。

    ![[設定] 索引標籤](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab.png)

1. 在 hello**服務組態**清單中，您想 tooupdate 選取 hello 服務組態。

    ![服務組態清單](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-select-configuration.png)

1. tooadd 自訂設定中，選取**加入設定**。

    ![新增自訂設定](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-add-setting.png)

1. 一旦 hello 新設定已新增 toohello 清單，更新 hello 清單中的 hello 列 hello 必要資訊。

    ![新增自訂設定](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-add-setting-new-setting.png)

    - **名稱**-輸入 hello hello 設定名稱。
    - **型別**-選取**字串**hello 下拉式清單中。
    - **值**-輸入 hello hello 設定值。 您可以輸入 hello 值直接插入 hello**值**資料格或選取 hello 省略符號 （...） tooenter hello 值 hello**編輯字串**對話方塊。  

1. toodelete 自訂設定中，選取 hello 設定，然後選取**移除設定**。

1. Hello Visual Studio 中，從工具列上，選取**儲存**。

## <a name="programmatically-access-a-custom-settings-value"></a>以程式設計方式存取自訂設定的值
 
hello 下列步驟顯示如何 tooprogrammatically 存取使用 C# 自訂設定。

1. 新增 hello 下列使用指示詞 tooa C# 檔案將 toouse hello 設定：

    ```csharp
    using Microsoft.WindowsAzure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.ServiceRuntime;
    ```

1. hello 下列程式碼說明如何的範例 tooaccess 自訂設定。 取代 hello &lt;SettingName > 預留位置 hello 適當的值。 
    
    ```csharp
    var settingValue = RoleEnvironment.GetConfigurationSettingValue("<SettingName>");
    ```

## <a name="manage-local-storage-for-each-role-instance"></a>管理每個角色執行個體的本機儲存體
您可以為角色的每個執行個體新增本機檔案系統儲存體。 預存在於儲存體不是可存取哪些 hello 會儲存資料，hello 角色的其他執行個體或其他角色的 hello 資料。  

1. 在 Visual Studio 中建立或開啟 Azure 雲端服務專案。

1. 在**方案總管 中**，展開 hello 專案節點。 在 hello**角色**節點、 以滑鼠右鍵按一下您想 tooupdate，並從 hello 內容功能表中，選取 hello 角色**屬性**。

    ![方案總管 Azure 角色操作功能表](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-azure-role-context-menu.png)

1. 選取 hello**本機儲存體** 索引標籤。

    ![本機儲存體索引標籤](./media/vs-azure-tools-configure-roles-for-cloud-service/role-local-storage-tab.png)

1. 在 hello**服務組態**清單，請確定**所有組態**hello 本機儲存體設定適用於 tooall 服務組態已選取。 任何其他值會導致在 hello 頁面上，已停用的 hello 輸入欄位。 

    ![服務組態清單](./media/vs-azure-tools-configure-roles-for-cloud-service/role-local-storage-tab-service-configuration.png)

1. tooadd 本機儲存體項目中，選取**加入本機儲存體**。

    ![新增本機儲存體](./media/vs-azure-tools-configure-roles-for-cloud-service/role-local-storage-tab-add-local-storage.png)

1. 一旦 hello 新的本機儲存體項目已加入 toohello 清單，更新 hello 清單中的 hello 列 hello 必要資訊。

    ![新增本機儲存體項目](./media/vs-azure-tools-configure-roles-for-cloud-service/role-local-storage-tab-new-local-storage.png)

    - **名稱**-輸入您要 hello 新的本機儲存體 toouse hello 名稱。
    - **大小 (MB)** -輸入 hello 大小以 mb 為單位，您需要的 hello 新的本機存放裝置。
    - **清除在角色回收**-hello hello 角色的虛擬機器回收時，選取此選項 tooremove hello 資料 hello 新區域儲存區中。

1. toodelete 本機儲存體項目中，選取 hello 項目，然後再選取**移除本機儲存體**。

1. Hello Visual Studio 中，從工具列上，選取**儲存**。

## <a name="programmatically-accessing-local-storage"></a>以程式設計方式存取本機儲存體

本節說明如何 tooprogrammatically 存取使用 C# 撰寫測試文字檔案的本機儲存體`MyLocalStorageTest.txt`。  

### <a name="write-a-text-file-toolocal-storage"></a>寫入文字檔案 toolocal 存放裝置

hello，下列程式碼示範如何 toowrite 文字檔案 toolocal 存放裝置。 取代 hello &lt;LocalStorageName > 預留位置 hello 適當的值。 

    ```csharp
    // Retrieve an object that points toohello local storage resource
    LocalResource localResource = RoleEnvironment.GetLocalResource("<LocalStorageName>");
    
    //Define hello file name and path
    string[] paths = { localResource.RootPath, "MyLocalStorageTest.txt" };
    String filePath = Path.Combine(paths);
    
    using (FileStream writeStream = File.Create(filePath))
    {
        Byte[] textToWrite = new UTF8Encoding(true).GetBytes("Testing Web role storage");
        writeStream.Write(textToWrite, 0, textToWrite.Length);
    }

    ```

### <a name="find-a-file-written-toolocal-storage"></a>尋找寫入 toolocal 儲存體的檔案

hello hello 前一節中的程式碼所建立的 tooview hello 檔案，請遵循下列步驟：
    
1.  在 hello Windows 通知區域中 hello Azure 圖示，以滑鼠右鍵按一下，然後從 hello 內容功能表中，選取**顯示計算模擬器 UI**。 

    ![顯示 Azure 計算模擬器](./media/vs-azure-tools-configure-roles-for-cloud-service/show-compute-emulator.png)

1. 選取 hello web 角色。

    ![Azure 計算模擬器](./media/vs-azure-tools-configure-roles-for-cloud-service/compute-emulator.png)

1. 在 hello **Microsoft Azure 計算模擬器**功能表上，選取**工具** > **開啟本機存放區**。

    ![開啟本機存放區功能表項目](./media/vs-azure-tools-configure-roles-for-cloud-service/compute-emulator-open-local-store-menu.png)

1. 當 hello Windows 檔案總管視窗開啟時，請輸入 'MyLocalStorageTest.txt' hello 到**搜尋**文字方塊，然後選取**Enter** toostart hello 搜尋。 

## <a name="next-steps"></a>後續步驟
藉由參閱 [設定 Azure 專案](vs-azure-tools-configuring-an-azure-project.md)深入了解 Visual Studio 中的 Azure 專案。 深入了解 hello 雲端服務結構描述讀取[結構描述參考](https://msdn.microsoft.com/library/azure/dd179398)。

