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
# <a name="using-dynamic-dns-tooregister-hostnames-in-your-own-dns-server"></a><span data-ttu-id="915b4-103">在您自己的 DNS 伺服器中使用動態 DNS tooregister 主機名稱</span><span class="sxs-lookup"><span data-stu-id="915b4-103">Using Dynamic DNS tooregister hostnames in your own DNS server</span></span>
<span data-ttu-id="915b4-104">[Azure 會為虛擬機器 (VM) 及角色執行個體提供名稱解析](virtual-networks-name-resolution-for-vms-and-role-instances.md) 。</span><span class="sxs-lookup"><span data-stu-id="915b4-104">[Azure provides name resolution](virtual-networks-name-resolution-for-vms-and-role-instances.md) for virtual machines (VMs) and role instances.</span></span> <span data-ttu-id="915b4-105">但是，當您的名稱解析需求超過 Azure 所提供的名稱解析時，您可以提供自己的 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="915b4-105">However, when your name resolution needs go beyond those provided by Azure, you can provide your own DNS servers.</span></span> <span data-ttu-id="915b4-106">這讓您的 DNS 方案 toosuit hello 電源 tootailor 您自己的特定需求。</span><span class="sxs-lookup"><span data-stu-id="915b4-106">This gives you hello power tootailor your DNS solution toosuit your own specific needs.</span></span> <span data-ttu-id="915b4-107">例如，您可能需要 tooaccess 內部資源，透過 Active Directory 網域控制站。</span><span class="sxs-lookup"><span data-stu-id="915b4-107">For example, you may need tooaccess on-premises resources via your Active Directory domain controller.</span></span>

<span data-ttu-id="915b4-108">當您自訂的 DNS 伺服器裝載為 Azure Vm，您可以轉送主機名稱會查詢 hello 相同 vnet tooAzure tooresolve 主機名稱。</span><span class="sxs-lookup"><span data-stu-id="915b4-108">When your custom DNS servers are hosted as Azure VMs you can forward hostname queries for hello same vnet tooAzure tooresolve hostnames.</span></span> <span data-ttu-id="915b4-109">如果您不想 toouse 此路由，您可以在您使用動態 DNS 的 DNS 伺服器中註冊您的 VM 主機名稱。</span><span class="sxs-lookup"><span data-stu-id="915b4-109">If you do not wish toouse this route, you can register your VM hostnames in your DNS server using Dynamic DNS.</span></span>  <span data-ttu-id="915b4-110">Azure 沒有 hello 功能 （例如認證） toodirectly 在您的 DNS 伺服器中建立記錄，因此通常不需要使用替代的排列方式。</span><span class="sxs-lookup"><span data-stu-id="915b4-110">Azure doesn't have hello ability (e.g. credentials) toodirectly create records in your DNS servers, so alternative arrangements are often needed.</span></span> <span data-ttu-id="915b4-111">以下是一些常見案例與替代方案。</span><span class="sxs-lookup"><span data-stu-id="915b4-111">Here are some common scenarios with alternatives.</span></span>

