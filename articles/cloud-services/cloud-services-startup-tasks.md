---
title: "在 Azure 雲端服務的啟動工作 aaaRun |Microsoft 文件"
description: "啟動工作可協助您為應用程式備妥雲端服務環境。 這會告訴您如何啟動工作的工作以及如何 toomake 它們"
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 886939be-4b5b-49cc-9a6e-2172e3c133e9
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: adegeo
ms.openlocfilehash: 3391a5d7434164f59972b8e497e5c34e33409543
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-and-run-startup-tasks-for-a-cloud-service"></a>影響 tooconfigure] 和 [執行啟動工作的雲端服務
在角色啟動之前，您可以使用啟動工作 tooperform 作業。 您可能想 tooperform 的作業包括安裝元件、 註冊 COM 元件、 設定登錄機碼，或啟動長時間執行的處理程序。

> [!NOTE]
> 不適用 tooVirtual 機器，只有 tooCloud 服務 Web 和背景工作角色啟動工作。
> 
> 

## <a name="how-startup-tasks-work"></a>啟動工作的運作方式
啟動工作是您的角色開始，且已定義在 hello 之前採取的動作[ServiceDefinition.csdef]檔案使用 hello[工作]hello 內的項目[啟動]項目。 啟動工作經常是批次檔，但也可以是主控台應用程式，或是啟動 PowerShell 指令碼的批次檔。

環境變數會將資訊傳入啟動工作，並本機儲存體可以是使用的 toopass 從啟動工作的資訊。 例如，環境變數可以指定 hello 路徑 tooa 程式您想 tooinstall，而且可以讀取稍後供您的角色的 toolocal 儲存體可以寫入檔案。

啟動工作可以將資訊和 hello 所指定的錯誤 toohello 目錄記錄**TEMP**環境變數。 Hello 啟動工作，期間 hello **TEMP**環境變數會解析 toohello *c:\\資源\\temp\\[guid]。 [rolename]\\RoleTemp* hello 雲端上執行時的目錄。

啟動工作也可以在重新開機之間執行數次。 例如，hello 角色回收時，每次將執行 hello 啟動工作，而角色回收不一定都包括重新開機。 啟動工作應該寫入外面 toorun 數次不會有問題的方式。

啟動工作的結尾必須**errorlevel** （或結束代碼） 為 hello 啟動處理序 toocomplete 零。 如果啟動工作結束非零值**errorlevel**，hello 角色將不會啟動。

## <a name="role-startup-order"></a>角色啟動順序
hello 以下列出 Azure 中的 hello 角色啟動程序：

1. hello 執行個體標示為**起始**而且不會接收流量。
2. 所有啟動工作會都執行根據 tootheir **taskType**屬性。
   
   * hello**簡單**工作會以同步方式，執行一次。
   * hello**背景**和**前景**工作會以非同步方式啟動的平行 toohello 啟動工作。  
     
     > [!WARNING]
     > IIS 可能未完全設定在 hello 啟動處理序中的 hello 啟動工作階段期間讓角色專屬的資料可能無法使用。 需要特定角色資料的啟動工作應該使用 [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx)。
     > 
     > 
3. hello 角色主機處理序會啟動，且在 IIS 中建立 hello 站台。
4. hello [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx)方法呼叫。
5. hello 執行個體標示為**準備**並且流量會路由的 toohello 執行個體。
6. hello [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.Run](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)方法呼叫。

## <a name="example-of-a-startup-task"></a>啟動工作範例
啟動工作定義在 hello [ServiceDefinition.csdef]檔案，請在 hello**工作**項目。 hello **commandLine**屬性會指定 hello 名稱和參數的 hello 啟動批次檔案或主控台命令，hello **executionContext**屬性會指定 hello hello 啟動權限層級工作及 hello **taskType**屬性會指定 hello 工作執行的方式。

在此範例中，環境變數， **MyVersionNumber**為 hello 啟動工作建立並設定 toohello 值、 「**1.0.0.0**"。

**ServiceDefinition.csdef**：

```xml
<Startup>
    <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple" >
        <Environment>
            <Variable name="MyVersionNumber" value="1.0.0.0" />
        </Environment>
    </Task>
</Startup>
```

在下列範例的 hello，hello **Startup.cmd**批次檔會將 hello 行"hello 新版 is 1.0.0.0"toohello StartupLog.txt 檔案寫入 hello hello TEMP 環境變數所指定的目錄中。 hello`EXIT /B 0`行將確保該 hello 的啟動工作以**errorlevel**為零。

```cmd
ECHO hello current version is %MyVersionNumber% >> "%TEMP%\StartupLog.txt" 2>&1
EXIT /B 0
```

> [!NOTE]
> 在 Visual Studio 中的 hello**複製 tooOutput 目錄**啟動批次檔的屬性應該設定太**永遠複製**toobe 確定啟動批次檔是否正確部署在 Azure 上的 tooyour 專案(**approot\\bin** Web 角色和**approot**背景工作角色)。
> 
> 

## <a name="description-of-task-attributes"></a>工作屬性說明
hello 以下描述的 hello hello 屬性**工作**hello 中的項目[ServiceDefinition.csdef]檔案：

**commandLine** -指定 hello hello 啟動工作的命令列：

