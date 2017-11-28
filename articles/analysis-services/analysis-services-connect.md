---
title: "aaaConnect tooAzure Analysis Services |Microsoft 文件"
description: "了解 tooconnect tooand 從 Azure 中的 Analysis Services 伺服器所取得的資料。"
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: b37f70a0-9166-4173-932d-935d769539d1
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: 5df94492feb48034f156b72e83e1009683988fc8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooan-azure-analysis-services-server"></a><span data-ttu-id="99cd3-103">Tooan Azure Analysis Services 伺服器連接</span><span class="sxs-lookup"><span data-stu-id="99cd3-103">Connect tooan Azure Analysis Services server</span></span>

<span data-ttu-id="99cd3-104">本文說明連線的 tooa 伺服器使用的資料模型化和管理應用程式，例如 SQL Server Management Studio (SSMS) 或 SQL Server Data Tools (SSDT)。</span><span class="sxs-lookup"><span data-stu-id="99cd3-104">This article describes connecting tooa server by using data modeling and management applications like SQL Server Management Studio (SSMS) or SQL Server Data Tools (SSDT).</span></span> <span data-ttu-id="99cd3-105">或是使用用戶端報表應用程式，例如 Microsoft Excel、Power BI Desktop 或自訂應用程式。</span><span class="sxs-lookup"><span data-stu-id="99cd3-105">Or, with client reporting applications like Microsoft Excel, Power BI Desktop, or custom applications.</span></span> <span data-ttu-id="99cd3-106">連線 tooAzure Analysis Services 會使用 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="99cd3-106">Connections tooAzure Analysis Services use HTTPS.</span></span>

## <a name="client-libraries"></a><span data-ttu-id="99cd3-107">用戶端程式庫</span><span class="sxs-lookup"><span data-stu-id="99cd3-107">Client libraries</span></span>
[<span data-ttu-id="99cd3-108">取得最新用戶端程式庫 hello</span><span class="sxs-lookup"><span data-stu-id="99cd3-108">Get hello latest Client libraries</span></span>](analysis-services-data-providers.md)

<span data-ttu-id="99cd3-109">所有的連線 tooa 伺服器，不論類型為何，都需要更新 AMO、 ADOMD.NET 和 OLEDB 用戶端程式庫 tooconnect tooand 介面與 Analysis Services 伺服器。</span><span class="sxs-lookup"><span data-stu-id="99cd3-109">All connections tooa server, regardless of type, require updated AMO, ADOMD.NET, and OLEDB client libraries tooconnect tooand interface with an Analysis Services server.</span></span> <span data-ttu-id="99cd3-110">SSMS、 SSDT、 Excel 2016 和 Power BI，hello 最新的用戶端程式庫會安裝或更新與每月發行版本。</span><span class="sxs-lookup"><span data-stu-id="99cd3-110">For SSMS, SSDT, Excel 2016, and Power BI, hello latest client libraries are installed or updated with monthly releases.</span></span> <span data-ttu-id="99cd3-111">不過，在某些情況下，可能會應用程式可能沒有 hello 最新版本。</span><span class="sxs-lookup"><span data-stu-id="99cd3-111">However, in some cases, it's possible an application may not have hello latest.</span></span> <span data-ttu-id="99cd3-112">例如，當更新原則延遲時，Office 365 更新上或位於 hello 延後的通道。</span><span class="sxs-lookup"><span data-stu-id="99cd3-112">For example, when policies delay updates, or Office 365 updates are on hello Deferred Channel.</span></span>

## <a name="server-name"></a><span data-ttu-id="99cd3-113">伺服器名稱</span><span class="sxs-lookup"><span data-stu-id="99cd3-113">Server name</span></span>

<span data-ttu-id="99cd3-114">當您在 Azure 中建立 Analysis Services 伺服器時，您可以指定其中 hello 伺服器是 toobe 建立的唯一名稱和 hello 區域。</span><span class="sxs-lookup"><span data-stu-id="99cd3-114">When you create an Analysis Services server in Azure, you specify a unique name and hello region where hello server is toobe created.</span></span> <span data-ttu-id="99cd3-115">指定在連接中的 hello 伺服器名稱，hello 伺服器命名配置時：</span><span class="sxs-lookup"><span data-stu-id="99cd3-115">When specifying hello server name in a connection, hello server naming scheme is:</span></span>

```
<protocol>://<region>/<servername>
```
 <span data-ttu-id="99cd3-116">其中通訊協定是字串**asazure**，區域是 hello hello 伺服器建立所在的 Uri (例如，westus.asazure.windows.net) 並為您 hello 區域內的唯一伺服器 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="99cd3-116">Where protocol is string **asazure**, region is hello Uri where hello server was created (for example, westus.asazure.windows.net) and servername is hello name of your unique server within hello region.</span></span>

