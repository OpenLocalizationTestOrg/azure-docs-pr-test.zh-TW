---
title: "已加入網域的 HDInsight 叢集使用 PowerShell-Azure aaaConfigure |Microsoft 文件"
description: "深入了解如何 tooset 安裝及設定使用 Azure PowerShell 的已加入網域的 HDInsight 叢集"
services: hdinsight
documentationcenter: 
author: saurinsh
manager: jhubbard
editor: cgronlun
tags: 
ms.assetid: a13b2f7a-612d-4800-bc92-7fc0524f3e89
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 11/02/2016
ms.author: saurinsh
ms.openlocfilehash: 49da3439513d1e51171f0f7f7f9c3d967d55cb7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-domain-joined-hdinsight-clusters-preview-using-azure-powershell"></a>使用 Azure PowerShell 設定已加入網域的 HDInsight 叢集 (預覽)
了解如何註冊 Azure HDInsight tooset 叢集與 Azure Active Directory (Azure AD) 和[Apache Ranger](http://hortonworks.com/apache/ranger/)使用 Azure PowerShell。 Azure PowerShell 指令碼會提供更快的 toomake hello 組態和較不易有錯誤。 您可以只在 Linux 架構的叢集上設定已加入網域的 HDInsight。 如需詳細資訊，請參閱[已加入網域的 HDInsight 叢集簡介](hdinsight-domain-joined-introduction.md)。

> [!IMPORTANT]
> Oozie 未在已加入網域的 HDInsight 上啟用。

典型的已加入網域的 HDInsight 叢集組態包含下列步驟的 hello:

1. 為您的 Azure AD 建立 Azure 傳統 VNet。  
2. 建立和設定 Azure AD 與 Azure AD DS。
3. 新增 VM toohello 傳統 VNet 來建立組織單位。 
4. 建立 Azure AD DS 的組織單位。
5. 在 hello Azure 資源管理模式中建立 HDInsight VNet。
6. 安裝程式 hello Azure AD DS 的反向 DNS 區域。
7. 對等 hello 兩個 Vnet。
8. 建立 HDInsight 叢集。

hello 所提供的 PowerShell 指令碼會執行步驟 3 到 7。 您必須手動進行步驟 1 和步驟 2。  如果您偏好 toouse Azure PowerShell，請參閱[設定網域的 HDInsight 叢集](hdinsight-domain-joined-configure.md)。 

Hello 最終拓撲的範例如下所示：

![已加入網域的 HDInsight 拓樸](./media/hdinsight-domain-joined-configure/hdinsight-domain-joined-topology.png)

因為 Azure AD 目前只支援傳統虛擬網路 (VNet)，而 Linux 架構的 HDInsight 叢集僅支援 Azure Resource Manager 架構的 VNet，HDInsight Azure AD 整合需要兩個 VNet 以及在兩者之間的對等互連。 Hello hello 兩個部署模型之間的比較資訊，請參閱[Azure Resource Manager vs 傳統部署： 了解部署模型及 hello 資源的狀態](../azure-resource-manager/resource-manager-deployment-model.md)。 兩個 Vnet 必須在 hello hello 與 hello Azure AD DS 相同的區域。

> [!NOTE]
> 本教學課程假設您已沒有 Azure AD。 如果有的話，您可以略過步驟 2 中的 hello 部分。
> 
> 

## <a name="prerequisites"></a>必要條件
您必須遵循本教學課程的項目 toogo hello:

* 您熟悉 [Azure AD 網域服務](https://azure.microsoft.com/services/active-directory-ds/)及其 [價格](https://azure.microsoft.com/pricing/details/active-directory-ds/)結構。
* 確定您的訂用帳戶已列入此公開預覽版本的允許清單中。 您可以傳送電子郵件toohdipreview@microsoft.com與您的訂用帳戶 id。
* SSL 憑證，需由您的網域的簽章授權單位簽署。 hello 憑證所需的設定安全 LDAP。 不可使用自我簽署憑證。
* Azure PowerShell。  請參閱[安裝和設定 Azure PowerShell](/powershell/azure/overview)。

## <a name="create-an-azure-classic-vnet-for-your-azure-ad"></a>為您的 Azure AD 建立 Azure 傳統 VNet。
Hello 指示，請參閱[這裡](hdinsight-domain-joined-configure.md#create-an-azure-virtual-network-classic)。

## <a name="create-and-configure-azure-ad-and-azure-ad-ds"></a>建立和設定 Azure AD 與 Azure AD DS。
Hello 指示，請參閱[這裡](hdinsight-domain-joined-configure.md#create-and-configure-azure-ad-ds-for-your-azure-ad)。

## <a name="run-hello-powershell-script"></a>執行 hello PowerShell 指令碼
您可以從下載 PowerShell 指令碼 hello [GitHub](https://github.com/hdinsight/DomainJoinedHDInsight)。 擷取 hello zip 檔案，並儲存在本機 hello 檔案。

**tooedit hello PowerShell 指令碼**

1. 使用 Windows PowerShell ISE 或任何文字編輯器開啟 run.ps1。
2. 填滿 hello hello 下列變數的值：
   
   * **$SubscriptionName** – hello hello 想 toocreate 您的 HDInsight 叢集的 Azure 訂用帳戶的名稱。 您已在此訂用帳戶，建立傳統的虛擬網路，而且將建立訂用帳戶底下的 hello HDInsight 叢集的 Azure 資源管理員虛擬網路。
   * **$ClassicVNetName** -hello 傳統虛擬網路包含 hello Azure AD DS。 此虛擬網路必須位於 hello 提供上述相同的訂用帳戶。 使用 hello Azure 入口網站，並不使用傳統入口網站，則必須建立此虛擬網路。 如果您依照中的 hello 指令[設定網域的 HDInsight 叢集 （預覽）](hdinsight-domain-joined-configure.md#create-an-azure-virtual-network-classic)，hello 預設名稱是 contosoaadvnet。
   * **$ClassicResourceGroupName** – hello hello 傳統虛擬網路上面所述的資源管理員群組名稱。 例如 contosoaadrg。 
   * **$ArmResourceGroupName** – hello 資源群組名稱中，您想要 toocreate hello HDInsight 叢集。 您可以使用 hello $ArmResourceGroupName 相同資源群組。  如果 hello 資源群組不存在，hello 指令碼會建立 hello 資源群組。
   * **$ArmVNetName** -hello 資源管理員虛擬網路名稱，而您想要在其中 toocreate hello HDInsight 叢集。 此虛擬網路將會置入 $ArmResourceGroupName。  如果 hello VNet 不存在，hello PowerShell 指令碼會建立它。 如果檔案存在，它應該是您提供上述的 hello 資源群組的一部分。
   * **$AddressVnetAddressSpace** – hello 網路 hello 資源管理員虛擬網路位址空間。 請確定此位址空間可供使用。 這個位址空間不得與 hello 傳統虛擬網路的位址空間相重疊。 例如，「10.1.0.0/16」
   * **$ArmVnetSubnetName** -您想要在其中 tooplace hello HDInsight 叢集 Vm 的 hello 資源管理員虛擬網路子網路名稱。 如果 hello 子網路不存在，hello PowerShell 指令碼會建立它。 如果檔案存在，它應該 hello 您提供以上的虛擬網路的一部分。
   * **$AddressSubnetAddressSpace** – hello 網路 hello 資源管理員虛擬網路子網路的位址範圍。 hello HDInsight 叢集 VM 的 IP 位址都將在此子網路位址範圍內。 例如，「10.1.0.0/24」。
   * **$ActiveDirectoryDomainName** – hello Azure AD 網域名稱的 toojoin hello HDInsight 叢集的 Vm。 例如，「contoso.onmicrosoft.com」
   * **$ClusterUsersGroups** – hello 的 hello 安全性群組，以從 AD 想 toosync toohello HDInsight 叢集的一般名稱。 此安全性群組中的 hello 使用者將無法使用其 active directory 網域認證 toohello 叢集儀表板上的無法 toolog。 這些安全性群組必須存在於 hello active directory 中。 例如，「hiveusers」或者「clusteroperatorusers」。
   * **$OrganizationalUnitName** -hello hello 網域內想 tooplace hello HDInsight 叢集 Vm 和 hello hello 叢集所用的服務主體中的組織單位。 hello PowerShell 指令碼會建立這個 OU，如果不存在。 例如，「HDInsightOU」。
3. 儲存 hello 的變更。

**toorun hello 指令碼**

1. 以系統管理員的身分執行 **Windows PowerShell**。
2. 瀏覽 run.ps1 toohello 資料夾。 
3. 輸入 hello 檔案名稱，以執行 hello 指令碼和叫用**ENTER**。  它會跳出 3 個登入對話方塊︰
   
   1. **登入 tooAzure 傳統入口網站**– 輸入您的認證以用 toosign tooAzure 傳統入口網站中的。 您必須建立 hello Azure AD 與 Azure AD DS 使用這些認證。
   2. **登入 tooAzure 資源管理員入口網站**– 輸入您的認證以用 toosign tooAzure 資源管理員入口網站中的。
   3. **網域使用者名稱**– 輸入 hello hello 網域使用者名稱，而您想 toobe hello HDInsight 叢集上的系統管理員認證。 如果您是從頭開始建立 Azure AD，您必須已使用這份文件建立此使用者。 
      
      > [!IMPORTANT]
      > 輸入 hello 使用者名稱格式如下： 
      > 
      > Domainname\username (例如 contoso.onmicrosoft.com\clusteradmin)
      > 
      > 
      
      此使用者必須具有 3 的權限： toojoin 機器 toohello 提供 Active Directory 網域。提供組織單位; toocreate 服務主體和 hello 內的電腦物件與 tooadd 反向 DNS proxy 規則。

建立反向 DNS 區域，hello 指令碼會提示您時 tooenter 網路識別碼。 此網路識別碼必須是 hello 資源管理員虛擬網路的位址首碼。 例如，如果資源管理員虛擬網路子網路位址空間是 10.2.0.0/24，10.2.0.0/24 時輸入 hello 工具會提示您輸入 hello 網路識別碼。 

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
     * **版本**：Hadoop 2.7.3 (HDI 3.5)。 在 HDInsight 叢集版本 3.5 上僅支援已加入網域的 HDInsight。
     * **叢集類型**：進階 PREMIUM
       
       按一下**選取**toosave hello 變更。
   * **認證**： 設定 hello hello 叢集使用者和 hello SSH 使用者的認證。
   * **資料來源**： 建立新的儲存體帳戶，或使用現有的儲存體帳戶，如 hello hello HDInsight 叢集的預設儲存體帳戶。 hello 位置必須 hello 與 hello 兩個 Vnet 相同。  hello 位置也是 hello 的位置 hello HDInsight 叢集。
   * **定價**： 選取叢集的背景工作角色節點的 hello 數目。
   * **進階組態**： 
     
     * **加入網域與 VNet/子網路**： 
       
       * **網域設定**： 
         
         * **網域名稱**：contoso.onmicrosoft.com
         * **網域使用者名稱**：輸入網域使用者名稱。 這個網域必須擁有下列權限的 hello： 加入機器 toohello 網域，並將它們放在您稍早; 設定 hello 組織單位建立您稍早; 設定 hello 組織單位內的服務主體建立反向 DNS 項目。 此網域的使用者將會變成此網域的 HDInsight 叢集的 hello 系統管理員。
         * **網域密碼**： 輸入 hello 網域使用者密碼。
         * **組織單位**： 輸入 hello hello 您先前設定的 OU 辨別的名稱。 例如︰OU=HDInsightOU,DC=contoso,DC=onmicrosoft,DC=com
         * **LDAPS URL**：ldaps://contoso.onmicrosoft.com:636
         * **存取使用者群組**： 指定 hello 安全性群組的使用者，您的 wan toosync toohello 叢集。 例如，HiveUsers。
           
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
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-domain-joined-hdinsight-cluster.json" target="_blank"><img src="./media/hdinsight-domain-joined-configure-use-powershell/deploy-to-azure.png" alt="Deploy tooAzure"></a>
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
   * **叢集使用者群組辨別名稱**："\"CN=HiveUsers,OU=AADDC Users,DC=<DomainName>,DC=onmicrosoft,DC=com\""
   * **LDAPS URL**：["ldaps://contoso.onmicrosoft.com:636"]
   * **DomainAdminUserName**: （Enter hello 網域系統管理員使用者名稱）
   * **DomainAdminPassword**: （輸入 hello 網域系統管理員使用者密碼）
   * **我同意 toohello 條款和條件，上述**: （檢查）
   * **Pin toodashboard**: （檢查）
3. 按一下 [購買]。 您將會看到標題為 [進行範本部署] 的新圖格。 大約需要約 20 分鐘 toocreate 叢集。 一旦建立 hello 叢集後，您可以按一下 hello 叢集刀鋒視窗中 hello 入口 tooopen 它。

完成 hello 教學課程之後，您可能想 toodelete hello 叢集。 利用 HDInsight，您的資料會儲存在 Azure 儲存體中，以便您在未使用叢集時安全地進行刪除。 您也需支付 HDInsight 叢集的費用 (即使未使用)。 由於 hello 叢集 hello 費用的次數超過儲存體的 hello 費用，經濟效益 toodelete 叢集時未使用。 刪除叢集的 hello 指示，請參閱[HDInsight 中使用的管理 Hadoop 叢集 hello Azure 入口網站](hdinsight-administer-use-management-portal.md#delete-clusters)。

## <a name="next-steps"></a>後續步驟

* 如需設定 Hive 原則和執行 Hive 查詢，請參閱[針對已加入網域的 HDInisight 叢集設定 Hive 原則](hdinsight-domain-joined-run-hive.md)。
* 使用 SSH tooconnect tooDomain 聯結 HDInsight 叢集，請參閱[搭配使用 SSH 和 HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined)。

