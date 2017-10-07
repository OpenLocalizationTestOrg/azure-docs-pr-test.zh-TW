---
title: "透過 Azure 角色的遠端桌面 aaaUsing |Microsoft 文件"
description: "搭配使用遠端桌面與 Azure 角色"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: f5727ebe-9f57-4d7d-aff1-58761e8de8c1
ms.service: multiple
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: d35fd421cde8be9e3caa474db95974a54e528bae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-remote-desktop-with-azure-roles"></a>搭配使用遠端桌面與 Azure 角色
使用 hello Azure SDK 和遠端桌面服務，您可以存取 Azure 角色和 Azure 託管的虛擬機器。 在 Visual Studio 中，您可以從 Azure 雲端服務專案設定遠端桌面服務。 tooenable 遠端桌面服務，您必須建立工作專案包含一個或多個角色，然後將它發行 tooAzure。

> [!IMPORTANT]
> 您應該只基於疑難排解或開發目的來存取 Azure 角色。 hello 每個虛擬機器的用途是 toorun Azure 應用程式中，不 toorun 特定角色的其他用戶端應用程式。 如果您想 toouse Azure toohost 可用於任何用途的虛擬機器，請參閱 < 從伺服器總管存取 Azure 虛擬機器。
> 
> 

## <a name="tooenable-and-use-remote-desktop-for-an-azure-role"></a>tooenable 以及 Azure 角色使用遠端桌面
1. 在 方案總管開啟 hello 雲端服務專案的捷徑功能表，然後選擇 **發行**。
   
    hello**發行 Azure 應用程式**精靈 隨即出現。
   
    ![雲端服務專案的發佈命令](./media/vs-azure-tools-remote-desktop-roles/IC799161.png)
2. 在 hello 底部**Microsoft Azure 發行設定**精靈頁面的 hello 選取 hello**啟用遠端桌面**所有角色的核取方塊。 
   
    hello**遠端桌面組態** 對話方塊隨即出現。
3. 在 hello 底部 hello**遠端桌面組態**對話方塊方塊中，選擇 hello**更多選項** 按鈕。 
   
    這會顯示下拉式清單方塊，可讓您建立或選擇的憑證，以便您在透過遠端桌面連線時可以加密認證資訊。
4. 在 hello 下拉式清單中，選擇  **&lt;建立 >**，或選擇現有從 hello 清單。 
   
    如果您選擇現有的憑證，請略過下列步驟的 hello。
   
   > [!NOTE]
   > hello 憑證所需的遠端桌面連線會與不同 hello 憑證用於其他 Azure 作業。 hello 遠端存取憑證必須具有私密金鑰。
   > 
   > 
   
    hello **Create Certificate**  對話方塊隨即出現。
   
   1. 提供新的憑證，hello 的易記名稱，然後選擇 [hello**確定**] 按鈕。 hello 新憑證會出現在 hello 下拉式清單方塊中。
   2. 在 hello**遠端桌面組態**對話方塊方塊中，提供使用者名稱和密碼。
      
       您無法使用現有的帳戶。 請勿指定系統管理員與 hello hello 新帳戶的使用者名稱。
      
      > [!NOTE]
      > 如果 hello 密碼不符合 hello 複雜性需求下, 一步 toohello 密碼 文字方塊中出現紅色圖示。 hello 密碼必須包含大寫字母、 小寫字母和數字或符號。
      > 
      > 
   3. 選擇在哪一個 hello 帳戶逾期和之後，遠端桌面連線將會遭到封鎖的日期。
   4. 提供所有 hello 必要的資訊之後，選擇 hello**確定** 按鈕。
      
       啟用遠端存取服務的數個設定會加入 toohello.cscfg 和.csdef 檔案。
5. 在 hello **Microsoft Azure 發行設定**精靈 中，選擇 hello **確定**按鈕當你準備 toopublish 您的雲端服務。
   
    如果您不準備 toopublish，請選擇 hello**取消** 按鈕。 hello 組態設定會儲存，而且您可以稍後再發行雲端服務。

## <a name="connect-tooan-azure-role-by-using-remote-desktop"></a>使用遠端桌面連線 tooan Azure 角色
發行 Azure 雲端服務之後，您可以使用伺服器總管 toolog hello 虛擬機器到 Azure 託管。 

1. 在 伺服器總管 中，展開 hello **Azure**  節點，然後展開 雲端服務和其角色 toodisplay 執行個體清單的其中一個 hello 節點。
2. 開啟 hello 一個執行個體節點的捷徑功能表，然後選擇**連接使用的遠端桌面**。
   
    ![透過遠端桌面連接](./media/vs-azure-tools-remote-desktop-roles/IC799162.png)
3. 輸入 hello 使用者名稱和您先前建立的密碼。 您現在已登入遠端工作階段。

