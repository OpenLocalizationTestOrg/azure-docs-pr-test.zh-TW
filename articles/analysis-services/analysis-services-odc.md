---
title: "建立 .odc 檔案以連線至 Azure Analysis Services 伺服器 | Microsoft Docs"
description: "了解如何建立 Office 資料連線檔案 ，以在 Azure 連線至 Analysis Services 伺服器並從該伺服器中取得資料。"
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/23/2017
ms.author: owend
ms.openlocfilehash: 530f3b5c9e90cb45ffb6e12d0d08a35f8d687471
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="create-an-office-data-connection-file"></a><span data-ttu-id="f6d64-103">建立 Office 資料連線檔案</span><span class="sxs-lookup"><span data-stu-id="f6d64-103">Create an Office Data Connection file</span></span>

<span data-ttu-id="f6d64-104">本文中的資訊說明如何從 Excel 2016 版本號碼 16.0.7369.2117 或更早版本或 Excel 2013，建立 Office 資料連線檔案，以連線至 Azure Analysis Services 伺服器。</span><span class="sxs-lookup"><span data-stu-id="f6d64-104">Information in this article describes how you can create an Office Data Connection file to connect to an Azure Analysis Services server from Excel 2016 version number 16.0.7369.2117 or earlier, or Excel 2013.</span></span> <span data-ttu-id="f6d64-105">還需要有更新的 [MSOLAP.7 提供者](analysis-services-data-providers.md)。</span><span class="sxs-lookup"><span data-stu-id="f6d64-105">An updated [MSOLAP.7 provider](analysis-services-data-providers.md) is also required.</span></span>


1. <span data-ttu-id="f6d64-106">複製下面的範例連線檔案，然後貼到文字編輯器。</span><span class="sxs-lookup"><span data-stu-id="f6d64-106">Copy the sample connection file below and paste into a text editor.</span></span> 

2. <span data-ttu-id="f6d64-107">在 `odc:ConnectionString` 中，變更下列屬性：</span><span class="sxs-lookup"><span data-stu-id="f6d64-107">In `odc:ConnectionString`, change the following properties:</span></span>

    *   <span data-ttu-id="f6d64-108">在 `Data Source=asazure://<region>.asazure.windows.net/<servername>;` 中，將 `<region>` 變更為 Analysis Services 伺服器的區域，並將 `<servername>` 變更為您的伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="f6d64-108">In `Data Source=asazure://<region>.asazure.windows.net/<servername>;` change `<region>` to the region of your Analysis Services server and `<servername>` to the name of your  server.</span></span>

    *   <span data-ttu-id="f6d64-109">在 `Initial Catalog=<database>;` 中，將 `<database>` 變更為您的資料庫名稱。</span><span class="sxs-lookup"><span data-stu-id="f6d64-109">In `Initial Catalog=<database>;` change `<database>` to the name of your database.</span></span>

3. <span data-ttu-id="f6d64-110">在 `<odc:CommandText>Model</odc:CommandText>` 中，將 `Model` 變更為您的模型或檢視方塊名稱。</span><span class="sxs-lookup"><span data-stu-id="f6d64-110">In `<odc:CommandText>Model</odc:CommandText>` change `Model` to the name of your model or perspective.</span></span> 

4. <span data-ttu-id="f6d64-111">以 `.odc` 副檔名將檔案儲存到 C:\Users\\*username*\Documents\My Data Sources 資料夾。</span><span class="sxs-lookup"><span data-stu-id="f6d64-111">Save the file with an `.odc` extension to the C:\Users\\*username*\Documents\My Data Sources folder.</span></span>

5. <span data-ttu-id="f6d64-112">在檔案上按一下滑鼠右鍵，然後按一下 [在 Excel 中開啟]。</span><span class="sxs-lookup"><span data-stu-id="f6d64-112">Right-click the file, and then click **Open in Excel**.</span></span> <span data-ttu-id="f6d64-113">或在 Excel 的 [資料] 功能區上，按一下 [現有連線]，選取您的檔案，然後按一下 [開啟]。</span><span class="sxs-lookup"><span data-stu-id="f6d64-113">Or in Excel, on the **Data** ribbon, click **Existing Connections**, select your file, and then click **Open**.</span></span>