### <a name="get-hello-server-name"></a><span data-ttu-id="99cd3-117">取得 hello 伺服器名稱</span><span class="sxs-lookup"><span data-stu-id="99cd3-117">Get hello server name</span></span>
<span data-ttu-id="99cd3-118">在**Azure 入口網站**> 伺服器 >**概觀** > **伺服器名稱**，複製 hello 整部伺服器的名稱。</span><span class="sxs-lookup"><span data-stu-id="99cd3-118">In **Azure portal** > server > **Overview** > **Server name**, copy hello entire server name.</span></span> <span data-ttu-id="99cd3-119">如果您的組織中的其他使用者要太連接 toothis 伺服器，您可以在與其共用此伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="99cd3-119">If other users in your organization are connecting toothis server too, you can share this server name with them.</span></span> <span data-ttu-id="99cd3-120">當指定伺服器名稱，就必須使用 hello 完整路徑。</span><span class="sxs-lookup"><span data-stu-id="99cd3-120">When specifying a server name, hello entire path must be used.</span></span>

![在 Azure 中取得伺服器名稱](./media/analysis-services-deploy/aas-deploy-get-server-name.png)


## <a name="connection-string"></a><span data-ttu-id="99cd3-122">連接字串</span><span class="sxs-lookup"><span data-stu-id="99cd3-122">Connection string</span></span>

<span data-ttu-id="99cd3-123">連接 tooAzure 時使用的 Analysis Services hello 表格式物件模型中，使用下列連接字串格式的 hello:</span><span class="sxs-lookup"><span data-stu-id="99cd3-123">When connecting tooAzure Analysis Services using hello Tabular Object Model, use hello following connection string formats:</span></span>

###### <a name="integrated-azure-active-directory-authentication"></a><span data-ttu-id="99cd3-124">整合型 Azure Active Directory 驗證</span><span class="sxs-lookup"><span data-stu-id="99cd3-124">Integrated Azure Active Directory authentication</span></span>
<span data-ttu-id="99cd3-125">整合式的驗證來收取 hello Azure Active Directory 認證快取，如果有的話。</span><span class="sxs-lookup"><span data-stu-id="99cd3-125">Integrated authentication picks up hello Azure Active Directory credential cache if available.</span></span> <span data-ttu-id="99cd3-126">如果沒有，則顯示 hello Azure 登入視窗。</span><span class="sxs-lookup"><span data-stu-id="99cd3-126">If not, hello Azure login window is shown.</span></span>

```
"Provider=MSOLAP;Data Source=<Azure AS instance name>;"
```


###### <a name="azure-active-directory-authentication-with-username-and-password"></a><span data-ttu-id="99cd3-127">以使用者名稱與密碼進行的 Azure Active Directory 驗證</span><span class="sxs-lookup"><span data-stu-id="99cd3-127">Azure Active Directory authentication with username and password</span></span>

```
"Provider=MSOLAP;Data Source=<Azure AS instance name>;User ID=<user name>;Password=<password>;Persist Security Info=True; Impersonation Level=Impersonate;";
```

###### <a name="windows-authentication-integrated-security"></a><span data-ttu-id="99cd3-128">Windows 驗證 (整合式安全性)</span><span class="sxs-lookup"><span data-stu-id="99cd3-128">Windows authentication (Integrated security)</span></span>
<span data-ttu-id="99cd3-129">使用 hello hello 目前處理序執行的 Windows 帳戶。</span><span class="sxs-lookup"><span data-stu-id="99cd3-129">Use hello Windows account running hello current process.</span></span>

```
"Provider=MSOLAP;Data Source=<Azure AS instance name>; Integrated Security=SSPI;Persist Security Info=True;"
```



## <a name="connect-using-an-odc-file"></a><span data-ttu-id="99cd3-130">使用 .odc 檔案進行連接</span><span class="sxs-lookup"><span data-stu-id="99cd3-130">Connect using an .odc file</span></span>
<span data-ttu-id="99cd3-131">與舊版的 Excel 中，使用者可以連線 tooan Azure Analysis Services 伺服器，使用 Office 資料連線 (.odc) 檔案。</span><span class="sxs-lookup"><span data-stu-id="99cd3-131">With older versions of Excel, users can connect tooan Azure Analysis Services server by using an Office Data Connection (.odc) file.</span></span> <span data-ttu-id="99cd3-132">詳細資訊，請參閱 toolearn[建立 Office 資料連線 (.odc) 檔案](analysis-services-odc.md)。</span><span class="sxs-lookup"><span data-stu-id="99cd3-132">toolearn more, see [Create an Office Data Connection (.odc) file](analysis-services-odc.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="99cd3-133">後續步驟</span><span class="sxs-lookup"><span data-stu-id="99cd3-133">Next steps</span></span>
<span data-ttu-id="99cd3-134">[使用 Excel 進行連接](analysis-services-connect-excel.md)  </span><span class="sxs-lookup"><span data-stu-id="99cd3-134">[Connect with Excel](analysis-services-connect-excel.md)  </span></span>  
<span data-ttu-id="99cd3-135">[使用 Power BI 進行連接](analysis-services-connect-pbi.md) </span><span class="sxs-lookup"><span data-stu-id="99cd3-135">[Connect with Power BI](analysis-services-connect-pbi.md) </span></span>  
[<span data-ttu-id="99cd3-136">管理您的伺服器</span><span class="sxs-lookup"><span data-stu-id="99cd3-136">Manage your server</span></span>](analysis-services-manage.md)   

