---
title: "多個 HDInsight 叢集的 Azure Data Lake Store 帳戶-Azure aaaUse |Microsoft 文件"
description: "了解如何 toouse 多超過一個 HDInsight 叢集與單一 Data Lake Store 帳戶"
keywords: "hdinsight 儲存體,hdfs,結構化資料,非結構化資料, data lake store"
services: hdinsight,storage
documentationcenter: 
tags: azure-portal
author: nitinme
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/02/2017
ms.author: nitinme
ms.openlocfilehash: 3a125b91fcc1e436270a1bd349f7a2d8f27e06fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-multiple-hdinsight-clusters-with-an-azure-data-lake-store-account"></a>利用一個 Azure Data Lake Store 帳戶使用多個 HDInsight 叢集

從 HDInsight 3.5 版開始，您可以建立 HDInsight 叢集與 Azure Data Lake Store 帳戶作為 hello 預設檔案系統。
Data Lake Store 支援無限制的儲存空間，不僅適合裝載大量資料，也適合裝載多個共用單一 Data Lake Store 帳戶的 HDInsight 叢集。 Instructionson 如何 toocreate 在 HDInsight 叢集為 hello 存放裝置的資料湖存放區，請參閱[建立 HDInsight 叢集與資料湖存放區](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md)。

本文章提供建議 toohello 資料湖存放區管理員來設定單一和共用資料湖存放區帳戶可跨多個**active** HDInsight 叢集。 這些建議適用於的 toohosting 多個安全與不安全的 Hadoop 叢集共用的資料湖存放區帳戶。


## <a name="data-lake-store-file-and-folder-level-acls"></a>Data Lake Store 檔案和資料夾等級 ACL

hello 本文的其餘部分假設您已經有相當的認識，檔案與資料夾層級 Acl 的 Azure 資料湖存放區，在詳細資料中所述在[Azure 資料湖存放區中的存取控制](../data-lake-store/data-lake-store-access-control.md)。

## <a name="data-lake-store-setup-for-multiple-hdinsight-clusters"></a>多個 HDInsight 叢集的 Data Lake Store 設定
讓我們需要兩個層級的資料夾階層 tooexplain hello 建議使用 Data Lake Store 帳戶的多個 HDInsight 叢集。 請考慮具有 hello 資料夾結構的 Data Lake Store 帳戶**/叢集/finance**。 此結構中，所有 hello 金融機構所需的 hello 叢集可以都使用 /clusters/finance hello 存放位置。 在未來，如果另一個組織，說出行銷、 想要使用的 HDInsight 叢集 toocreate hello 相同 Data Lake Store 帳戶，他們無法建立 /clusters/marketing hello。 現在，我們只要使用 **/clusters/finance** 即可。

此資料夾結構 toobe 有效地使用 HDInsight 叢集 tooenable，hello 資料湖存放區系統管理員必須指派適當的權限，hello 資料表中所述。 hello hello 表所示的權限對應 tooAccess Acl，並不會進行預設 Acl。 


|資料夾  |權限  |擁有使用者  |擁有群組  | 具名使用者 | 具名使用者權限 | 具名群組 | 具名群組權限 |
|---------|---------|---------|---------|---------|---------|---------|---------|
|/ | rwxr-x--x  |admin |admin  |服務主體 |--x  |FINGRP   |r-x         |
|/clusters | rwxr-x--x |admin |admin |服務主體 |--x  |FINGRP |r-x         |
|/clusters/finance | rwxr-x--t |admin |FINGRP  |服務主體 |rwx  |-  |-     |

Hello 資料表中

- **系統管理員**是 hello 建立者以及 「 hello Data Lake Store 帳戶系統管理員。
- **服務主體**是 hello Azure Active Directory (AAD) 的服務主體與 hello 帳戶相關聯。
- **FINGRP**是在包含使用者從 hello 金融機構中的 AAD 中建立使用者群組。

