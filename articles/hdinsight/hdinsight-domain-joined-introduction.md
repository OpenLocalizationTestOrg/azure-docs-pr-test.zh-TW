---
title: "aaaHadoop 安全性-已加入網域的 HDInsight 叢集-Azure |Microsoft 文件"
description: "了解 ..."
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
ms.date: 10/31/2016
ms.author: saurinsh
ms.openlocfilehash: 5a9469402a61bcba4017e1ff4bd06dfba23ac963
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="an-introduction-toohadoop-security-with-domain-joined-hdinsight-clusters-preview"></a>與已加入網域的 HDInsight 叢集 （預覽） 簡介 tooHadoop 安全性

到目前為止，Azure HDInsight 僅支援單一使用者本機系統管理員。這很適合用於比較小型的應用程式團隊或部門。 為獲得更多的人氣指數 hello 企業磁區，在 hello 根據工作負載需要企業的 Hadoop 等級功能，例如 active directory 型驗證、 多使用者支援和角色型存取控制變得越來越重要。 您可以使用已加入網域的 HDInsight 叢集，來建立 HDInsight 叢集已加入 tooan Active Directory 網域、 設定從 hello 企業可以透過 Azure Active Directory toolog tooHDInsight 叢集上進行驗證的員工的清單項目。 Hello 企業之外的任何人都無法登入或存取 hello HDInsight 叢集。 hello 企業系統管理員可以設定角色型存取控制的 Hive 安全性使用[Apache Ranger](http://hortonworks.com/apache/ranger/)，因此如往常般需要限制存取 toodata tooonly。 最後，hello 系統管理員可以稽核 hello 員工的資料存取，任何執行變更 tooaccess 控制原則，因此可達到較高程度的控管其公司資源。

> [!NOTE]
> hello 這個預覽中所述的新功能是僅適用於以 Linux 為基礎的 HDInsight 叢集的 Hive 工作負載。 hello 的其他工作負載，例如將在未來啟用 HBase、 Spark、 Storm 和 Kafka，會釋出。

> [!IMPORTANT]
> Oozie 未在已加入網域的 HDInsight 上啟用。

## <a name="benefits"></a>優點
企業安全性包含四大要件 – 周邊安全性、驗證、授權和加密。

![已加入網域的 HDInsight 叢集優點要件](./media/hdinsight-domain-joined-introduction/hdinsight-domain-joined-four-pillars.png)。

### <a name="perimeter-security"></a>周邊安全性
使用虛擬網路和閘道服務可達成 HDInsight 中的周邊安全性。 現在，企業系統管理員可以建立虛擬網路內的 HDInsight 叢集，並且使用網路安全性群組 （輸入或輸出防火牆規則） toorestrict 存取 toohello 虛擬網路。 只有 hello hello 中定義的 IP 位址輸入防火牆規則將會是能 toocommunicate 與 hello HDInsight 叢集，因此能提供周邊安全性。 使用閘道服務可以達成另一層的周邊安全性。 hello 閘道是 hello 服務可做為的第一線，它有任何內送要求 toohello HDInsight 叢集。 它接受 hello 要求，進行驗證並只允許 hello 要求 toopass toohello 其他節點在叢集中，因此能提供周邊安全性 tooother hello 叢集中的名稱和資料節點。

### <a name="authentication"></a>驗證
利用此公開預覽，企業系統管理員可以在[虛擬網路](https://azure.microsoft.com/services/virtual-network/)中佈建已加入網域的 HDInsight 叢集。 hello hello HDInsight 叢集節點將會聯結的 toohello hello 企業所受的網域。 透過使用 [Azure Active Directory Domain Services](../active-directory-domain-services/active-directory-ds-overview.md) 即可達成此目的。 Hello 叢集中的所有 hello 節點都是聯結的 tooa hello 企業管理的網域。 使用這個設定，hello 企業員工可以登入 toohello 叢集節點使用其網域認證。 他們也可以使用其網域認證 tooauthenticate 與色調、 Ambari 檢視、 ODBC、 JDBC、 PowerShell 和 REST Api 與 hello 叢集 toointeract 像其他核准端點。 hello 管理員有完全控制權限制 hello 與 hello 叢集中，透過這些端點互動的使用者數目。

### <a name="authorization"></a>Authorization
後面接著大多數的企業的最佳作法是不是每一位員工具有存取 tooall 企業資源。 同樣地，此版本中，與 hello 系統管理員可以定義 hello 叢集資源的角色型存取控制原則。 Hello 系統管理員可以設定，例如[Apache Ranger](http://hortonworks.com/apache/ranger/) tooset 登錄區的存取控制原則。 這項功能可確保員工將會無法 tooaccess 只需要 toobe 工作成功的資料量。 SSH 存取 toohello 叢集也是限制只有 toohello 系統管理員。

### <a name="auditing"></a>稽核
以及保護的 hello HDInsight 叢集資源從未經授權的使用者，與設定安全性稽核的 hello 資料的所有存取 toohello 叢集資源，和 hello 資料是必要的 tootrack 未經授權或無意的 hello 資源的存取權。 此預覽中，與 hello 系統管理員可以檢視，並報告所有存取 toohello HDInsight 叢集資源和資料。 hello 系統管理員也可以檢視和報表的所有變更完成 Apache Ranger toohello 存取控制原則支援端點。 已加入網域的 HDInsight 叢集會使用 hello 熟悉 Apache Ranger UI toosearch 稽核記錄。 Hello 後端，使用廣[Apache Solr](http://hortonworks.com/apache/solr/)來儲存及搜尋 hello 記錄檔。

### <a name="encryption"></a>加密
保護資料很重要的會議組織的安全性和法規遵循需求，以及來自未經授權的員工限制存取 toodata，它應該也受到保護的加密。 同時 hello HDInsight 叢集，Azure 儲存體 Blob 的資料存放區及 Azure 資料湖存放區支援透明的伺服器端[資料加密](../storage/common/storage-service-encryption.md)靜止。 安全的 HDInsight 叢集會完美地與此伺服器端待用資料加密功能配合運作。

## <a name="next-steps"></a>後續步驟
* 如需設定已加入網域的 HDInsight 叢集，請參閱[設定已加入網域的 HDInisight 叢集](hdinsight-domain-joined-configure.md)。
* 如需管理已加入網域的 HDInsight 叢集，請參閱[管理已加入網域的 HDInisight 叢集](hdinsight-domain-joined-manage.md)。
* 如需設定 Hive 原則和執行 Hive 查詢，請參閱[針對已加入網域的 HDInisight 叢集設定 Hive 原則](hdinsight-domain-joined-run-hive.md)。
* 若要在已加入網域的 HDInsight 叢集上使用 SSH 執行 Hive 查詢，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined)。