* hello 命令，以選擇性的命令列參數開始 hello 啟動工作。
* 這通常是.cmd 或.bat 批次檔的 hello 檔名。
* hello 工作是相對 toohello AppRoot\\hello 部署的 Bin 資料夾。 在決定 hello 路徑和檔案的 hello 工作，不會展開環境變數。 如果需要展開環境變數，可以建立小型 .cmd 指令碼，藉以呼叫啟動工作。
* 可以是主控台應用程式，或啟動 [PowerShell 指令碼](cloud-services-startup-tasks-common.md#create-a-powershell-startup-task)的批次檔。

**executionContext** -指定 hello hello 啟動工作的權限層級。 hello 權限層級可以限制或提高權限：

* **limited**  
  hello 啟動工作執行與 hello 相同 hello 角色權限。 當 hello **executionContext**屬性 hello[執行階段]項目也是**有限**，則會使用使用者的權限。
* **elevated**  
  hello 啟動工作執行系統管理員權限。 這可讓啟動工作 tooinstall 程式、 進行 IIS 組態變更、 執行登錄變更，以及其他系統管理員層級工作，而不會增加權限層級 hello hello 角色本身。  

> [!NOTE]
> hello 的啟動工作的權限層級不需要 toobe hello 相同 hello 角色本身。
> 
> 

**taskType** -指定要執行 hello 方式啟動工作。

* **simple**  
  執行工作時同步執行，一次一個，hello 順序 hello 中指定[ServiceDefinition.csdef]檔案。 當一**簡單**啟動工作以**errorlevel**為零，hello 接下來**簡單**啟動工作的執行。 如果已無其他**簡單**啟動工作 tooexecute，然後將啟動 hello 角色本身。   
  
  > [!NOTE]
  > 如果 hello**簡單**非零值結束工作**errorlevel**，hello 執行個體將會被封鎖。 後續**簡單**啟動工作和 hello 角色本身，將不會啟動。
  > 
  > 
  
    批次檔結尾的 tooensure **errorlevel**為零，執行 hello 命令`EXIT /B 0`hello 批次的檔案處理序的結尾處。
* **background**  
  以非同步方式執行工作與 hello hello 角色啟動並行。
* **foreground**  
  以非同步方式執行工作與 hello hello 角色啟動並行。 hello 之間的主要差異**前景**和**背景**工作是**前景**工作會導致 hello 角色回收或直到 hello 工作已關閉結束。 hello**背景**工作沒有這項限制。

## <a name="environment-variables"></a>環境變數
環境變數是方式 toopass 資訊 tooa 啟動工作。 例如，您可以放入 hello 路徑 tooa blob，其中包含程式 tooinstall，或連接埠號碼，將使用您的角色或啟動工作設定 toocontrol 功能。

有兩種類型的啟動工作; 的環境變數靜態環境變數和環境變數根據成員的 hello [RoleEnvironment]類別。 兩者都是在 hello[環境]區段 hello [ServiceDefinition.csdef]檔案，以及這兩個使用 hello[變數]項目和**名稱**屬性。

靜態環境變數使用 hello**值**屬性 hello[變數]項目。 上述的 hello 範例會建立 hello 環境變數**MyVersionNumber**具有靜態值為"**1.0.0.0**"。 另一個範例就是 toocreate **StagingOrProduction**環境變數，您可以手動設定的 toovalues"**暫存**「 或 」**生產**"tooperform不同的啟動動作為基礎的 hello hello 值**StagingOrProduction**環境變數。

依據的 hello RoleEnvironment 類別成員的環境變數不會使用 hello**值**屬性 hello[變數]項目。 相反地，hello [RoleInstanceValue]子項目，以適當的 hello **XPath**屬性值，根據 hello 的特定成員的環境變數會使用的 toocreate [RoleEnvironment]類別。 值為 hello **XPath**各種屬性 tooaccess [RoleEnvironment]可以找到值[這裡](cloud-services-role-config-xpath.md)。

比方說，toocreate 是環境變數"**true**"hello 執行個體在 hello 計算模擬器中，執行時和"**false**"hello 雲端中執行時，使用 hello 下列[變數]和[RoleInstanceValue]項目：

```xml
<Startup>
    <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple">
        <Environment>

            <!-- Create hello environment variable that informs hello startup task whether it is running
                in hello Compute Emulator or in hello cloud. "%ComputeEmulatorRunning%"=="true" when
                running in hello Compute Emulator, "%ComputeEmulatorRunning%"=="false" when running
                in hello cloud. -->

            <Variable name="ComputeEmulatorRunning">
                <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
            </Variable>

        </Environment>
    </Task>
</Startup>
```

## <a name="next-steps"></a>後續步驟
深入了解如何 tooperform 某些[常見的啟動工作](cloud-services-startup-tasks-common.md)與雲端服務。

[封裝](cloud-services-model-and-package.md) 雲端服務。  

[ServiceDefinition.csdef]: cloud-services-model-and-package.md#csdef
[工作]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Task
[啟動]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Startup
[執行階段]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Runtime
[環境]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Environment
[變數]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Variable
[RoleInstanceValue]: https://msdn.microsoft.com/library/azure/gg557552.aspx#RoleInstanceValue
[RoleEnvironment]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.aspx
