---
title: "aaaUsing 動態 DNS tooregister 主機名稱"
description: "此頁面詳細說明如何 tooset 註冊您自己的 DNS 伺服器中的動態 DNS tooregister 主機名稱。"
services: dns
documentationcenter: na
author: GarethBradshawMSFT
manager: timlt
editor: 
ms.assetid: c315961a-fa33-45cf-82b9-4551e70d32dd
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/23/2017
ms.author: garbrad
ms.openlocfilehash: 8d4b44265714e6976f26bfb3446e8101aa70996a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-dynamic-dns-tooregister-hostnames-in-your-own-dns-server"></a>在您自己的 DNS 伺服器中使用動態 DNS tooregister 主機名稱
[Azure 會為虛擬機器 (VM) 及角色執行個體提供名稱解析](virtual-networks-name-resolution-for-vms-and-role-instances.md) 。 但是，當您的名稱解析需求超過 Azure 所提供的名稱解析時，您可以提供自己的 DNS 伺服器。 這讓您的 DNS 方案 toosuit hello 電源 tootailor 您自己的特定需求。 例如，您可能需要 tooaccess 內部資源，透過 Active Directory 網域控制站。

當您自訂的 DNS 伺服器裝載為 Azure Vm，您可以轉送主機名稱會查詢 hello 相同 vnet tooAzure tooresolve 主機名稱。 如果您不想 toouse 此路由，您可以在您使用動態 DNS 的 DNS 伺服器中註冊您的 VM 主機名稱。  Azure 沒有 hello 功能 （例如認證） toodirectly 在您的 DNS 伺服器中建立記錄，因此通常不需要使用替代的排列方式。 以下是一些常見案例與替代方案。

## <a name="windows-clients"></a>Windows 用戶端
未加入網域的 Windows 用戶端在開機或在 IP 位址改變時，會嘗試進行不安全的動態 DNS (DDNS) 更新。 hello DNS 名稱是 hello 主機名稱加上 hello 主要 DNS 尾碼。 Azure 將主要 DNS 尾碼 hello 保留為空白，但您可以在透過 hello hello VM，將此[UI](https://technet.microsoft.com/library/cc794784.aspx)或[使用 automation](https://social.technet.microsoft.com/forums/windowsserver/3720415a-6a9a-4bca-aa2a-6df58a1a47d7/change-primary-dns-suffix)。

已加入網域的 Windows 用戶端使用安全的動態 DNS，與 hello 網域控制站登錄其 IP 位址。 hello 網域加入程序 hello 用戶端上設定主要 DNS 尾碼 hello 和建立及維護 hello 信任關係。

## <a name="linux-clients"></a>Linux 用戶端
Linux 用戶端通常不自行註冊以 hello DNS 伺服器啟動時，它們假設 hello DHCP 伺服器運作。 在您的 DNS 伺服器，azure 的 DHCP 伺服器沒有 hello 能力或認證 tooregister 記錄。  您可以使用一個工具，稱為*nsupdate*、 隨附於 hello 繫結封裝、 toosend 動態 DNS 更新。 因為已標準化 hello 動態 DNS 通訊協定，您可以使用*nsupdate*即使當您在不繫結上使用 hello DNS 伺服器。

您可以使用所提供的 hello DHCP 用戶端 toocreate hello 攔截程序，並維護 hello hello DNS 伺服器中的主機名稱項目。 Hello 用戶端會在 hello DHCP 週期中，執行中的 hello 指令碼*/etc/dhcp/dhclient-exit-hooks.d/*。 這可以是供 tooregister hello 新的 IP 位址使用*nsupdate*。 例如：

        #!/bin/sh
        requireddomain=mydomain.local

        # only execute on hello primary nic
        if [ "$interface" != "eth0" ]
        then
            return
        fi

        # when we have a new IP, perform nsupdate
        if [ "$reason" = BOUND ] || [ "$reason" = RENEW ] ||
           [ "$reason" = REBIND ] || [ "$reason" = REBOOT ]
        then
            host=`hostname`
            nsupdatecmds=/var/tmp/nsupdatecmds
              echo "update delete $host.$requireddomain a" > $nsupdatecmds
              echo "update add $host.$requireddomain 3600 a $new_ip_address" >> $nsupdatecmds
              echo "send" >> $nsupdatecmds

              nsupdate $nsupdatecmds
        fi

        
        

您也可以使用 hello *nsupdate*命令 tooperform 安全的動態 DNS 更新。 例如，當您使用繫結 DNS 伺服器時，會 [產生](http://linux.yyz.us/nsupdate/)公開-私密金鑰組。  hello DNS 伺服器是[設定](http://linux.yyz.us/dns/ddns-server.html)與 hello 的 hello 金鑰，使它可以驗證 hello hello 要求簽章的公開部分。 您必須使用 hello *-k*選項 tooprovide hello 金鑰組太*nsupdate*順序 hello 動態 DNS 更新要求 toobe 簽署。

當您使用 Windows DNS 伺服器時，您可以使用 Kerberos 驗證以 hello *-g*中的參數*nsupdate* (hello Windows 版本中無法使用*nsupdate*). toodo 此，請使用*kinit* tooload hello 認證 (例如從[keytab 檔案](http://www.itadmintools.com/2011/07/creating-kerberos-keytab-files.html))。 然後*nsupdate g*拾取 hello 從 hello 快取的認證。

如有需要您可以新增 DNS 搜尋尾碼 tooyour Vm。 hello 中指定 hello DNS 尾碼*/etc/resolv.conf*檔案。 多數 Linux 散發版本會自動管理 hello 內容的這個檔案，因此通常無法編輯。 不過，您可以使用覆寫 hello 尾碼 hello DHCP 用戶端的*取代*命令。 toodo 這樣，請在*/etc/dhcp/dhclient.conf*，加入：

        supersede domain-name <required-dns-suffix>;

