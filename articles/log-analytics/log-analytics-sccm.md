---
title: "Configuration Manager tooLog 分析 aaaConnect |Microsoft 文件"
description: "本文示範 hello 步驟 tooconnect Configuration Manager tooLog 分析和分析資料的開始。"
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: f2298bd7-18d7-4371-b24a-7f9f15f06d66
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/12/2017
ms.author: banders
ms.openlocfilehash: dc50ebc46020a806d99d1a3e3d0e91fd09ad2c32
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-configuration-manager-toolog-analytics"></a>Connect Configuration Manager tooLog 分析
您可以連接 System Center Configuration Manager tooLog 分析 OMS toosync 裝置收集資料。 這可讓 Configuration Manager 階層中的資料可在 OMS 中使用。

## <a name="prerequisites"></a>必要條件

Log Analytics 支援 System Center Configuration Manager 目前分支，1606 版和更高版本。  

## <a name="configuration-overview"></a>組態概觀
hello 步驟摘要說明 hello 程序 tooconnect Configuration Manager tooLog 分析。  

1. 在 hello Azure 管理入口網站中，Configuration Manager 登錄為 Web 應用程式和/或 Web API 的應用程式，並確認您擁有 hello 用戶端識別碼和用戶端秘密金鑰與 Azure Active Directory 中的 hello 註冊。 請參閱[使用入口網站 toocreate Active Directory 應用程式和服務主體可存取資源](../azure-resource-manager/resource-group-create-service-principal-portal.md)如需如何完成此步驟。
2. 在 hello Azure 管理入口網站中， [Configuration Manager （hello 註冊的 web 應用程式） 提供權限 tooaccess OMS](#provide-configuration-manager-with-permissions-to-oms)。
3. 在 Configuration Manager[新增連線使用 hello 加入 OMS 連線精靈](#add-an-oms-connection-to-configuration-manager)。
4. 在 Configuration Manager[更新 hello 連接屬性](#update-oms-connection-properties)如果 hello 密碼或用戶端秘密金鑰曾經過期，或遺失。
5. Hello OMS 入口網站，從資訊[下載並安裝 Microsoft Monitoring Agent hello](#download-and-install-the-agent) hello 電腦執行 hello Configuration Manager 服務連線點站台系統角色。 hello 代理程式會將 Configuration Manager 資料 tooOMS。
6. 在 Log Analytics 中，以電腦群組的形式[從 Configuration Manager 匯入集合](#import-collections)。
7. 在 Log Analytics 中，以電腦群組的形式[從 Configuration Manager 檢視資料](log-analytics-computer-groups.md)。

閱讀更多有關連接在 Configuration Manager tooOMS [Configuration Manager toohello Microsoft Operations Management Suite 中的資料同步](https://technet.microsoft.com/library/mt757374.aspx)。

## <a name="provide-configuration-manager-with-permissions-toooms"></a>Configuration Manager 提供權限 tooOMS
hello 下列程序提供具有權限 tooaccess OMS hello Azure 管理入口網站。 具體來說，您必須授與 hello*參與者角色*hello 資源群組中的順序 tooallow toousers hello Azure 管理入口網站 tooconnect Configuration Manager tooOMS。

> [!NOTE]
> 您必須為 Configuration Manager 指定 OMS 的權限。 否則，您就會收到錯誤訊息 Configuration Manager 中使用 hello 組態精靈。
>
>

1. 開啟 hello [Azure 入口網站](https://portal.azure.com/)按一下**瀏覽** > **記錄分析 (OMS)** tooopen hello 記錄分析 (OMS) 刀鋒視窗。  
2. 在 hello**記錄分析 (OMS)**刀鋒視窗中，按一下 **新增**tooopen hello **OMS 工作區**刀鋒視窗。  
   ![OMS 刀鋒視窗](./media/log-analytics-sccm/sccm-azure01.png)
3. 在 hello **OMS 工作區**刀鋒視窗中，提供下列資訊的 hello，然後按**確定**。

   * **OMS 工作區**
   * **訂用帳戶**
   * **資源群組**
   * **位置**
   * **定價層**  
     ![OMS 刀鋒視窗](./media/log-analytics-sccm/sccm-azure02.png)  

     > [!NOTE]
     > 上述的 hello 範例會建立新的資源群組。 hello 資源群組都只能使用的 tooprovide Configuration Manager 與在此範例中的權限 toohello OMS 工作區。
     >
     >
4. 按一下**瀏覽** > **資源群組**tooopen hello**資源群組**刀鋒視窗。
5. 在 [hello**資源群組**刀鋒視窗中，按一下 hello tooopen hello 先前建立的資源群組&lt;資源群組名稱&gt;設定] 刀鋒視窗。  
   ![資源群組設定刀鋒視窗](./media/log-analytics-sccm/sccm-azure03.png)
6. 在 hello&lt;資源群組名稱&gt;設定刀鋒視窗中，按一下 存取控制 (IAM) tooopen hello&lt;資源群組名稱&gt;使用者 刀鋒視窗。  
   ![資源群組使用者刀鋒視窗](./media/log-analytics-sccm/sccm-azure04.png)  
7. 在 [hello&lt;資源群組名稱&gt;使用者] 刀鋒視窗中，按一下**新增**tooopen hello**新增存取**刀鋒視窗。
8. 在 hello**新增存取**刀鋒視窗中，按一下 **選取角色**，然後選取 hello**參與者**角色。  
   ![選取角色](./media/log-analytics-sccm/sccm-azure05.png)  
9. 按一下**將使用者新增**hello Configuration Manager 使用者進行選取，按一下 **選取**，然後按一下**確定**。  
   ![新增使用者](./media/log-analytics-sccm/sccm-azure06.png)  

## <a name="add-an-oms-connection-tooconfiguration-manager"></a>加入 OMS 連線 tooConfiguration 管理員
在訂單 tooadd OMS 連線，必須具有 Configuration Manager 環境[服務連接點](https://technet.microsoft.com/library/mt627781.aspx)設定為線上模式。

1. 在 hello**管理**工作區的 Configuration Manager，選取**OMS Connector**。 這會開啟 hello**加入 OMS 連線精靈**。 選取 [下一步] 。
2. 在 hello**一般**畫面上，確認您已完成下列動作的 hello 和您擁有詳細資料，每個項目，然後選取 **下一步**。

   1. 在 hello Azure 管理入口網站，您已註冊，Configuration Manager 做為 Web 應用程式和/或 Web API 的應用程式，而且您擁有 hello， [hello 註冊用戶端識別碼](../active-directory/active-directory-integrating-applications.md)。
   2. 在 hello Azure 管理入口網站，您已建立 hello Azure Active Directory 中註冊應用程式的應用程式祕密金鑰。  
   3. Hello Azure 管理入口網站，在您提供了 hello 註冊的 web 應用程式的權限 tooaccess OMS。  
      ![連接 tooOMS 精靈一般頁面](./media/log-analytics-sccm/sccm-console-general01.png)
3. 在 hello **Azure Active Directory**畫面上，設定您的連接設定 tooOMS 藉由提供您**租用戶**，**用戶端識別碼**，和**用戶端秘密金鑰** ，然後選取**下一步**。  
   ![連接 tooOMS 精靈 Azure Active Directory 頁面](./media/log-analytics-sccm/sccm-wizard-tenant-filled03.png)
4. 如果您已完成所有 hello 其他程序成功，然後 hello 有關 hello **OMS 連線設定**畫面會自動出現在此頁面。 Hello 連接設定的資訊應該會出現為您**Azure 訂用帳戶**， **Azure 資源群組**，和**Operations Management Suite 工作區**。  
   ![連接 tooOMS 精靈 OMS 連接 頁面](./media/log-analytics-sccm/sccm-wizard-configure04.png)
5. hello 精靈會連線 toohello OMS 服務使用您已輸入 hello 資訊。 選取您想要使用 OMS toosync，然後按一下 hello 裝置集合**新增**。  
   ![選取集合](./media/log-analytics-sccm/sccm-wizard-add-collections05.png)
6. 確認您的連線設定上 hello**摘要**畫面，然後選取**下一步**。 hello**進度**螢幕會顯示 hello 連接狀態，則應該**完成**。

> [!NOTE]
> 您必須連接 OMS toohello 頂層站台階層中。 如果您連線到 OMS tooa 獨立主要網站，然後再新增管理中心網站 tooyour 環境，您會有 toodelete，並重新建立 hello 新階層中的 hello OMS 連線。
>
>

您已將 Configuration Manager tooOMS 連結之後，您可以新增或移除的集合，並檢視 hello hello OMS 連線屬性。

## <a name="update-oms-connection-properties"></a>更新 OMS 連線屬性
如果曾密碼或用戶端秘密金鑰會過期，或遺失，您將需要 toomanually 更新 hello OMS 連線內容。

1. 在 [組態管理員] 中，瀏覽過**雲端服務**，然後選取**OMS Connector** tooopen hello **OMS 連線內容**頁面。
2. 這個頁面上，按一下 hello **Azure Active Directory**索引標籤上 tooview 您**租用戶**，**用戶端識別碼**，**用戶端秘密金鑰到期**。 **確認****用戶端秘密金鑰**是否已過期。

## <a name="download-and-install-hello-agent"></a>下載並安裝 hello 代理程式
1. 在 hello OMS 入口網站，[下載 hello 代理程式安裝程式檔案從 OMS](log-analytics-windows-agents.md#download-the-agent-setup-file-from-oms)。
2. 使用其中一種下列方法 tooinstall hello hello 代理程式電腦上及設定 hello 執行 hello Configuration Manager 服務連線點站台系統角色：
   * [Hello 使用安裝代理程式安裝程式](log-analytics-windows-agents.md#install-the-agent-using-setup)
   * [Hello 使用安裝代理程式 hello 命令列](log-analytics-windows-agents.md#install-the-agent-using-the-command-line)
   * [安裝在 Azure 自動化中使用 DSC 的 hello 代理程式](log-analytics-windows-agents.md#install-the-agent-using-dsc-in-azure-automation)

## <a name="import-collections"></a>匯入集合
您加入 OMS 連線 tooConfiguration 管理員，並安裝 hello 代理程式後 hello 電腦執行 hello Configuration Manager 服務連線點站台系統角色，hello 下一個步驟是 tooimport 集合從 Configuration Manager 在 OMS 中為電腦群組。

Hello 集合成員資格資訊啟用匯入之後，會擷取每個過去 3 小時內 tookeep hello 集合成員資格目前。 您可以選擇在任何時候 toodisable 匯入作業。

1. 在 hello OMS 入口網站中，按一下 **設定**。
2. 按一下 hello**電腦群組**索引標籤，然後按一下hello **SCCM**  索引標籤。
3. 選取 匯入 Configuration Manager 集合成員資格，然後按一下儲存。  
   ![電腦群組 - SCCM 索引標籤](./media/log-analytics-sccm/sccm-computer-groups01.png)

## <a name="view-data-from-configuration-manager"></a>從 Configuration Manager 檢視資料
在您加入 OMS 連線 tooConfiguration 管理員，並執行 hello Configuration Manager 服務連線點站台系統角色的 hello 電腦上安裝 hello 代理程式之後，從 hello 代理程式的資料會傳送 tooOMS。 在 OMS 中，Configuration Manager 集合會顯示為[電腦群組](log-analytics-computer-groups.md)。 您可以檢視從 hello hello 分組**Configuration Manager**頁面**電腦群組**中**設定**。

之後 hello 匯入集合，您會看到已偵測到多少部電腦與集合成員資格。 您也可以看到已匯入集合的 hello 數目。

![電腦群組 - SCCM 索引標籤](./media/log-analytics-sccm/sccm-computer-groups02.png)

當您按一下其中一個，搜尋會開啟，顯示 hello 的所有匯入群組或屬於 tooeach 群組的所有電腦。 使用 [記錄搜尋](log-analytics-log-searches.md)，您就可以開始深入分析 Configuration Manager 資料。

## <a name="next-steps"></a>後續步驟
* 使用[記錄搜尋](log-analytics-log-searches.md)tooview 詳細的 Configuration Manager 資料的相關資訊。
