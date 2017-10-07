---
title: "aaaConnecting 您的安全性產品 toohello Operations Management Suite (OMS) 的安全性和稽核解決方案 |Microsoft 文件"
description: "這份文件可協助您 tooconnect 您的安全性產品 tooOperations 管理套件的安全性和稽核解決方案使用通用的事件格式。"
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: 
ms.assetid: 46eee484-e078-4bad-8c89-c88a3508f6aa
ms.service: operations-management-suite
ms.custom: oms-security
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2017
ms.author: yurid
ms.openlocfilehash: 0f4b372d0379987c4e249628a3c8d52733be65c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connecting-your-security-products-toohello-operations-management-suite-oms-security-and-audit-solution"></a>連接您的安全性產品 toohello Operations Management Suite (OMS) 的安全性和稽核解決方案 
這份文件可協助您連接到 hello OMS 安全性和稽核解決方案的安全性產品。 支援下列來源的 hello:

- 常見事件格式 (CEF) 事件
- Cisco ASA 事件


## <a name="what-is-cef"></a>什麼是 CEF？
一般事件格式 (CEF) 是業界標準格式之上許多安全性廠商 tooallow 事件之間的互通性不同平台所使用的 Syslog 訊息。 OMS 安全性和稽核解決方案支援 OMS 安全性搭配使用 CEF，可讓您 tooconnect 安全性產品擷取資料。 

藉由連接您的資料來源 tooOMS，便能 tootake hello 遵循屬於此平台的功能的優點：

- 搜尋與相互關聯
- 稽核
- 警示
- 威脅情報
- 值得注意的問題

## <a name="collection-of-security-solution-logs"></a>收集安全性解決方案的記錄檔

OMS 安全性支援收集使用 CEF over Syslogs 的記錄檔和 [Cisco ASA](https://blogs.technet.microsoft.com/msoms/2016/08/25/add-your-cisco-asa-logs-to-oms-security/) 記錄檔。 在此範例中，hello 來源 （會產生 hello 記錄檔的電腦） 是執行 syslog ng 精靈的 Linux 電腦且 hello 目標是 OMS 安全性。 您必須遵循 tooperform hello tooprepare hello Linux 電腦的工作：

- Hello OMS Agent for Linux，版本 1.2.0-25 或下載上方。
- 請遵循 hello 區段**快速安裝指南**從[本文](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#steps-to-install-the-oms-agent-for-linux)tooinstall 和上架 hello 代理程式 tooyour 工作區。

一般而言，另一個在 hello 記錄產生的 hello 與不同的電腦上安裝 hello 代理程式。 轉送 hello 記錄 toohello 代理程式電腦通常會需要 hello 下列步驟：

- 設定記錄產品/機器 tooforward hello 必要的事件 toohello syslog 服務精靈 （rsyslog 或 syslog-ng） hello hello 代理程式電腦上。
- 啟用 hello 代理程式機器 tooreceive 訊息從遠端系統上的 hello syslog 服務精靈。

Hello 代理程式在電腦上，hello 事件需要傳送嗨 syslog 服務精靈 toolocal UDP 連接埠 25226 toobe。 hello 代理程式會接聽內送事件，在此連接埠。 hello 下列是寄 hello 本機系統 toohello 代理程式 （您可以修改 hello 組態 toofit 您的本機設定） 的所有事件的範例組態：

1. 開啟 hello 終端機視窗，並移 toohello 目錄*/etc/syslog-ng /* 
2. 建立新的檔案*安全性-設定-omsagent.conf*並加入下列內容的 hello: OMS_facility = local4
    
    filter f_local4_oms { facility(local4); };

    destination security_oms { tcp("127.0.0.1" port(25226)); };

    log { source(src); filter(f_local4_oms); destination(security_oms); };
    
3. 下載 hello 檔案*security_events.conf*然後將放在*/etc/opt/microsoft/omsagent/conf/omsagent.d/* hello OMS 代理程式的電腦中。
4. 輸入 hello 命令下方 toorestart hello syslog 服務精靈：*的 syslog ng 執行：*
    
    ```
    sudo service rsyslog restart
    ```

    若為 rsyslog 執行︰
    
    ```
    /etc/init.d/syslog-ng restart
    ```
5. 輸入 hello 下方 toorestart hello OMS 代理程式的命令：

    *若為 syslog-ng 執行* ︰
    
    ```
    sudo service omsagent restart
    ```

    若為 rsyslog 執行︰
    
    ```
    systemctl restart omsagent
    ```
6. 輸入下方的 hello 命令，然後檢閱 hello 結果 tooconfirm hello OMS 代理程式記錄檔中沒有任何錯誤：

    ``` 
    tail /var/opt/microsoft/omsagent/log/omsagent.log
    ```

## <a name="reviewing-collected-security-events"></a>檢閱收集到的安全性事件

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

Hello 組態完成之後，hello 安全性事件將會啟動 toobe 內嵌 OMS 安全性的。 toovisualize 這些事件中，開啟 hello 記錄搜尋中，輸入 hello 命令*類型 = CommonSecurityLog*在 hello 搜尋欄位，然後按 ENTER 鍵。 hello 下列範例顯示 hello 結果，此命令，請注意，在此情況下 OMS 安全性已內嵌由多個廠商的安全性記錄檔：
   
![OMS 安全性和稽核基準評估](./media/oms-security-connect-products/oms-security-connect-products-fig1.png)

您可以修改此搜尋一個單一的廠商，例如 toovisualize 線上 Cisco 記錄、 型別：*類型 = CommonSecurityLog DeviceVendor = Cisco*。 hello"CommonSecurityLog 」 具有預先定義欄位，針對任何 CEF 標頭包括 hello 基本 extensios，任何其他擴充功能時，無論是 「 自訂延伸模組 >，就會插入到 「 AdditionalExtensions 」 欄位。 您可以使用它從 hello 自訂欄位功能 tooget 專用欄位。 

### <a name="accessing-computers-missing-baseline-assessment"></a>存取遺失基準評估的電腦
OMS 會支援 Windows Server 2008 R2 上總 tooWindows Server 2012 R2 hello 網域成員基準設定檔。 Windows Server 2016 基準尚未定案，將在發佈後盡快新增。 透過 OMS 安全性和稽核基準評估掃描的所有其他作業系統出現在 hello**遺失基準評估電腦**> 一節。

## <a name="see-also"></a>另請參閱
在本文件中，您學到如何 tooconnect 您 CEF 方案 tooOMS。 toolearn 進一步了解 OMS 安全性，請參閱下列文章 hello:

* [Operations Management Suite (OMS) 概觀](operations-management-suite-overview.md)
* [監視及回應 tooSecurity 警示在 Operations Management Suite 安全性和稽核解決方案](oms-security-responding-alerts.md)
* [在 Operations Management Suite 安全性和稽核解決方案內監視資源](oms-security-monitoring-resources.md)

