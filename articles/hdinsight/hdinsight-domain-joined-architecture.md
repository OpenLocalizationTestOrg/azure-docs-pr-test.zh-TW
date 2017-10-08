---
title: "aaaDomain 加入 Azure HDInsight 架構 |Microsoft 文件"
description: "了解如何 tooplan 已加入網域的 HDInsight。"
services: hdinsight
documentationcenter: 
author: saurinsh
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 7dc6847d-10d4-4b5c-9c83-cc513cf91965
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 02/03/2017
ms.author: saurinsh
ms.openlocfilehash: 1c3ecedf3739b4f8fa54160225be9c1d6e2ca6cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="plan-azure-domain-joined-hadoop-clusters-in-hdinsight"></a>規劃 HDInsight 中已加入網域的 Azure Hadoop 叢集

hello 傳統 Hadoop 是單一使用者叢集。 它適合大部分以小型應用程式團隊建置大型資料工作負載的公司。 隨著 Hadoop 日益普及，許多企業都轉而採用由 IT 團隊管理叢集，且多個應用程式團隊共用叢集的模式。 因此，功能涉及多使用者叢集皆 hello Azure HDInsight 中最要求的功能。

而非建立自己的多位使用者的驗證和授權，HDInsight 依賴 hello 熱門身分識別提供者--Active Directory (AD)。 在 AD 中的 hello 功能強大的安全性功能可以使用的 toomanage HDInsight 中的多使用者授權。 藉由使用 AD 整合 HDInsight，您可以使用與通訊 hello 叢集 AD 認證。 HDInsight AD 使用者 tooa 本機 Hadoop 使用者對應，因此所有 hello HDInsight 上執行的服務 (Ambari 登錄區伺服器，廣，Spark thrift 伺服器和其他人) hello 驗證使用者順暢地運作。

## <a name="integrate-hdinsight-with-ad-and-ad-on-iaas-vm"></a>整合 HDInsight 與 AD 和 IaaS VM 上的 AD

藉由使用 Azure AD 或 Iaas VM 上的 AD 整合 HDInsight，hello HDInsight 叢集節點若為已加入網域的 tooa 網域。 HDInsight 建立服務主體的 hello hello 叢集上執行的 Hadoop 服務，並指定組織單位 (OU) 中放入 Azure AD 或 IaaS VM 上的 AD。 HDInsight 也會建立反向 DNS 對應 hello 的 hello 網域中的 hello 節點 toohello 已加入的網域的 IP 位址。

您可以使用多個架構來達到這種設定。 您可以選擇從 hello 下列架構。

**HDInsight 已與在 Azure IaaS 上執行的 AD 整合**

這是整合 Active Directory HDInsight hello 簡單的架構。 hello AD 網域控制站會在 Azure 中一個 （或多個） 的虛擬機器 (Vm) 上執行。 這些 VM 通常位於虛擬網路中。 您設定 hello HDInsight 叢集的另一個虛擬網路。 HDInsight toohave 的視野 tooActive 目錄，您需要 toopeer 這些虛擬網路使用[對等互連的 VNet 對 VNet](../virtual-network/virtual-network-create-peering.md)。 如果您要建立 hello ARM 中的 Active Directory，則您可以建立 hello Active Directory，並在 HDInsight hello 相同的 VNet，而且您不需要 toodo 對等互連。 

![已加入網域的 HDInsight 叢集拓撲](./media/hdinsight-domain-joined-architecture/hdinsight-domain-joined-architecture_1.png)

> [!NOTE]
> 在這種架構，您無法使用 Azure 資料湖存放區與 hello HDInsight 叢集。


Active Directory 的必要條件︰

