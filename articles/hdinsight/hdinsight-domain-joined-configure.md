---
title: "aaaConfigure 已加入網域的 HDInsight 叢集 Azure |Microsoft 文件"
description: "深入了解如何 tooset 安裝及設定已加入網域的 HDInsight 叢集"
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
ms.openlocfilehash: 8c4b3d269a7662d27a49b839e5cd05a3e24f7023
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-domain-joined-hdinsight-clusters-preview"></a>設定已加入網域的 HDInsight 叢集 (預覽)

了解如何註冊 Azure HDInsight tooset 叢集與 Azure Active Directory (Azure AD) 和[Apache Ranger](http://hortonworks.com/apache/ranger/) tootake 善用增強式驗證及豐富的角色型存取控制 (RBAC) 原則。  您可以只在 Linux 架構的叢集上設定已加入網域的 HDInsight。 如需詳細資訊，請參閱[已加入網域的 HDInsight 叢集簡介](hdinsight-domain-joined-introduction.md)。

> [!IMPORTANT]
> Oozie 未在已加入網域的 HDInsight 上啟用。

本文是 hello 的一系列的第一個教學課程：

* 建立 Apache Ranger 啟用 （透過 hello Azure Directory 網域服務功能） HDInsight 叢集連線 tooAzure AD。
* 建立和套用 Hive 原則透過 Apache 廣，且可讓使用者 （例如，資料科學家） tooconnect tooHive 使用 ODBC 為基礎的工具，例如 Excel、 Tableau 等等。Microsoft 努力加入其他工作負載，例如 HBase、 Spark，和 Storm、 tooDomain 聯結 HDInsight 很快。

Hello 最終拓撲的範例如下所示：

![已加入網域的 HDInsight 拓樸](./media/hdinsight-domain-joined-configure/hdinsight-domain-joined-topology.png)

因為 Azure AD 目前只支援傳統虛擬網路 (VNet)，而 Linux 架構的 HDInsight 叢集僅支援 Azure Resource Manager 架構的 VNet，HDInsight Azure AD 整合需要兩個 VNet 以及在兩者之間的對等互連。 Hello hello 兩個部署模型之間的比較資訊，請參閱[Azure Resource Manager vs 傳統部署： 了解部署模型及 hello 資源的狀態](../azure-resource-manager/resource-manager-deployment-model.md)。 兩個 Vnet 必須在 hello hello 與 hello Azure AD DS 相同的區域。

Azure 服務名稱必須是全域唯一的。 本教學課程中，會使用下列名稱的 hello。 Contoso 是虛構的名稱。 您必須取代*contoso*具有不同名稱，當您瀏覽 hello 教學課程。 

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

本教學課程提供 hello 步驟設定已加入網域的 HDInsight 叢集。 每個區段有連結 tooother 發行項的詳細背景資訊。

## <a name="prerequisite"></a>必要條件：
* 您熟悉 [Azure AD 網域服務](https://azure.microsoft.com/services/active-directory-ds/)及其 [價格](https://azure.microsoft.com/pricing/details/active-directory-ds/)結構。
* 確定您的訂用帳戶已列入此公開預覽版本的允許清單中。 您可以傳送電子郵件toohdipreview@microsoft.com與您的訂用帳戶 id。
* SSL 憑證，需由您的網域的簽章授權單位簽署。 hello 憑證所需的設定安全 LDAP。 不可使用自我簽署憑證。

## <a name="procedures"></a>程序
1. 為您的 Azure AD 建立 Azure 傳統 VNet。  
2. 建立和設定 Azure AD 與 Azure AD DS。
3. 在 hello Azure 資源管理模式中建立 HDInsight VNet。
4. 對等 hello 兩個 Vnet。
5. 建立 HDInsight 叢集。

> [!NOTE]
> 本教學課程假設您已沒有 Azure AD。 如果有的話，您可以略過步驟 2 中的 hello 部分。
> 
> 

有 PowerShell 指令碼可自動執行步驟 3 到步驟 7。  如需詳細資訊，請參閱[使用 Azure PowerShell 設定已加入網域的 HDInsight 叢集](hdinsight-domain-joined-configure-use-powershell.md)。

## <a name="create-an-azure-virtual-network-classic"></a>建立 Azure 虛擬網路 (傳統)
在本節中，您可以建立虛擬網路 （傳統） 使用 hello Azure 入口網站。 在 hello 下一節中，您可以啟用 hello Azure AD DS hello 虛擬網路中您 Azure ad。 如需 hello 遵循程序，並使用其他虛擬網路建立方法的詳細資訊，請參閱[利用 hello Azure 入口網站建立虛擬網路 （傳統）](../virtual-network/virtual-networks-create-vnet-classic-pportal.md)。

**toocreate 傳統的 VNet**

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。 
2. 按一下 [新增]  >  [網路]  >  [虛擬網路]。
3. 在 選取部署模型 中，選取 傳統，然後按一下建立。
4. 輸入或選取下列值的 hello:
   
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
     > 同時 hello 傳統 VNet 而且 hello 資源群組 VNet 必須在 hello 與 hello Azure AD DS 相同的區域。
     > 
     > 
5. 按一下**建立**toocreate hello VNet。

## <a name="create-and-configure-azure-ad-ds-for-your-azure-ad"></a>為您的 Azure AD 建立和設定 Azure AD DS。
在本節中，您將：

1. 建立 Azure AD。
2. 建立 Azure AD 使用者。 這些使用者是網域使用者。 您可以使用 hello 第一位使用者設定以 hello Azure AD 的 hello HDInsight 叢集。  hello 其他兩個使用者是選擇性的在本教學課程。 當您設定 Apache Ranger 時，您會使用他們來[針對已加入網域的 HDInsight 叢集設定 Hive 原則](hdinsight-domain-joined-run-hive.md)。
3. 建立 hello AAD DC Administrators 群組，並新增 hello Azure AD 使用者 toohello 群組。 您使用這個使用者 toocreate hello 組織單位。
4. 啟用 hello Azure AD 的 Azure AD 網域服務 (Azure AD DS)。
5. 設定 LDAPS hello Azure AD。 hello 輕量型目錄存取通訊協定 (LDAP) 是從使用的 tooread 和撰寫 tooAzure AD。

如果您偏好 toouse 的現有 Azure AD，您可以略過步驟 1 和 2。

**Azure AD 的 toocreate**

1. 從 hello [Azure 傳統入口網站](https://manage.windowsazure.com)，按一下 **新增** > **應用程式服務** > **Active Directory**  > **目錄** > **自訂建立**。 
2. 輸入或選取下列值的 hello:
   
   * **名稱**：contosoaaddirectory
   * **網域名稱**：contoso。  此名稱必須是全域唯一的。
   * **國家或區域**：選取您的國家或區域。
3. 按一下頁面底部的 [新增] 。

**建立 Azure AD 使用者**

1. 從 hello [Azure 傳統入口網站](https://manage.windowsazure.com)，按一下  **Active Directory** -> **contosoaaddirectory**。 
2. 按一下**使用者**從 hello 上方的功能表。
3. 按一下 [加入使用者] 。
4. 輸入 使用者名稱，然後按一下下一步。 
5. 設定使用者設定檔；在 角色 選取 全域管理員，然後按一下下一步。  hello 全域管理員角色是需要的 toocreate 組織單位。
6. 按一下**建立**tooget 暫時密碼。
7. 建立一份 hello 密碼，然後按一下**完成**。 稍後在本教學課程中，您將使用此全域系統管理員使用者 toocreate hello HDInsight 叢集。

後續 hello 相同的程序 toocreate 兩個的多個使用者以 hello**使用者**角色、 hiveuser1 和 hiveuser2。 hello 下列使用者將會使用[設定 hive 控制檔的原則，已加入網域的 HDInsight 叢集的](hdinsight-domain-joined-run-hive.md)。

**toocreate hello AAD DC Administrators' 群組，然後加入 Azure AD 使用者**

1. 從 hello [Azure 傳統入口網站](https://manage.windowsazure.com)，按一下  **Active Directory** > **contosoaaddirectory**。 
2. 按一下**群組**從 hello 上方的功能表。
3. 按一下 [新增一個群組] 或 [新增群組]。
4. 輸入或選取下列值的 hello:
   
   * **名稱**：AAD DC 系統管理員。  請不要變更 hello 群組名稱。
   * **群組類型**：安全性。
5. 按一下頁面底部的 [新增] 。
6. 按一下**AAD DC 管理員**tooopen hello 群組。
7. 按一下[新增成員]。
8. 選取 hello hello 前一個步驟中建立的第一個使用者，然後按一下**完成**。
9. Hello 重複相同步驟 toocreate 另一個群組稱為**HiveUsers**，並加入兩個 hello Hive 使用者 toohello 群組。

如需詳細資訊，請參閱[Azure AD 網域服務 (Preview)-建立 hello ' AAD DC Administrators' 群組](../active-directory-domain-services/active-directory-ds-getting-started.md)。

**您的 Azure AD 的 tooenable Azure AD DS**

1. 從 hello [Azure 傳統入口網站](https://manage.windowsazure.com)，按一下  **Active Directory** > **contosoaaddirectory**。 
2. 按一下**設定**從 hello 上方的功能表。
3. 向下捲動太**網域服務**，並設定 hello 遵循值：
   
   * **啟用此目錄的網域服務**：是。
   * **網域服務的 DNS 網域名稱**： 這會顯示 hello Azure directory hello 預設 DNS 名稱。 例如，contoso.onmicrosoft.com。
   * **網域服務 toothis 虛擬網路連線**： 選取 hello 傳統您稍早建立的虛擬網路也就是**contosoaadvnet**。
4. 按一下**儲存**從 hello hello 頁面的底部。 您會看到**暫止...**下一步太**啟用這個目錄的網域服務**。  
5. 等 [擱置中...] 消失，[IP 位址] 就會填入值。 一共會填入兩個 IP 位址。 這些是 hello hello 佈建的網域服務的網域控制站的 IP 位址。 Hello 對應的網域控制站已佈建並就緒之後，會顯示每個 IP 位址。 記下 hello 兩個 IP 位址。 稍後您將需要這些資訊。

如需詳細資訊，請參閱 [Azure AD 網域服務 (預覽) - 啟用 Azure AD 網域服務](../active-directory-domain-services/active-directory-ds-getting-started-enableaadds.md)。

**toosynchronize 密碼**

如果您使用您自己的網域，您會需要 toosynchronize hello 密碼。 請參閱[啟用密碼同步處理 tooAzure AD 網域服務中的 僅限雲端的 Azure AD 目錄](../active-directory-domain-services/active-directory-ds-getting-started-password-sync.md)。

**tooconfigure LDAPS hello Azure AD**

1. 取得由您的網域的簽章授權單位簽署的 SSL 憑證。 如果您想 toouse 自我簽署憑證，請聯繫toohdipreview@microsoft.com例外狀況。
2. 從 hello [Azure 傳統入口網站](https://manage.windowsazure.com)，按一下  **Active Directory** > **contosoaaddirectory**。 
3. 按一下**設定**從 hello 上方的功能表。
4. 捲動太**網域服務**。
5. 按一下 [設定憑證]。
6. 請遵循 hello 指示 toospecify hello 憑證檔案和 hello 密碼。 您會看到**暫止...**下一步太**啟用這個目錄的網域服務**。  
7. 等 [擱置中...] 消失，[安全 LDAP 憑證] 就會填入值。  這項作業需要 10 分鐘或更久。

> [!NOTE]
> 如果 hello Azure AD DS 上正在執行某些背景工作，您可能會看到錯誤時正在上傳憑證-<i>沒有正在執行此租用戶的作業。請稍後再試。</i>  如果您遇到這個錯誤，請稍待片刻後再試一次。 第二個網域控制站 IP 可能佔用 too3 小時 toobe 佈建的 hello。
> 
> 

如需詳細資訊，請參閱[針對 Azure AD 網域服務受管理網域設定安全的 LDAP (LDAPS)](../active-directory-domain-services/active-directory-ds-admin-guide-configure-secure-ldap.md)。

## <a name="create-a-resource-manager-vnet-for-hdinsight-cluster"></a>建立用於 HDInsight 叢集的 Resource Manager VNet
在本節中，您將建立 Azure 資源管理員 VNet 用於 hello HDInsight 叢集。 如需使用其他方法建立 Azure VNet 的詳細資訊，請參閱[建立虛擬網路](../virtual-network/virtual-networks-create-vnet-arm-pportal.md)。

建立 hello VNet 之後, 您將設定資源管理員 VNet toouse hello 做為相同的 DNS 伺服器，Azure AD VNet hello。 如果您遵循此教學課程 toocreate 中的 hello 步驟 hello 傳統 VNet 和 hello Azure AD，hello DNS 伺服器在 10.1.0.4 且 10.1.0.5。

**toocreate 資源管理員 VNet**

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。
2. 依序按一下 [新增]、[網路] 及 [虛擬網路]。 
3. 在 選取部署模型 中，選取 Resource Manager，然後按一下建立。
4. 輸入或選取下列值的 hello:
   
   * **名稱**：contosohdivnet
   * **位址空間**：10.2.0.0/16。 請確定 hello 位址範圍不能與 hello hello IP 位址範圍重疊傳統的 VNet。
   * **子網路名稱**：Subnet1
   * **子網路位址範圍**：10.2.0.0/24
   * **訂用帳戶**：(選取您的 Azure 訂用帳戶。)
   * **資源群組**：contosohdirg
   * **位置**: (如 hello Azure AD 的 VNet，也就是 contosoaadvnet 選取 hello 相同的位置)。
5. 按一下 [建立] 。

**資源管理員 VNet hello tooconfigure DNS**

1. 從 hello [Azure 入口網站](https://portal.azure.com)，按一下 **更多服務** -> **虛擬網路**。 請確定未 tooclick**虛擬網路 （傳統）**。
2. 按一下 [contosohdivnet]。
3. 按一下**DNS 伺服器**從 hello hello 新刀鋒視窗的左邊。
4. 按一下**自訂**，然後輸入 hello 下列值：
   
   * 10.1.0.4
   * 10.1.0.5
     
     這些 DNS 伺服器 IP 位址必須符合 toohello hello Azure AD VNet (傳統 VNet) 中的 DNS 伺服器。
5. 按一下 [儲存] 。

## <a name="peer-hello-azure-ad-vnet-and-hello-hdinsight-vnet"></a>對等 hello Azure AD VNet 與 hello HDInsight VNet
**toopeer hello 兩個 VNet**

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。
2. 按一下**更多服務**hello 左側功能表中。
3. 按一下 [虛擬網路]。 確定沒有按到 [虛擬網路 (傳統)]。
4. 按一下 [contosohdivnet]。  這是 hello HDInsight VNet。
5. 按一下**對等互連**hello 左窗格中的 hello 刀鋒視窗上。
6. 按一下**新增**從 hello 上方的功能表。 它會開啟 hello**加入對等互連**刀鋒視窗。
7. 在 hello**新增對等互連**刀鋒視窗中，設定或選取 hello 下列值：
   
   * **名稱**：ContosoAADHDIVNetPeering
   * **虛擬網路部署模型**︰傳統
   * **訂用帳戶**： 選取用於 hello 傳統 (Azure AD) vnet 您訂用帳戶名稱。
   * **虛擬網路**：contosoaadvnet
   * **允許虛擬網路存取**：(勾選)
   * **允許轉送的流量**：(勾選)。 不要 hello 其他兩個核取方塊選取。
8. 按一下 [確定] 。

## <a name="create-hdinsight-cluster"></a>建立 HDInsight 叢集
在本節中，您建立使用任一 hello Azure 入口網站的 HDInsight 中的 linux Hadoop 叢集或[Azure Resource Manager 範本](../azure-resource-manager/resource-group-template-deploy.md)。 適用於其他叢集建立方法，並了解 hello 設定，請參閱[建立 HDInsight 叢集](hdinsight-hadoop-provision-linux-clusters.md)。 如需有關使用資源管理員範本 toocreate Hadoop 叢集 HDInsight 中，請參閱 <<c0> [ 建立 Hadoop 叢集 HDInsight 使用資源管理員範本中](hdinsight-hadoop-create-windows-clusters-arm-templates.md)

**已加入網域的 HDInsight 叢集使用 toocreate hello Azure 入口網站**

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。
2. 依序選取 [新增]、[情報 + 分析] 及 [HDInsight]。
3. 從 hello**新的 HDInsight 叢集**刀鋒視窗中，輸入或選取下列值的 hello:
   
   * **叢集名稱**： 輸入新的叢集名稱 hello 已加入網域的 HDInsight 叢集。
   * **訂用帳戶**：選取用來建立此叢集的 Azure 訂用帳戶。
   * **叢集組態**：
     
     * **叢集類型**：Hadoop。 目前在 Hadoop 叢集上僅支援已加入網域的 HDInsight。
     * **作業系統**：Linux。  目前在 Linux 架構的 HDInsight 叢集上僅支援已加入網域的 HDInsight。
     * **版本**：HDI 3.6。 在 HDInsight 叢集版本 3.6 上僅支援已加入網域的 HDInsight。
     * **叢集類型**：進階 PREMIUM
       
       按一下**選取**toosave hello 變更。
   * **認證**： 設定 hello hello 叢集使用者和 hello SSH 使用者的認證。
   * **資料來源**： 建立新的儲存體帳戶，或使用現有的儲存體帳戶，如 hello hello HDInsight 叢集的預設儲存體帳戶。 hello 位置必須 hello 與 hello 兩個 Vnet 相同。  hello 位置也是 hello 的位置 hello HDInsight 叢集。
   * **定價**： 選取叢集的背景工作角色節點的 hello 數目。
   * **進階組態**： 
     
     * **加入網域與 VNet/子網路**： 
       
       * **網域設定**： 
         
         * **網域名稱**：contoso.onmicrosoft.com
         * **網域使用者名稱**：輸入網域使用者名稱。 這個網域必須擁有下列權限的 hello： 加入機器 toohello 網域，並將它們放在您指定在叢集建立; 期間 hello 組織單位建立您指定在叢集建立; 期間 hello 組織單位內的服務主體建立反向 DNS 項目。 此網域的使用者將會變成此網域的 HDInsight 叢集的 hello 系統管理員。
         * **網域密碼**： 輸入 hello 網域使用者密碼。
         * **組織單位**： 輸入您想要與 HDInsight 叢集 toouse OU hello hello 辨別的名稱。 例如：OU=HDInsightOU,DC=contoso,DC=onmicrosoft,DC=com。如果不存在這個 OU，HDInsight 叢集會 toocreate 這個 OU。 請確定 hello OU 已經存在，或 hello 網域帳戶的權限 toocreate 新建一個。 如果您使用 hello 網域帳戶的一部分 AADDC 系統管理員，它將具有必要的權限 toocreate hello OU。
         * **LDAPS URL**：ldaps://contoso.onmicrosoft.com:636
         * **存取使用者群組**： 指定 hello 安全性群組的使用者想 toosync toohello 叢集。 例如，HiveUsers。
           
           按一下**選取**toosave hello 變更。
           
           ![已加入網域的 HDInsight 入口網站的設定網域](./media/hdinsight-domain-joined-configure/hdinsight-domain-joined-portal-domain-setting.png)
       * **虛擬網路**：contosohdivnet
       * **子網路**：Subnet1
         
         按一下**選取**toosave hello 變更。        
         按一下**選取**toosave hello 變更。
   * **資源群組**： 選取 hello hello HDInsight VNet (contosohdirg) 所使用的資源群組。
4. 按一下 [建立] 。  

建立加入網域的 HDInsight 叢集的另一個選項是 toouse Azure 資源管理範本。 下列程序的 hello 為您示範如何：

**toocreate 使用資源管理範本的已加入網域的 HDInsight 叢集**

1. 按一下下列映像 tooopen Resource Manager 範本使用 hello Azure 入口網站中的 hello。 hello Resource Manager 範本位於 公用 blob 容器中。 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-domain-joined-hdinsight-cluster.json" target="_blank"><img src="./media/hdinsight-domain-joined-configure/deploy-to-azure.png" alt="Deploy tooAzure"></a>
2. 從 hello**參數**刀鋒視窗中，輸入下列值的 hello:
   
   * **訂用帳戶**：(選取您的 Azure 訂用帳戶。)
   * **資源群組**： 按一下**使用現有**，並指定 hello 已經使用相同的資源群組。  例如 contosohdirg。 
   * **位置**：指定資源群組的位置。
   * **叢集名稱**： 輸入您要建立 hello Hadoop 叢集的名稱。 例如 contosohdicluster。
   * **叢集類型**：選取叢集類型。  hello 預設值是**hadoop**。
   * **位置**： 選取 hello 叢集的位置。  hello 預設儲存體帳戶使用 hello 相同的位置。
   * **叢集背景工作節點計數**： 選取 hello 背景工作節點數。
   * **叢集登入名稱和密碼**: hello 預設登入名稱是**admin**。
   * **SSH 使用者名稱和密碼**: hello 預設使用者名稱是**sshuser**。  您可以將它重新命名。 
   * **虛擬網路識別碼**：/subscriptions/&lt;SubscriptionID>/resourceGroups/&lt;ResourceGroupName>/providers/Microsoft.Network/virtualNetworks/&lt;VNetName>
   * **虛擬網路子網路**：/subscriptions/&lt;SubscriptionID>/resourceGroups/&lt;ResourceGroupName>/providers/Microsoft.Network/virtualNetworks/&lt;VNetName>/subnets/Subnet1
   * **網域名稱**：contoso.onmicrosoft.com
   * **組織單位辨別名稱**：OU=HDInsightOU,DC=contoso,DC=onmicrosoft,DC=com
   * **叢集使用者群組 DN**：[\"HiveUsers\"]
   * **LDAPS URL**：["ldaps://contoso.onmicrosoft.com:636"]
   * **DomainAdminUserName**: （Enter hello 網域系統管理員使用者名稱）
   * **DomainAdminPassword**: （輸入 hello 網域系統管理員使用者密碼）
   * **我同意 toohello 條款和條件，上述**: （檢查）
   * **Pin toodashboard**: （檢查）
3. 按一下 [購買]。 您將會看到標題為 [進行範本部署] 的新圖格。 大約需要約 20 分鐘 toocreate 叢集。 一旦建立 hello 叢集後，您可以按一下 hello 叢集刀鋒視窗中 hello 入口 tooopen 它。

完成 hello 教學課程之後，您可能想 toodelete hello 叢集。 利用 HDInsight，您的資料會儲存在 Azure 儲存體中，以便您在未使用叢集時安全地進行刪除。 您也需支付 HDInsight 叢集的費用 (即使未使用)。 由於 hello 叢集 hello 費用的次數超過儲存體的 hello 費用，經濟效益 toodelete 叢集時未使用。 刪除叢集的 hello 指示，請參閱[HDInsight 中使用的管理 Hadoop 叢集 hello Azure 入口網站](hdinsight-administer-use-management-portal.md#delete-clusters)。

## <a name="next-steps"></a>後續步驟
* 如需設定 Hive 原則和執行 Hive 查詢，請參閱[針對已加入網域的 HDInisight 叢集設定 Hive 原則](hdinsight-domain-joined-run-hive.md)。
* 使用 SSH tooconnect tooDomain 聯結 HDInsight 叢集，請參閱[搭配使用 SSH 和 Linux、 Unix 或 OS X 的 HDInsight 上的 Linux Hadoop](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined)。