## <a name="windows-clients"></a><span data-ttu-id="915b4-112">Windows 用戶端</span><span class="sxs-lookup"><span data-stu-id="915b4-112">Windows clients</span></span>
<span data-ttu-id="915b4-113">未加入網域的 Windows 用戶端在開機或在 IP 位址改變時，會嘗試進行不安全的動態 DNS (DDNS) 更新。</span><span class="sxs-lookup"><span data-stu-id="915b4-113">Non-domain-joined Windows clients attempt unsecured Dynamic DNS (DDNS) updates when they boot or when their IP address changes.</span></span> <span data-ttu-id="915b4-114">hello DNS 名稱是 hello 主機名稱加上 hello 主要 DNS 尾碼。</span><span class="sxs-lookup"><span data-stu-id="915b4-114">hello DNS name is hello hostname plus hello primary DNS suffix.</span></span> <span data-ttu-id="915b4-115">Azure 將主要 DNS 尾碼 hello 保留為空白，但您可以在透過 hello hello VM，將此[UI](https://technet.microsoft.com/library/cc794784.aspx)或[使用 automation](https://social.technet.microsoft.com/forums/windowsserver/3720415a-6a9a-4bca-aa2a-6df58a1a47d7/change-primary-dns-suffix)。</span><span class="sxs-lookup"><span data-stu-id="915b4-115">Azure leaves hello primary DNS suffix blank, but you can set this in hello VM, via hello [UI](https://technet.microsoft.com/library/cc794784.aspx) or [by using automation](https://social.technet.microsoft.com/forums/windowsserver/3720415a-6a9a-4bca-aa2a-6df58a1a47d7/change-primary-dns-suffix).</span></span>

<span data-ttu-id="915b4-116">已加入網域的 Windows 用戶端使用安全的動態 DNS，與 hello 網域控制站登錄其 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="915b4-116">Domain-joined Windows clients register their IP addresses with hello domain controller by using secure Dynamic DNS.</span></span> <span data-ttu-id="915b4-117">hello 網域加入程序 hello 用戶端上設定主要 DNS 尾碼 hello 和建立及維護 hello 信任關係。</span><span class="sxs-lookup"><span data-stu-id="915b4-117">hello domain-join process sets hello primary DNS suffix on hello client and creates and maintains hello trust relationship.</span></span>

## <a name="linux-clients"></a><span data-ttu-id="915b4-118">Linux 用戶端</span><span class="sxs-lookup"><span data-stu-id="915b4-118">Linux clients</span></span>
<span data-ttu-id="915b4-119">Linux 用戶端通常不自行註冊以 hello DNS 伺服器啟動時，它們假設 hello DHCP 伺服器運作。</span><span class="sxs-lookup"><span data-stu-id="915b4-119">Linux clients generally don't register themselves with hello DNS server on startup, they assume hello DHCP server does it.</span></span> <span data-ttu-id="915b4-120">在您的 DNS 伺服器，azure 的 DHCP 伺服器沒有 hello 能力或認證 tooregister 記錄。</span><span class="sxs-lookup"><span data-stu-id="915b4-120">Azure's DHCP servers do not have hello ability or credentials tooregister records in your DNS server.</span></span>  <span data-ttu-id="915b4-121">您可以使用一個工具，稱為*nsupdate*、 隨附於 hello 繫結封裝、 toosend 動態 DNS 更新。</span><span class="sxs-lookup"><span data-stu-id="915b4-121">You can use a tool called *nsupdate*, which is included in hello Bind package, toosend Dynamic DNS updates.</span></span> <span data-ttu-id="915b4-122">因為已標準化 hello 動態 DNS 通訊協定，您可以使用*nsupdate*即使當您在不繫結上使用 hello DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="915b4-122">Because hello Dynamic DNS protocol is standardized, you can use *nsupdate* even when you're not using Bind on hello DNS server.</span></span>

<span data-ttu-id="915b4-123">您可以使用所提供的 hello DHCP 用戶端 toocreate hello 攔截程序，並維護 hello hello DNS 伺服器中的主機名稱項目。</span><span class="sxs-lookup"><span data-stu-id="915b4-123">You can use hello hooks that are provided by hello DHCP client toocreate and maintain hello hostname entry in hello DNS server.</span></span> <span data-ttu-id="915b4-124">Hello 用戶端會在 hello DHCP 週期中，執行中的 hello 指令碼*/etc/dhcp/dhclient-exit-hooks.d/*。</span><span class="sxs-lookup"><span data-stu-id="915b4-124">During hello DHCP cycle, hello client executes hello scripts in */etc/dhcp/dhclient-exit-hooks.d/*.</span></span> <span data-ttu-id="915b4-125">這可以是供 tooregister hello 新的 IP 位址使用*nsupdate*。</span><span class="sxs-lookup"><span data-stu-id="915b4-125">This can be used tooregister hello new IP address by using *nsupdate*.</span></span> <span data-ttu-id="915b4-126">例如：</span><span class="sxs-lookup"><span data-stu-id="915b4-126">For example:</span></span>

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

        
        

<span data-ttu-id="915b4-127">您也可以使用 hello *nsupdate*命令 tooperform 安全的動態 DNS 更新。</span><span class="sxs-lookup"><span data-stu-id="915b4-127">You can also use hello *nsupdate* command tooperform secure Dynamic DNS updates.</span></span> <span data-ttu-id="915b4-128">例如，當您使用繫結 DNS 伺服器時，會 [產生](http://linux.yyz.us/nsupdate/)公開-私密金鑰組。</span><span class="sxs-lookup"><span data-stu-id="915b4-128">For example, when you're using a Bind DNS server, a public-private key pair is [generated](http://linux.yyz.us/nsupdate/).</span></span>  <span data-ttu-id="915b4-129">hello DNS 伺服器是[設定](http://linux.yyz.us/dns/ddns-server.html)與 hello 的 hello 金鑰，使它可以驗證 hello hello 要求簽章的公開部分。</span><span class="sxs-lookup"><span data-stu-id="915b4-129">hello DNS server is [configured](http://linux.yyz.us/dns/ddns-server.html) with hello public part of hello key so that it can verify hello signature on hello request.</span></span> <span data-ttu-id="915b4-130">您必須使用 hello *-k*選項 tooprovide hello 金鑰組太*nsupdate*順序 hello 動態 DNS 更新要求 toobe 簽署。</span><span class="sxs-lookup"><span data-stu-id="915b4-130">You must use hello *-k* option tooprovide hello key-pair too*nsupdate* in order for hello Dynamic DNS update request toobe signed.</span></span>

<span data-ttu-id="915b4-131">當您使用 Windows DNS 伺服器時，您可以使用 Kerberos 驗證以 hello *-g*中的參數*nsupdate* (hello Windows 版本中無法使用*nsupdate*).</span><span class="sxs-lookup"><span data-stu-id="915b4-131">When you're using a Windows DNS server, you can use Kerberos authentication with hello *-g* parameter in *nsupdate* (not available in hello Windows version of *nsupdate*).</span></span> <span data-ttu-id="915b4-132">toodo 此，請使用*kinit* tooload hello 認證 (例如從[keytab 檔案](http://www.itadmintools.com/2011/07/creating-kerberos-keytab-files.html))。</span><span class="sxs-lookup"><span data-stu-id="915b4-132">toodo this, use *kinit* tooload hello credentials (e.g. from a [keytab file](http://www.itadmintools.com/2011/07/creating-kerberos-keytab-files.html)).</span></span> <span data-ttu-id="915b4-133">然後*nsupdate g*拾取 hello 從 hello 快取的認證。</span><span class="sxs-lookup"><span data-stu-id="915b4-133">Then *nsupdate -g* will pick up hello credentials from hello cache.</span></span>

<span data-ttu-id="915b4-134">如有需要您可以新增 DNS 搜尋尾碼 tooyour Vm。</span><span class="sxs-lookup"><span data-stu-id="915b4-134">If needed, you can add a DNS search suffix tooyour VMs.</span></span> <span data-ttu-id="915b4-135">hello 中指定 hello DNS 尾碼*/etc/resolv.conf*檔案。</span><span class="sxs-lookup"><span data-stu-id="915b4-135">hello DNS suffix is specified in hello */etc/resolv.conf* file.</span></span> <span data-ttu-id="915b4-136">多數 Linux 散發版本會自動管理 hello 內容的這個檔案，因此通常無法編輯。</span><span class="sxs-lookup"><span data-stu-id="915b4-136">Most Linux distros automatically manage hello content of this file, so usually you can't edit it.</span></span> <span data-ttu-id="915b4-137">不過，您可以使用覆寫 hello 尾碼 hello DHCP 用戶端的*取代*命令。</span><span class="sxs-lookup"><span data-stu-id="915b4-137">However, you can override hello suffix by using hello DHCP client's *supersede* command.</span></span> <span data-ttu-id="915b4-138">toodo 這樣，請在*/etc/dhcp/dhclient.conf*，加入：</span><span class="sxs-lookup"><span data-stu-id="915b4-138">toodo this, in */etc/dhcp/dhclient.conf*, add:</span></span>

        supersede domain-name <required-dns-suffix>;

