---
title: "應用程式服務-Azure 堆疊中的背景工作角色出 aaaScale |Microsoft 文件"
description: "調整 Azure Stack 應用程式服務的詳細指導方針"
services: azure-stack
documentationcenter: 
author: kathm
manager: slinehan
editor: anwestg
ms.assetid: 3cbe87bd-8ae2-47dc-a367-51e67ed4b3c0
ms.service: azure-stack
ms.workload: app-service
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 4/6/2017
ms.author: kathm
ms.openlocfilehash: 252b4a531655e38f3a3747f8a04b16fc6303f9e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="app-service-on-azure-stack-adding-more-worker-roles"></a>Azure Stack 上的 App Service：新增更多背景工作角色 

本文件提供有關如何指示 tooscale 應用程式服務堆疊 Azure 工作者角色上的。 它包含建立額外的背景工作角色 toosupport 應用程式的任何大小的步驟。

> [!NOTE]
> 如果您 Azure Stack POC 環境的 RAM 未超過 96 GB，您可能很難增加額外的容量。

根據預設值，Azure Stack 上的 App Service 支援免費和共用背景工作角色層。 tooadd 其他背景工作層，您需要 tooadd 更多背景工作角色。

如果您不確定哪些部署時已安裝 Azure 堆疊上的 hello 預設應用程式服務，您可以檢閱 hello 中的其他資訊[應用程式服務在 Azure 堆疊概觀](azure-stack-app-service-overview.md)。