* [組織單位](../active-directory-domain-services/active-directory-ds-admin-guide-create-ou.md)必須建立，您將其放在 hello HDInsight 叢集 Vm 和 hello hello 叢集所用的服務主體。
* 必須設定[輕量型目錄存取通訊協定](../active-directory-domain-services/active-directory-ds-admin-guide-configure-secure-ldap.md) (LDAP)，才能與 AD 進行通訊。 向上 LDAPS hello 用憑證 tooset 必須是實際的憑證 （不自我簽署憑證）。
* 反向 DNS 區域必須建立 hello HDInsight 子網路 (例如，在上一張圖片 hello 10.2.0.0/24) hello IP 位址範圍的 hello 網域上。
* 需要服務帳戶或使用者帳戶。 使用此帳戶 toocreate hello HDInsight 叢集。 此帳戶必須具有下列權限的 hello:

    - 權限 toocreate 服務主體物件和 hello 組織單位中的電腦物件
    - 權限 toocreate 反向 DNS proxy 規則
    - 權限 toojoin 機器 toohello Active Directory 網域

**HDInsight 與僅限雲端的 Azure AD 整合**

若為僅限雲端的 Azure AD，請設定網域控制站，讓 HDInsight 可以與 Azure AD 整合。 使用 [Azure Active Directory Domain Services](../active-directory-domain-services/active-directory-ds-overview.md) (Azure AD DS) 即可達成此目的。 Azure AD DS hello 雲端上建立網域控制站機器，並提供其 IP 位址。 它會建立兩個網域控制站，以達到高可用性。

目前，Azure AD DS 只存在於傳統虛擬網路。 如果這不是使用 hello Azure 傳統入口網站會產生錯誤。 hello hello 需要 toobe 的 Azure 入口網站中存在虛擬網路的 HDInsight 所以與 hello 傳統虛擬網路使用對等互連的 VNet 對 VNet。

> [!NOTE]
> 傳統的虛擬網路與虛擬網路，都必須在這兩個虛擬網路中的 Azure 資源管理員之間的對等互連 hello 相同的地區和在 hello 相同 Azure 訂用帳戶。

![已加入網域的 HDInsight 叢集拓撲](./media/hdinsight-domain-joined-architecture/hdinsight-domain-joined-architecture_2.png)

Azure AD 的必要條件：

* [組織單位](../active-directory-domain-services/active-directory-ds-admin-guide-create-ou.md)必須內建立，您將其放 hello HDInsight 叢集 Vm 和 hello hello 叢集所用的服務主體。
* 您必須在設定 Azure AD DS 時設定 [LDAPS](../active-directory-domain-services/active-directory-ds-admin-guide-configure-secure-ldap.md)。 向上 LDAPS hello 用憑證 tooset 必須是實際的憑證 （不自我簽署憑證）。
* 反向 DNS 區域必須建立 hello HDInsight 子網路 (例如，在上一張圖片 hello 10.2.0.0/24) hello IP 位址範圍的 hello 網域上。
* [密碼雜湊](../active-directory-domain-services/active-directory-ds-getting-started-password-sync.md)必須與 Azure AD tooAzure AD DS 同步。
* 需要服務帳戶或使用者帳戶。 使用此帳戶 toocreate hello HDInsight 叢集。 此帳戶必須具有下列權限的 hello:

    - 權限 toocreate 服務主體物件和 hello 組織單位中的電腦物件
    - 權限 toocreate 反向 DNS proxy 規則
    - 權限 toojoin 機器 toohello Azure AD 網域

## <a name="next-steps"></a>後續步驟
* tooconfigure 已加入網域的 HDInsight 叢集，請參閱[設定已加入網域的 HDInsight 叢集](hdinsight-domain-joined-configure.md)。
* toomanage 已加入網域的 HDInsight 叢集，請參閱[管理已加入網域的 HDInsight 叢集](hdinsight-domain-joined-manage.md)。
* tooconfigure Hive 原則和執行的 Hive 查詢，請參閱[設定 hive 控制檔的原則，已加入網域的 HDInsight 叢集的](hdinsight-domain-joined-run-hive.md)。
* 在已加入網域的 HDInsight 叢集上使用 SSH toorun Hive 查詢都看到[搭配使用 SSH 和 HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md)。
