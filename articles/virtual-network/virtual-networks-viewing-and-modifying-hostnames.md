---
title: "aaaViewing 及修改主機名稱 |Microsoft 文件"
description: "Azure 虛擬機器，tooview 及變更主機名稱的 web 和背景工作角色的名稱解析"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
ms.assetid: c668cd8e-4e43-4d05-acc3-db64fa78d828
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/27/2016
ms.author: jdial
ms.openlocfilehash: 17d0dd7911754a94db3f37b924b4687da1c70aca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="viewing-and-modifying-hostnames"></a><span data-ttu-id="37a7d-103">檢視與修改主機名稱</span><span class="sxs-lookup"><span data-stu-id="37a7d-103">Viewing and modifying hostnames</span></span>
<span data-ttu-id="37a7d-104">tooallow 您角色執行個體 toobe 參考依主機名稱，則必須將 hello hello 主機名稱的值為每個角色的 hello 服務組態檔中。</span><span class="sxs-lookup"><span data-stu-id="37a7d-104">tooallow your role instances toobe referenced by host name, you must set hello value for hello host name in hello service configuration file for each role.</span></span> <span data-ttu-id="37a7d-105">您執行此作業，加入所需的 hello 主機名稱 toohello **vmName**屬性 hello**角色**項目。</span><span class="sxs-lookup"><span data-stu-id="37a7d-105">You do that by adding hello desired host name toohello **vmName** attribute of hello **Role** element.</span></span> <span data-ttu-id="37a7d-106">hello 值 hello **vmName**屬性用於做為基底 hello 的每個角色執行個體的主機名稱。</span><span class="sxs-lookup"><span data-stu-id="37a7d-106">hello value of hello **vmName** attribute is used as a base for hello host name of each role instance.</span></span> <span data-ttu-id="37a7d-107">例如，如果**vmName**是*webrole*有三個該角色執行個體，hello hello 執行個體的主機名稱將是*webrole0*， *webrole1*，和*webrole2*。</span><span class="sxs-lookup"><span data-stu-id="37a7d-107">For example, if **vmName** is *webrole* and there are three instances of that role, hello host names of hello instances will be *webrole0*, *webrole1*, and *webrole2*.</span></span> <span data-ttu-id="37a7d-108">因為根據 hello 虛擬機器名稱填入 hello 虛擬機器的主機名稱不需要 toospecify hello 組態檔中，虛擬機器的主機名稱。</span><span class="sxs-lookup"><span data-stu-id="37a7d-108">You do not need toospecify a host name for virtual machines in hello configuration file, because hello host name for a virtual machine is populated based on hello virtual machine name.</span></span> <span data-ttu-id="37a7d-109">如需設定 Microsoft Azure 服務的詳細資訊，請參閱 [Azure 服務組態結構描述 (.cscfg 檔)](https://msdn.microsoft.com/library/azure/ee758710.aspx)</span><span class="sxs-lookup"><span data-stu-id="37a7d-109">For more information about configuring a Microsoft Azure service, see [Azure Service Configuration Schema (.cscfg File)](https://msdn.microsoft.com/library/azure/ee758710.aspx)</span></span>

## <a name="viewing-hostnames"></a><span data-ttu-id="37a7d-110">檢視主機名稱</span><span class="sxs-lookup"><span data-stu-id="37a7d-110">Viewing hostnames</span></span>
<span data-ttu-id="37a7d-111">您可以使用任何下列的 hello 工具，在雲端服務中檢視 hello 的虛擬機器和角色執行個體的主機名稱。</span><span class="sxs-lookup"><span data-stu-id="37a7d-111">You can view hello host names of virtual machines and role instances in a cloud service by using any of hello tools below.</span></span>

### <a name="azure-portal"></a><span data-ttu-id="37a7d-112">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="37a7d-112">Azure Portal</span></span>
<span data-ttu-id="37a7d-113">您可以使用 hello [Azure 入口網站](http://portal.azure.com)tooview hello 的主機名稱的虛擬機器的 hello 概觀刀鋒視窗上的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="37a7d-113">You can use hello [Azure portal](http://portal.azure.com) tooview hello host names for virtual machines on hello overview blade for a virtual machine.</span></span> <span data-ttu-id="37a7d-114">請記住，hello 刀鋒視窗中顯示的值**名稱**和**主機名稱**。</span><span class="sxs-lookup"><span data-stu-id="37a7d-114">Keep in mind that hello blade shows a value for **Name** and **Host Name**.</span></span> <span data-ttu-id="37a7d-115">雖然它們一開始 hello 相同變更 hello 主機名稱不會變更 hello hello 虛擬機器或角色執行個體的名稱。</span><span class="sxs-lookup"><span data-stu-id="37a7d-115">Although they are initially hello same, changing hello host name will not change hello name of hello virtual machine or role instance.</span></span>

<span data-ttu-id="37a7d-116">角色執行個體也可以檢視在 hello Azure 入口網站，但如果您列出雲端服務中的 hello 執行個體時，不會顯示 hello 主機名稱。</span><span class="sxs-lookup"><span data-stu-id="37a7d-116">Role instances can also be viewed in hello Azure portal, but when you list hello instances in a cloud service, hello host name is not displayed.</span></span> <span data-ttu-id="37a7d-117">您會看到每個執行個體名稱，但該名稱不能代表 hello 主機名稱。</span><span class="sxs-lookup"><span data-stu-id="37a7d-117">You will see a name for each instance, but that name does not represent hello host name.</span></span>

### <a name="service-configuration-file"></a><span data-ttu-id="37a7d-118">服務組態檔</span><span class="sxs-lookup"><span data-stu-id="37a7d-118">Service configuration file</span></span>
<span data-ttu-id="37a7d-119">您可以部署之服務的 hello 服務組態檔從 hello**設定**hello Azure 入口網站中的 hello 服務刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="37a7d-119">You can download hello service configuration file for a deployed service from hello **Configure** blade of hello service in hello Azure portal.</span></span> <span data-ttu-id="37a7d-120">然後您可以查看 hello **vmName**屬性 hello**角色名稱**元素 toosee hello 主機名稱。</span><span class="sxs-lookup"><span data-stu-id="37a7d-120">You can then look for hello **vmName** attribute for hello **Role name** element toosee hello host name.</span></span> <span data-ttu-id="37a7d-121">請注意，這個主機名稱用於做為基底 hello 的每個角色執行個體的主機名稱。</span><span class="sxs-lookup"><span data-stu-id="37a7d-121">Keep in mind that this host name is used as a base for hello host name of each role instance.</span></span> <span data-ttu-id="37a7d-122">例如，如果**vmName**是*webrole*有三個該角色執行個體，hello hello 執行個體的主機名稱將是*webrole0*， *webrole1*，和*webrole2*。</span><span class="sxs-lookup"><span data-stu-id="37a7d-122">For example, if **vmName** is *webrole* and there are three instances of that role, hello host names of hello instances will be *webrole0*, *webrole1*, and *webrole2*.</span></span>

### <a name="remote-desktop"></a><span data-ttu-id="37a7d-123">遠端桌面</span><span class="sxs-lookup"><span data-stu-id="37a7d-123">Remote Desktop</span></span>
<span data-ttu-id="37a7d-124">啟用遠端桌面 (Windows)、 Windows PowerShell 遠端執行功能 (Windows) 或 SSH （Linux 和 Windows） 連線 tooyour 虛擬機器或角色執行個體之後，您可以透過各種方式檢視 hello 作用中的遠端桌面連線的主機名稱：</span><span class="sxs-lookup"><span data-stu-id="37a7d-124">After you enable Remote Desktop (Windows), Windows PowerShell remoting (Windows), or SSH (Linux and Windows) connections tooyour virtual machines or role instances, you can view hello host name from an active Remote Desktop connection in various ways:</span></span>

* <span data-ttu-id="37a7d-125">輸入主機名稱在 hello 命令提示字元或 SSH 終端機。</span><span class="sxs-lookup"><span data-stu-id="37a7d-125">Type hostname at hello command prompt or SSH terminal.</span></span>
* <span data-ttu-id="37a7d-126">輸入 ipconfig/所有 hello 命令提示 (僅限 Windows)。</span><span class="sxs-lookup"><span data-stu-id="37a7d-126">Type ipconfig /all at hello command prompt (Windows only).</span></span>
* <span data-ttu-id="37a7d-127">Hello 系統檢視 hello 電腦名稱設定 (僅限 Windows)。</span><span class="sxs-lookup"><span data-stu-id="37a7d-127">View hello computer name in hello system settings (Windows only).</span></span>

### <a name="azure-service-management-rest-api"></a><span data-ttu-id="37a7d-128">Azure 服務管理 REST API</span><span class="sxs-lookup"><span data-stu-id="37a7d-128">Azure Service Management REST API</span></span>
<span data-ttu-id="37a7d-129">從 REST 用戶端，請遵循下列指示：</span><span class="sxs-lookup"><span data-stu-id="37a7d-129">From a REST client, follow these instructions:</span></span>

1. <span data-ttu-id="37a7d-130">確定您擁有用戶端憑證 tooconnect toohello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="37a7d-130">Ensure that you have a client certificate tooconnect toohello Azure portal.</span></span> <span data-ttu-id="37a7d-131">tooobtain 用戶端憑證，請依照下列中的 hello 步驟[How to： 下載和匯入發佈設定及訂用帳戶資訊](https://msdn.microsoft.com/library/dn385850.aspx)。</span><span class="sxs-lookup"><span data-stu-id="37a7d-131">tooobtain a client certificate, follow hello steps presented in [How to: Download and Import Publish Settings and Subscription Information](https://msdn.microsoft.com/library/dn385850.aspx).</span></span> 
2. <span data-ttu-id="37a7d-132">設定名稱為 x-ms-version，值為 2013-11-01 的標頭項目。</span><span class="sxs-lookup"><span data-stu-id="37a7d-132">Set a header entry named x-ms-version with a value of 2013-11-01.</span></span>
3. <span data-ttu-id="37a7d-133">以下列格式的 hello 傳送要求： https://management.core.windows.net/\<subscrition 識別碼\>/services/hostedservices/\<服務名稱\>？ 內嵌詳細資料 = true</span><span class="sxs-lookup"><span data-stu-id="37a7d-133">Send a request in hello following format: https://management.core.windows.net/\<subscrition-id\>/services/hostedservices/\<service-name\>?embed-detail=true</span></span>
4. <span data-ttu-id="37a7d-134">尋找 hello **HostName**每個項目**RoleInstance**項目。</span><span class="sxs-lookup"><span data-stu-id="37a7d-134">Look for hello **HostName** element for each **RoleInstance** element.</span></span>

> [!WARNING]
> <span data-ttu-id="37a7d-135">您也可以檢視雲端服務從 hello REST 呼叫回應 hello 內部網域尾碼，藉由檢查 hello **InternalDnsSuffix**項目，或藉由執行 ipconfig/全部從命令提示字元中的遠端桌面工作階段 (Windows)或從 SSH 終端機 (Linux) 執行 cat /etc/resolv.conf。</span><span class="sxs-lookup"><span data-stu-id="37a7d-135">You can also view hello internal domain suffix for your cloud service from hello REST call response by checking hello **InternalDnsSuffix** element, or by running ipconfig /all from a command prompt in a Remote Desktop session (Windows), or by running cat /etc/resolv.conf from an SSH terminal (Linux).</span></span>
> 
> 

## <a name="modifying-a-hostname"></a><span data-ttu-id="37a7d-136">修改主機名稱</span><span class="sxs-lookup"><span data-stu-id="37a7d-136">Modifying a hostname</span></span>
<span data-ttu-id="37a7d-137">上傳已修改的服務組態檔，或從遠端桌面工作階段的 hello 電腦重新命名，您可以修改 hello 任何虛擬機器或角色執行個體的主機名稱。</span><span class="sxs-lookup"><span data-stu-id="37a7d-137">You can modify hello host name for any virtual machine or role instance by uploading a modified service configuration file, or by renaming hello computer from a Remote Desktop session.</span></span>

## <a name="next-steps"></a><span data-ttu-id="37a7d-138">後續步驟</span><span class="sxs-lookup"><span data-stu-id="37a7d-138">Next steps</span></span>
[<span data-ttu-id="37a7d-139">名稱解析 (DNS)</span><span class="sxs-lookup"><span data-stu-id="37a7d-139">Name Resolution (DNS)</span></span>](virtual-networks-name-resolution-for-vms-and-role-instances.md)

[<span data-ttu-id="37a7d-140">Azure 服務組態結構描述 (.cscfg)</span><span class="sxs-lookup"><span data-stu-id="37a7d-140">Azure Service Configuration Schema (.cscfg)</span></span>](https://msdn.microsoft.com/library/windowsazure/ee758710.aspx)

[<span data-ttu-id="37a7d-141">Azure 虛擬網路組態結構描述</span><span class="sxs-lookup"><span data-stu-id="37a7d-141">Azure Virtual Network Configuration Schema</span></span>](http://go.microsoft.com/fwlink/?LinkId=248093)

[<span data-ttu-id="37a7d-142">使用網路組態檔指定 DNS 設定</span><span class="sxs-lookup"><span data-stu-id="37a7d-142">Specify DNS settings using network configuration files</span></span>](virtual-networks-specifying-a-dns-settings-in-a-virtual-network-configuration-file.md)