有兩種方式 tooadd 額外容量 tooApp Azure 堆疊上的服務：
1.  [新增其他工作者直接從 hello 應用程式服務資源提供者系統管理員內](#Add-additional-workers-directly-from-within-the-App-Service-Resource-Provider-Admin)。
2.  [手動建立其他 Vm，並將它們加入 toohello 應用程式服務資源提供者](#Create-additional-VMs-manually-and-add-them-to-the-App-Service-Resource-Provider)。

## <a name="add-additional-workers-directly-within-hello-app-service-resource-provider-admin"></a>加入額外的背景工作，直接在 hello 應用程式服務資源提供者系統管理員。

1.  登入 toohello 堆疊 Azure 入口網站以 hello 服務系統管理員身分。
2.  瀏覽過**資源提供者**和選取 hello**應用程式服務資源提供者系統管理員**。![Azure Stack 資源提供者][1]
3.  按一下 [角色]。  這裡您會看到所有的應用程式服務角色部署的 hello 分解。
4.  按一下 hello 選項**新的角色執行個體**![新增新的角色執行個體][2]
5.  在 hello**新的角色執行個體**刀鋒視窗中：
    1. 選擇多少其他**角色執行個體**希望 tooadd。  在 hello 預覽中，沒有最多 10 個。
    2. 選取 hello**角色類型**。  在此預覽中，這個選項會限制的 tooWeb 背景工作。
    3. 選取 hello**背景工作層**希望 toodeploy 這個工作者，預設的選項是小型、 中型、 大型 或共用。  如果您已建立自己的背景工作層，也可選取您的背景工作層。
    4. 按一下**確定**toodeploy hello 額外的背景工作
6.  Hello 其他 Vm，請將其設定、 安裝 hello 所需的所有軟體，將它們標示為已備妥，完成此程序時，現在將加入 Azure 堆疊會在應用程式服務。  此程序大約需要 80 分鐘。
7.  您可以藉由檢視 hello 工作者在 hello 監視 hello hello 整備 hello 新背景工作的進度**角色**刀鋒視窗。

>[!NOTE]
>  在此預覽中，hello 整合新的角色執行個體流程有限的 tooWorker 角色並將 Vm 部署的大小只 A1。  我們將在未來版本中擴充此功能。

## <a name="manually-adding-additional-capacity-tooapp-service-on-azure-stack"></a>手動新增額外的容量 tooApp Azure 堆疊上的服務。

hello 下列步驟是必要的 tooadd 其他角色：

1. [建立新的虛擬機器](#step-1-create-a-new-vm-to-support-the-new-instance-size)
2. [Hello 虛擬機器設定](#step-2-configure-the-virtual-machine)
3. [在 hello Azure 堆疊入口網站中設定 hello web 背景工作角色](#step-3-configure-the-web-worker-role-in-the-azure-stack-portal)
4. [設定 App Service 方案](#step-4-configure-app-service-plans)

## <a name="step-1-create-a-new-vm-toosupport-hello-new-instance-size"></a>步驟 1： 建立新 VM toosupport hello 新執行個體的大小
建立虛擬機器中所述[本文](azure-stack-provision-vm.md)，確保 hello 下列則會選取：

* 使用者名稱和密碼： 提供 hello 相同使用者名稱和您在安裝 Azure 堆疊上的應用程式服務時，您提供的密碼。
* 訂用帳戶： 使用 hello 預設提供者訂用帳戶。
* 資源群組：選擇 [AppService-LOCAL]。

> [!NOTE]
> 將背景工作角色的 hello 虛擬機器儲存在 hello Azure 堆疊上的應用程式服務相同資源群組部署至。 (這是適用於此版本的建議作法)。
> 
> 

## <a name="step-2-configure-hello-virtual-machine"></a>步驟 2： 設定 hello 虛擬機器
Hello 部署完成後，請 hello 下列組態會是必要的 toosupport hello web 背景工作角色：

1. 瀏覽 toohello **AppService 本機**hello 入口網站和選取 hello 您在步驟 1 中建立新的機器中的資源群組。
2. 按一下 [連線] hello VM 刀鋒視窗 toodownload hello 遠端桌面設定檔中。  開啟 hello 設定檔 tooopen 遠端桌面工作階段 tooyour VM。
3. 登入 toohello VM hello 使用者名稱和您在步驟 1 中指定的密碼。
4. 開啟 PowerShell，依序按一下 hello**啟動**按鈕並輸入 PowerShell。 以滑鼠右鍵按一下**PowerShell.exe**，然後選取**系統管理員身分執行**tooopen PowerShell 以系統管理員模式。
5. 複製和貼上每個 hello 到 hello PowerShell 視窗，然後按下列命令 （一次一個） 的輸入：
   
   ```netsh advfirewall firewall set rule group="File and Printer Sharing" new enable=Yes```
   ```netsh advfirewall firewall set rule group="Windows Management Instrumentation (WMI)" new enable=yes```
   ```reg add HKLM\\SOFTWARE\\Microsoft\\Windows\\CurrentVersion\\Policies\\system /v LocalAccountTokenFilterPolicy /t REG\_DWORD /d 1 /f```
   
6. 關閉您的遠端桌面工作階段。
7. 重新啟動 hello VM 從 hello 入口網站。

> [!NOTE]
> 這些是針對 Azure Stack 上之 App Service 的最低需求。 它們是 hello hello Azure 堆疊所包含的 Windows 2012 R2 映像的預設設定。 已提供 hello 指示供日後參考，並使用不同的影像。
> 
> 

## <a name="step-3-configure-hello-worker-role-in-hello-azure-stack-portal"></a>步驟 3: Hello Azure 堆疊入口網站中設定 hello 背景工作角色
1. 在 hello 服務系統管理員身分開啟 hello 入口網站**ClientVM**。
2. 瀏覽過**資源提供者** &gt; **應用程式服務資源提供者系統管理員**。![應用程式服務資源提供者管理][3]
3. 在 hello 設定刀鋒視窗中，按一下 **角色**。![應用程式服務資源提供者角色][4]
4. 按一下 [新增角色執行個體]。
5. 中的 hello 文字方塊**伺服器名稱**輸入 hello **IP 位址**hello 伺服器稍早 （區段 1) 中所建立。
6. 選取 hello**角色類型**希望 tooadd-控制器、 管理伺服器、 前端、 Web 背景工作、 發行者或檔案伺服器。  在此範例中，請選取 [Web 背景工作]。
7. 按一下 hello**層**會像 toodeploy hello 的新執行個體太 （小型、 中型、 大型或共用）。  如果您已建立自己的背景工作層，也可選取這些背景工作層。
8. 按一下 [確定]。
9. 返回 toohello**角色**檢視
10. 按一下 hello 資料列對應 toohello 角色類型和背景工作層的組合，您指派至 VM。
11. 尋找 hello 您剛才加入的伺服器名稱。 檢閱 hello 狀態 資料行，並等候 toomove toohello 下一個步驟，直到 hello 狀態是 「 就緒 」。 這大約需要 80 分鐘。 ![App Service 資源提供者角色就緒][5]

## <a name="step-4-configure-app-service-plans"></a>步驟 4：設定 App Service 方案

1. 登入上 hello ClientVM toohello 入口網站。
2. 瀏覽過**新增** &gt; **Web 和行動裝置版**。
3. 選取 hello 類型的應用程式中，您想要 toodeploy。
4. 提供 hello hello 應用程式的資訊，然後選取**應用程式服務方案 / 位置**。
    1. 按一下 [新建] 。
    2. 建立您的計劃中，然後再選取 hello 相對應的定價層 hello 計劃。

> [!NOTE]
> 您可以在此刀鋒視窗上建立多個方案。 您部署，但是之前, 請確定您已選取 hello 適當的計畫。
> 
> 

hello 下列預設會顯示 hello 的範例可以使用多個定價層。  您注意到，是否有特定的背景工作層沒有可用的背景工作，對應的定價層 hello 選項 toochoose hello 就無法使用。![Azure Stack 上的 App Service 預設定價層][6]

<!--Image references-->
[1]: ./media/azure-stack-app-service-add-worker-roles/azure-stack-resource-providers.png
[2]: ./media/azure-stack-app-service-add-worker-roles/app-service-new-role-instance.png
[3]: ./media/azure-stack-app-service-add-worker-roles/app-service-resource-provider-admin.png
[4]: ./media/azure-stack-app-service-add-worker-roles/app-service-resource-provider-roles.png
[5]: ./media/azure-stack-app-service-add-worker-roles/app-service-resource-provider-role-ready.png
[6]: ./media/azure-stack-app-service-add-worker-roles/app-service-resource-provider-pricing-tier.png
