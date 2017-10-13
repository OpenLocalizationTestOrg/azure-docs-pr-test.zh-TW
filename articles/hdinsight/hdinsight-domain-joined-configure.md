---
title: "設定已加入網域的 HDInsight 叢集 - Azure | Microsoft Docs"
description: "了解如何安裝及設定已加入網域的 HDInsight 叢集"
services: hdinsight
documentationcenter: 
author: saurinsh
manager: jhubbard
editor: cgronlun
tags: 
ms.assetid: 0cbb49cc-0de1-4a1a-b658-99897caf827c
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 11/02/2016
ms.author: saurinsh
ms.openlocfilehash: 9964c3dff24ef8a3a6047fe18c0f36c12c1de33d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="configure-domain-joined-hdinsight-clusters-preview"></a>設定已加入網域的 HDInsight 叢集 (預覽)

了解如何設定 Azure HDInsight 叢集與 Azure Active Directory (Azure AD) 和 [Apache Ranger](http://hortonworks.com/apache/ranger/)，以利用增強式驗證和豐富的角色型存取控制 (RBAC) 原則。  您可以只在 Linux 架構的叢集上設定已加入網域的 HDInsight。 如需詳細資訊，請參閱[已加入網域的 HDInsight 叢集簡介](hdinsight-domain-joined-introduction.md)。

> [!IMPORTANT]
> Oozie 未在已加入網域的 HDInsight 上啟用。

本文是此系列文章的其中一篇：

* 建立連接到已啟用 Apache Ranger 之 Azure AD 的 HDInsight 叢集 (透過 Azure Directory 網域服務功能)。
* 透過 Apache Ranger 建立和套用 Hive 原則，並允許使用者 (如資料科學家) 使用 ODBC 型工具 (如 Excel、Tableau 等) 連線到 Hive。Microsoft 正努力將其他工作負載 (例如 HBase、Spark、Storm) 盡快新增至已加入網域的 HDInsight。

最終的拓樸範例如下：

![已加入網域的 HDInsight 拓樸](./media/hdinsight-domain-joined-configure/hdinsight-domain-joined-topology.png)

因為 Azure AD 目前只支援傳統虛擬網路 (VNet)，而 Linux 架構的 HDInsight 叢集僅支援 Azure Resource Manager 架構的 VNet，HDInsight Azure AD 整合需要兩個 VNet 以及在兩者之間的對等互連。 如需兩種部署模型的比較資訊，請參閱 [Azure Resource Manager 與傳統部署比較：了解資源的部署模型和狀態](../azure-resource-manager/resource-manager-deployment-model.md)。 這兩個 VNet 必須位於與 Azure AD DS 相同的區域中。

Azure 服務名稱必須是全域唯一的。 本教學課程中使用下列名稱。 Contoso 是虛構的名稱。 當您進行本教學課程時，必須將 contoso 取代為其他名稱。 

**名稱︰**

| 屬性 | 值 |
| --- | --- |
| Azure AD VNet |contosoaadvnet |
| Azure AD Vnet 資源群組 |contosoaadrg |
| Azure AD 目錄 |contosoaaddirectory |
| Azure AD 網域名稱 |contoso (contoso.onmicrosoft.com) |
| HDInsight VNet |contosohdivnet |
| HDInsight VNet 資源群組 |contosohdirg |
| HDInsight 叢集 |contosohdicluster |

本教學課程提供「設定已加入網域的 HDInsight 叢集」的步驟。 每一節都有其他文件的連結，以提供更詳細的背景資訊。

## <a name="prerequisite"></a>必要條件：
* 您熟悉 [Azure AD 網域服務](https://azure.microsoft.com/services/active-directory-ds/)及其 [價格](https://azure.microsoft.com/pricing/details/active-directory-ds/)結構。
* 確定您的訂用帳戶已列入此公開預覽版本的允許清單中。 您可以傳送電子郵件與您的訂用帳戶識別碼給 hdipreview@microsoft.com 要求列入。
* SSL 憑證，需由您的網域的簽章授權單位簽署。 設定安全的 LDAP 需有此憑證。 不可使用自我簽署憑證。

## <a name="procedures"></a>程序
1. 為您的 Azure AD 建立 Azure 傳統 VNet。  
2. 建立和設定 Azure AD 與 Azure AD DS。
3. 在 Azure 資源管理模式中建立 HDInsight VNet。
4. 對等互連兩個 VNet。
5. 建立 HDInsight 叢集。

> [!NOTE]
> 本教學課程假設您已沒有 Azure AD。 如果您有的話，可以略過步驟 2 的部分。
> 
> 

有 PowerShell 指令碼可自動執行步驟 3 到步驟 7。  如需詳細資訊，請參閱[使用 Azure PowerShell 設定已加入網域的 HDInsight 叢集](hdinsight-domain-joined-configure-use-powershell.md)。

## <a name="create-an-azure-virtual-network-classic"></a>建立 Azure 虛擬網路 (傳統)
在本節中，您會使用 Azure 入口網站建立虛擬網路 (傳統)。 在下一節，您會啟用虛擬網路中 Azure AD 的 Azure AD DS。 如需下列程序和使用其他虛擬網路建立方法的詳細資訊，請參閱[使用 Azure 入口網站建立虛擬網路 (傳統)](../virtual-network/virtual-networks-create-vnet-classic-pportal.md)。

**建立傳統 VNet**

1. 登入 [Azure 入口網站](https://portal.azure.com)。 
2. 按一下 [新增]  >  [網路]  >  [虛擬網路]。
3. 在 [選取部署模型] 中，選取 [傳統]，然後按一下 [建立]。
4. 輸入或選取下列值：
   
   * **名稱**：contosoaadvnet
   * **位址空間**：10.1.0.0/16
   * **子網路名稱**：Subnet1
   * **子網路位址範圍**：10.1.0.0/24
   * **訂用帳戶**：(選取用來建立此 VNet 的訂用帳戶。)
   * **ResourceGroup**：contosoaadrg
   * **位置**：(選取 HDInsight 叢集的區域。)
     
     > [!IMPORTANT]
     > 您必須選擇支援 Azure AD DS 的位置。 如需詳細資訊，請參閱[不同區域提供的產品](https://azure.microsoft.com/en-us/regions/services/)。 
     > 
     > 傳統 VNet 和資源群組 VNet 皆必須位於與 Azure AD DS 相同的區域。
     > 
     > 
5. 按一下 [建立] 來建立 VNet。

## <a name="create-and-configure-azure-ad-ds-for-your-azure-ad"></a>為您的 Azure AD 建立和設定 Azure AD DS。
在本節中，您將：

1. 建立 Azure AD。
2. 建立 Azure AD 使用者。 這些使用者是網域使用者。 您使用第一位使用者來設定搭配 Azure AD 的 HDInsight 叢集。  其他兩位使用者在本教學課程中都是選擇性的。 當您設定 Apache Ranger 時，您會使用他們來[針對已加入網域的 HDInsight 叢集設定 Hive 原則](hdinsight-domain-joined-run-hive.md)。
3. 建立 AAD DC 系統管理員群組，並將 Azure AD 使用者新增至群組。 您可以使用這位使用者來建立組織單位。
4. 啟用 Azure AD 的 Azure AD 網域服務 (Azure AD DS)。
5. 設定 Azure AD 的 LDAPS。 輕量型目錄存取通訊協定 (LDAP) 是用來從 Azure AD 讀取和寫入 Azure AD。

如果您想要使用現有的 Azure AD，可以略過步驟 1 和 2。

**建立 Azure AD**

1. 在 [Azure 傳統入口網站](https://manage.windowsazure.com)中，按一下 [新增]  >  [應用程式服務]  >  [Active Directory]  >  [目錄]  >  [自訂建立]。 
2. 輸入或選取下列值：
   
   * **名稱**：contosoaaddirectory
   * **網域名稱**：contoso。  此名稱必須是全域唯一的。
   * **國家或區域**：選取您的國家或區域。
3. 按一下頁面底部的 [新增] 。

**建立 Azure AD 使用者**

1. 在 [Azure 傳統入口網站](https://manage.windowsazure.com)中，按一下 [Active Directory]  ->  [contosoaaddirectory]。 
2. 按一下頂端功能表中的 [使用者]。
3. 按一下 [加入使用者] 。
4. 輸入 [使用者名稱]，然後按一下 [下一步]。 
5. 設定使用者設定檔；在 [角色] 選取 [全域管理員]，然後按一下 [下一步]。  需要「全域管理員角色」才能建立組織單位。
6. 按一下 [建立] 取得暫時密碼。
7. 複製一份密碼，然後按一下 [完成]。 在本教學課程稍後，您會使用這個全域管理使用者來建立 HDInsight 叢集。

依照相同程序建立另外兩位使用者，**使用者**角色分別為 hiveuser1 和 hiveuser2。 下列使用者會用於[針對已加入網域的 HDInsight 叢集設定 Hive 原則](hdinsight-domain-joined-run-hive.md)。

**建立 AAD DC 系統管理員群組，並新增 Azure AD 使用者**

1. 在 [Azure 傳統入口網站](https://manage.windowsazure.com)中，按一下 [Active Directory]  >  [contosoaaddirectory]。 
2. 按一下頂端功能表中的 [群組]。
3. 按一下 [新增一個群組] 或 [新增群組]。
4. 輸入或選取下列值：
   
   * **名稱**：AAD DC 系統管理員。  請勿變更群組名稱。
   * **群組類型**：安全性。
5. 按一下頁面底部的 [新增] 。
6. 按一下[AAD DC 系統管理員] 以開啟群組。
7. 按一下[新增成員]。
8. 選取您在前一個步驟建立的第一位使用者，然後按一下 [完成]。
9. 重複相同步驟來建立另一個名為 **HiveUsers** 的群組，並將兩個 Hive 使用者新增至群組。

如需詳細資訊，請參閱[Azure AD 網域服務 (預覽) - 建立「AAD DC 系統管理員」的群組](../active-directory-domain-services/active-directory-ds-getting-started.md)。

**為您的 Azure AD 啟用 Azure AD DS**

1. 在 [Azure 傳統入口網站](https://manage.windowsazure.com)中，按一下 [Active Directory]  >  [contosoaaddirectory]。 
2. 按一下頂端的 [設定]。
3. 向下捲動至 [網域服務]，設定下列值︰
   
   * **啟用此目錄的網域服務**：是。
   * **網域服務的 DNS 網域名稱**︰這會顯示 Azure 目錄的預設 DNS 名稱。 例如，contoso.onmicrosoft.com。
   * **將網域服務連接到此虛擬網路**：選取您稍早建立的傳統虛擬網路，即 **contosoaadvnet**。
4. 按一下頁面底部的 [儲存]。 在 [啟用此目錄的網域服務] 旁您會看到 [擱置中...]。  
5. 等 [擱置中...] 消失，[IP 位址] 就會填入值。 一共會填入兩個 IP 位址。 這些是由網域服務佈建的網域控制站的 IP 位址。 對應的網域控制站佈建並就緒之後，將會顯示每個 IP 位址。 寫下這兩個 IP 位址。 稍後您將需要這些資訊。

如需詳細資訊，請參閱 [Azure AD 網域服務 (預覽) - 啟用 Azure AD 網域服務](../active-directory-domain-services/active-directory-ds-getting-started-enableaadds.md)。

**同步處理密碼**

如果您使用自己的網域，您需要將密碼同步。 請參閱[為僅限雲端的 Azure AD 目錄啟用 Azure AD 網域服務的密碼同步處理](../active-directory-domain-services/active-directory-ds-getting-started-password-sync.md)。

**設定 Azure AD 的 LDAPS**

1. 取得由您的網域的簽章授權單位簽署的 SSL 憑證。 如果您要使用自我簽署憑證，請向 hdipreview@microsoft.com 要求例外處理。
2. 在 [Azure 傳統入口網站](https://manage.windowsazure.com)中，按一下 [Active Directory]  >  [contosoaaddirectory]。 
3. 按一下頂端的 [設定]。
4. 捲動到 [網域服務]。
5. 按一下 [設定憑證]。
6. 依照指示來指定憑證檔案和密碼。 在 [啟用此目錄的網域服務] 旁您會看到 [擱置中...]。  
7. 等 [擱置中...] 消失，[安全 LDAP 憑證] 就會填入值。  這項作業需要 10 分鐘或更久。

> [!NOTE]
> 如果 Azure AD DS 上正在執行某些背景工作，您上傳憑證時可能會看到錯誤 - 此租用戶有作業正在執行。<i>請稍後再試。</i>  如果您遇到這個錯誤，請稍待片刻後再試一次。 佈建第二個網域控制站 IP 可能需要長達 3 小時。
> 
> 

如需詳細資訊，請參閱[針對 Azure AD 網域服務受管理網域設定安全的 LDAP (LDAPS)](../active-directory-domain-services/active-directory-ds-admin-guide-configure-secure-ldap.md)。

## <a name="create-a-resource-manager-vnet-for-hdinsight-cluster"></a>建立用於 HDInsight 叢集的 Resource Manager VNet
在本節中，您會建立將用於 HDInsight 的 Azure Resource Manager VNet。 如需使用其他方法建立 Azure VNet 的詳細資訊，請參閱[建立虛擬網路](../virtual-network/virtual-networks-create-vnet-arm-pportal.md)。

建立 VNet 之後，需將 Azure Resource Manager VNet 設定成使用與 Azure AD VNet 所用的同一 DNS 伺服器。 如果您已遵循本教學課程中的步驟建立傳統 VNet 和 Azure AD，則 DNS 伺服器是 10.1.0.4 和 10.1.0.5。

**建立 Resource Manager VNet**

1. 登入 [Azure 入口網站](https://portal.azure.com)。
2. 依序按一下 [新增]、[網路] 及 [虛擬網路]。 
3. 在 [選取部署模型] 中，選取 [Resource Manager]，然後按一下 [建立]。
4. 輸入或選取下列值：
   
   * **名稱**：contosohdivnet
   * **位址空間**：10.2.0.0/16。 請確定位址範圍沒有與傳統 VNet 的 IP位址範圍重疊。
   * **子網路名稱**：Subnet1
   * **子網路位址範圍**：10.2.0.0/24
   * **訂用帳戶**：(選取您的 Azure 訂用帳戶。)
   * **資源群組**：contosohdirg
   * **位置**：(選取與 Azure AD VNet 相同的位置，也就是 contosoaadvnet。)
5. 按一下 [建立] 。

**設定 Resource Manager VNet 的 DNS**

1. 在 [Azure 入口網站](https://portal.azure.com)中，按一下 [更多服務]  ->  [虛擬網路]。 確定沒有按到 [虛擬網路 (傳統)]。
2. 按一下 [contosohdivnet]。
3. 按一下左側刀鋒視窗中的 [DNS 伺服器]。
4. 按一下 [自訂]，然後輸入下列值︰
   
   * 10.1.0.4
   * 10.1.0.5
     
     這些 DNS 伺服器 IP 位址必須與 Azure AD VNet (傳統 VNet) 中的 DNS 伺服器相符。
5. 按一下 [儲存] 。

## <a name="peer-the-azure-ad-vnet-and-the-hdinsight-vnet"></a>對等互連 Azure AD VNet 和 HDInsight VNet
**對等互連兩個 VNet**

1. 登入 [Azure 入口網站](https://portal.azure.com)。
2. 按一下左側功能表中的 [更多服務]。
3. 按一下 [虛擬網路]。 確定沒有按到 [虛擬網路 (傳統)]。
4. 按一下 [contosohdivnet]。  這是 HDInsight VNet。
5. 按一下刀鋒視窗左側功能表中的 [對等互連]。
6. 按一下頂端功能表中的 [新增]。 [新增對等互連] 刀鋒視窗隨即開啟。
7. 在 [新增對等互連] 刀鋒視窗中，設定或選取下列值：
   
   * **名稱**：ContosoAADHDIVNetPeering
   * **虛擬網路部署模型**︰傳統
   * **訂用帳戶**：選取您用於傳統 (Azure AD) VNet 的訂用帳戶名稱
   * **虛擬網路**：contosoaadvnet
   * **允許虛擬網路存取**：(勾選)
   * **允許轉送的流量**：(勾選)。 其他兩個核取方塊保持未勾選。
8. 按一下 [確定] 。

## <a name="create-hdinsight-cluster"></a>建立 HDInsight 叢集
在本節中，您會使用 Azure 入口網站或 [Azure Resource Manager 範本](../azure-resource-manager/resource-group-template-deploy.md)，在 HDInsight 中建立 Linux 架構的 Hadoop 叢集。 如需其他叢集建立方法及了解各項設定，請參閱 [建立 HDInsight 叢集](hdinsight-hadoop-provision-linux-clusters.md)。 如需有關使用 Resource Manager 範本在 HDInsight 中建立 Hadoop 叢集的詳細資訊，請參閱[使用 Resource Manager 範本在 HDInsight 中建立 Hadoop 叢集](hdinsight-hadoop-create-windows-clusters-arm-templates.md)。

**使用 Azure 入口網站建立已加入網域的 HDInsight 叢集**

1. 登入 [Azure 入口網站](https://portal.azure.com)。
2. 依序選取 [新增]、[情報 + 分析] 及 [HDInsight]。
3. 在 [新增 HDInsight 叢集] 刀鋒視窗中，輸入或選取下列值：
   
   * **叢集名稱**︰為已加入網域的 HDInsight 叢集輸入新叢集名稱。
   * **訂用帳戶**：選取用來建立此叢集的 Azure 訂用帳戶。
   * **叢集組態**：
     
     * **叢集類型**：Hadoop。 目前在 Hadoop 叢集上僅支援已加入網域的 HDInsight。
     * **作業系統**：Linux。  目前在 Linux 架構的 HDInsight 叢集上僅支援已加入網域的 HDInsight。
     * **版本**：HDI 3.6。 在 HDInsight 叢集版本 3.6 上僅支援已加入網域的 HDInsight。
     * **叢集類型**：進階 PREMIUM
       
       按一下 [選取] 儲存變更。
   * **認證**︰設定叢集使用者和 SSH 使用者的認證。
   * **資料來源**：建立新的儲存體帳戶或使用現有的儲存體帳戶，做為 HDInsight 叢集的預設儲存體帳戶。 此位置必須與兩個 VNet 的位置相同。  此位置也是 HDInsight 叢集的位置。
   * **價格**：選取叢集的背景工作角色節點數目。
   * **進階組態**： 
     
     * **加入網域與 VNet/子網路**： 
       
       * **網域設定**： 
         
         * **網域名稱**：contoso.onmicrosoft.com
         * **網域使用者名稱**：輸入網域使用者名稱。 這個網域必須有下列權限︰將電腦加入網域，並將它們放在您於叢集建立期間指定的組織單位內；在您於叢集建立期間指定的組織單位內建立服務主體；建立反向 DNS 項目。 此網域使用者會成為這個已加入網域的 HDInsight 叢集的系統管理員。
         * **網域密碼**︰輸入網域使用者密碼。
         * **組織單位**︰輸入您要搭配 HDInsight 叢集使用的 OU 辨別名稱。 例如：OU=HDInsightOU,DC=contoso,DC=onmicrosoft,DC=com。 如果此 OU 不存在，HDInsight 叢集會嘗試建立這個 OU。 確定 OU 已經存在，或是網域帳戶具有建立新 OU 的權限。 如果您使用屬於 AADDC 系統管理員的網域帳戶，它就已經有建立 OU 的所需權限。
         * **LDAPS URL**：ldaps://contoso.onmicrosoft.com:636
         * **存取使用者群組**︰指定您要將其使用者同步至叢集的安全性群組。 例如，HiveUsers。
           
           按一下 [選取] 儲存變更。
           
           ![已加入網域的 HDInsight 入口網站的設定網域](./media/hdinsight-domain-joined-configure/hdinsight-domain-joined-portal-domain-setting.png)
       * **虛擬網路**：contosohdivnet
       * **子網路**：Subnet1
         
         按一下 [選取] 儲存變更。        
         按一下 [選取] 儲存變更。
   * **資源群組**：選取用於 HDInsight VNet 的資源群組 (contosohdirg)。
4. 按一下 [建立] 。  

建立加入網域的 HDInsight 叢集的另一個選擇，是使用 Azure Resource Management 範本。 下列程序說明做法：

**使用 Azure Resource Manager 範本建立加入網域的 HDInsight 叢集**

1. 在 Azure 入口網站中，按一下以下影像以開啟 Resource Manager 範本。 Resource Manager 範本位於公用 Blob 容器中。 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-domain-joined-hdinsight-cluster.json" target="_blank"><img src="./media/hdinsight-domain-joined-configure/deploy-to-azure.png" alt="Deploy to Azure"></a>
2. 在 [參數] 刀鋒視窗中輸入下列值：
   
   * **訂用帳戶**：(選取您的 Azure 訂用帳戶。)
   * **資源群組**︰ 按一下 [使用現有的]，並指定您剛才使用的同一資源群組。  例如 contosohdirg。 
   * **位置**：指定資源群組的位置。
   * **叢集名稱**：輸入您將建立的 Hadoop 叢集的名稱。 例如 contosohdicluster。
   * **叢集類型**：選取叢集類型。  預設值為 **hadoop**。
   * **位置**：選取叢集的位置。  預設儲存體帳戶會使用相同的位置。
   * **叢集背景工作節點計數**︰選取背景工作角色節點的數目。
   * **叢集登入名稱和密碼**：預設登入名稱是 **admin**。
   * **SSH 使用者名稱和密碼**：預設使用者名稱是 **sshuser**。  您可以將它重新命名。 
   * **虛擬網路識別碼**：/subscriptions/&lt;SubscriptionID>/resourceGroups/&lt;ResourceGroupName>/providers/Microsoft.Network/virtualNetworks/&lt;VNetName>
   * **虛擬網路子網路**：/subscriptions/&lt;SubscriptionID>/resourceGroups/&lt;ResourceGroupName>/providers/Microsoft.Network/virtualNetworks/&lt;VNetName>/subnets/Subnet1
   * **網域名稱**：contoso.onmicrosoft.com
   * **組織單位辨別名稱**：OU=HDInsightOU,DC=contoso,DC=onmicrosoft,DC=com
   * **叢集使用者群組 DN**：[\"HiveUsers\"]
   * **LDAPS URL**：["ldaps://contoso.onmicrosoft.com:636"]
   * **DomainAdminUserName**：(輸入網域系統管理員使用者名稱)
   * **DomainAdminPassword**：(輸入網域系統管理員使用者密碼)
   * **我同意上方所述的條款及條件**：(勾選)
   * **釘選到儀表板**：(勾選)
3. 按一下 [購買]。 您將會看到標題為 [進行範本部署] 的新圖格。 大約需要 20 分鐘的時間來建立叢集。 一旦建立叢集後，您可以在入口網站按一下 [叢集] 刀鋒視窗來開啟它。

完成本教學課程之後，您可以刪除叢集。 利用 HDInsight，您的資料會儲存在 Azure 儲存體中，以便您在未使用叢集時安全地進行刪除。 您也需支付 HDInsight 叢集的費用 (即使未使用)。 由於叢集費用是儲存體費用的許多倍，所以刪除未使用的叢集符合經濟效益。 如需有關刪除叢集的指示，請參閱[使用 Azure 入口網站管理 HDInsight 中的 Hadoop 叢集](hdinsight-administer-use-management-portal.md#delete-clusters)。

## <a name="next-steps"></a>後續步驟
* 如需設定 Hive 原則和執行 Hive 查詢，請參閱[針對已加入網域的 HDInisight 叢集設定 Hive 原則](hdinsight-domain-joined-run-hive.md)。
* 如需使用 SSH 連線到已加入網域的 HDInsight 叢集，請參閱[從 Linux、Unix 或 OS X 在 HDInsight 上搭配使用 SSH 與以 Linux 為基礎的 Hadoop](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined)。