如需有關如何 toocreate 的 AAD 應用程式 （也會建立服務主體），請參閱指示[建立 AAD 應用程式](../azure-resource-manager/resource-group-create-service-principal-portal.md#create-an-azure-active-directory-application)。 如需有關如何 toocreate 使用者群組在 AAD 時，請參閱指示[管理 Azure Active Directory 中的群組](../active-directory/active-directory-accessmanagement-manage-groups.md)。

一些重點 tooconsider。

- hello 兩個層級的資料夾結構 (**/叢集/finance/**) 必須建立並佈建具有適當權限的 hello 資料湖存放區管理員**之前**hello 儲存體帳戶用於叢集。 建立叢集時不會自動建立此結構。
- 上述的 hello 範例建議設定 hello 擁有的群組**/叢集/finance**為**FINGRP** ，並且允許**r-x**存取 tooFINGRP toohello 整個資料夾階層從 hello 根目錄開始。 這可確保 FINGRP hello 成員可瀏覽 hello 資料夾結構從根目錄開始。
- 在 hello 情況下如果不同的 AAD 服務主體可以建立叢集下的**/叢集/finance**，hello 自黏位元 (hello 上設定**finance**資料夾) 可確保一項服務所建立的資料夾無法刪除 hello 其他主體。
- HDInsight 叢集建立程序之後 hello 資料夾結構與權限的位置，建立在特定叢集的儲存體 loaction **/叢集/finance/**。 例如，可能是與 hello 名稱 fincluster01 叢集 hello 存放裝置**/clusters/finance/fincluster01**。 hello 擁有權和權限的 HDInsight 叢集所建立的 hello 資料夾表所示 hello 這裡。

    |資料夾  |權限  |擁有使用者  |擁有群組  | 具名使用者 | 具名使用者權限 | 具名群組 | 具名群組權限 |
    |---------|---------|---------|---------|---------|---------|---------|---------|
    |/clusters/finanace/ fincluster01 | rwxr-x---  |服務主體 |FINGRP  |- |-  |-   |-  | 
   


## <a name="recommendations-for-job-input-and-output-data"></a>作業輸入和輸出資料的相關建議

我們建議輸入資料 tooa 工作，並 hello 從作業的輸出儲存在外部的資料夾**/叢集**。 這可確保即使 hello 特定叢集的資料夾刪除的 tooreclaim 一些儲存空間、 hello 工作輸入和輸出仍然可供未來使用。 在這種情況下，請確定用於儲存 hello 工作輸入和輸出的 hello 資料夾階層允許適當的 hello 的存取層級服務主體。

## <a name="limit-on-clusters-sharing-a-single-storage-account"></a>共用單一儲存體帳戶的叢集所受的限制

hello hello 可以共用單一的 Data Lake Store 帳戶的叢集數目上限取決於 hello 這些叢集上執行的工作負載。 共用儲存體帳戶的 hello 叢集上有太多的叢集或非常繁重的工作負載可能會導致 hello 儲存體帳戶入口/出口 tooget 節流。

## <a name="support-for-default-acls"></a>預設 ACL 的支援

當建立服務主體具有名為使用者存取權 （如 hello 如上表所示），我們建議您**不**新增 hello 名為使用者使用預設 ACL。 使用預設 Acl 結果中 hello 分派 770 權限的使用者擁有、 主控群組和其他人的佈建名為使用者存取。 雖然此預設值 770 不會取走擁有使用者 (7) 或擁有群組 (7) 的權限，但會取走其他人 (0) 的所有權限。 這會導致一個特定使用案例，在 hello 中詳細討論的已知問題[的已知問題及因應措施](#known-issues-and-workarounds)> 一節。

## <a name="known-issues-and-workarounds"></a>已知問題和因應措施

此區段會列出使用資料湖存放區，以及其因應措施的 HDInsight 的已知問題的 hello。

### <a name="publicly-visible-localized-yarn-resources"></a>公開可見的當地語系化 YARN 資源

建立新的 Azure 資料湖存放區帳戶時，hello 根目錄的自動佈建與存取 ACL 權限位元組 too770。 hello 根資料夾的擁有使用者建立 hello 帳戶 （hello 資料湖存放區系統管理員） 設定 toohello 使用者並 hello 擁有群組設定 toohello 建立 hello 帳戶 hello 使用者的主要群組。 不會提供存取權給「其他人」。

這些設定稱為 tooaffect 一個特定 HDInsight 使用案例中擷取[YARN 247](https://hwxmonarch.atlassian.net/browse/YARN-247)。 工作提交失敗，錯誤訊息類似 toothis:

    Resource XXXX is not publicly accessible and as such cannot be part of hello public cache.

中所述 hello YARN JIRA 更早版本，連結時當地語系化公用資源，hello 定位器會驗證所有 hello 要求的資源為確實公用藉由檢查其 hello 遠端檔案系統上的權限。 任何不符合該條件的 LocalResource 將會被拒絕進行當地語系化。 hello 檢查權限，包括讀取權限 toohello 檔案的 「 其他人 」。 這種情況下無法運作的方塊外時裝載 Azure Data Lake，在 HDInsight 叢集，因為 Azure 資料湖太拒絕所有存取 「 其他 」 在根資料夾層級。

#### <a name="workaround"></a>因應措施
設定讀取執行權限**其他**透過 hello 階層，例如在 **/** ， **/叢集**和  **/叢集/finance** hello 如上表所示。

## <a name="see-also"></a>另請參閱

* [建立以 Data Lake 存放區當做儲存體的 HDInsight 叢集](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md)