<span data-ttu-id="f6d64-114">**範例連線檔案**</span><span class="sxs-lookup"><span data-stu-id="f6d64-114">**Sample connection file**</span></span>
```
<html xmlns:o="urn:schemas-microsoft-com:office:office"
xmlns="http://www.w3.org/TR/REC-html40">

<head>
<meta http-equiv=Content-Type content="text/x-ms-odc; charset=utf-8">
<meta name=ProgId content=ODC.Cube>
<meta name=SourceType content=OLEDB>
<meta name=Catalog content="Database">
<meta name=Table content=Model>
<title>AzureAnalysisServicesConnection</title>
<xml id=docprops><o:DocumentProperties
  xmlns:o="urn:schemas-microsoft-com:office:office"
  xmlns="http://www.w3.org/TR/REC-html40">
  <o:Name>SampleAzureAnalysisServices</o:Name>
 </o:DocumentProperties>
</xml><xml id=msodc><odc:OfficeDataConnection
  xmlns:odc="urn:schemas-microsoft-com:office:odc"
  xmlns="http://www.w3.org/TR/REC-html40">
  <odc:Connection odc:Type="OLEDB">
   <odc:ConnectionString>Provider=MSOLAP.7;Data Source=asazure://<region>.asazure.windows.net/<servername>;Initial Catalog=<database>;</odc:ConnectionString>
   <odc:CommandType>Cube</odc:CommandType>
   <odc:CommandText>Model</odc:CommandText>
  </odc:Connection>
 </odc:OfficeDataConnection>
</xml>
<style>
<!--
    .ODCDataSource
    {
    behavior: url(dataconn.htc);
    }
-->
</style>
 
</head>

<body onload='init()' scroll=no leftmargin=0 topmargin=0 rightmargin=0 style='border: 0px'>
<table style='border: solid 1px threedface; height: 100%; width: 100%' cellpadding=0 cellspacing=0 width='100%'> 
  <tr> 
    <td id=tdName style='font-family:arial; font-size:medium; padding: 3px; background-color: threedface'> 
      &nbsp; 
    </td> 
     <td id=tdTableDropdown style='padding: 3px; background-color: threedface; vertical-align: top; padding-bottom: 3px'>

      &nbsp; 
    </td> 
  </tr> 
  <tr> 
    <td id=tdDesc colspan='2' style='border-bottom: 1px threedshadow solid; font-family: Arial; font-size: 1pt; padding: 2px; background-color: threedface'>

      &nbsp; 
    </td> 
  </tr> 
  <tr> 
    <td colspan='2' style='height: 100%; padding-bottom: 4px; border-top: 1px threedhighlight solid;'> 
      <div id='pt' style='height: 100%' class='ODCDataSource'></div> 
    </td> 
  </tr> 
</table> 

  
<script language='javascript'> 

function init() { 
  var sName, sDescription; 
  var i, j; 
  
  try { 
    sName = unescape(location.href) 
  
    i = sName.lastIndexOf(".") 
    if (i>=0) { sName = sName.substring(1, i); } 
  
    i = sName.lastIndexOf("/") 
    if (i>=0) { sName = sName.substring(i+1, sName.length); } 

    document.title = sName; 
    document.getElementById("tdName").innerText = sName; 

    sDescription = document.getElementById("docprops").innerHTML; 
  
    i = sDescription.indexOf("escription>") 
    if (i>=0) { j = sDescription.indexOf("escription>", i + 11); } 

    if (i>=0 && j >= 0) { 
      j = sDescription.lastIndexOf("</", j); 

      if (j>=0) { 
          sDescription = sDescription.substring(i+11, j); 
        if (sDescription != "") { 
            document.getElementById("tdDesc").style.fontSize="x-small"; 
          document.getElementById("tdDesc").innerHTML = sDescription; 
          } 
        } 
      } 
    } 
  catch(e) { 

    } 
  } 
</script> 

</body> 
 
</html>

```



