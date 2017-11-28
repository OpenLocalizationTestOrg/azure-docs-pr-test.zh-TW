---
title: "aaaView SAML 傳回由 hello 存取控制服務 (Java)"
description: "了解如何在 Java 應用程式中的 hello 存取控制服務所傳回的 SAML tooview 裝載於 Azure。"
services: active-directory
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 6cd216f9-eb43-46b4-b30d-f194d0ae2d48
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.custom: aaddev
ms.openlocfilehash: b6733bc98b505cfa89a4ce456f368ee15da11427
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooview-saml-returned-by-hello-azure-access-control-service"></a><span data-ttu-id="2edb3-103">Tooview SAML hello Azure 存取控制服務所傳回的方式</span><span class="sxs-lookup"><span data-stu-id="2edb3-103">How tooview SAML returned by hello Azure Access Control Service</span></span>
<span data-ttu-id="2edb3-104">本指南將說明 tooview hello 基礎安全性聲明標記語言 (SAML) 式 hello Azure 存取控制服務 (ACS) 傳回 tooyour 應用程式的方式。</span><span class="sxs-lookup"><span data-stu-id="2edb3-104">This guide will show you how tooview hello underlying Security Assertion Markup Language (SAML) returned tooyour application by hello Azure Access Control Service (ACS).</span></span> <span data-ttu-id="2edb3-105">hello 指南是根據 hello[如何 tooAuthenticate Eclipse 向 Azure 存取控制服務使用的 Web 使用者](active-directory-java-authenticate-users-access-control-eclipse.md)主題，提供顯示 hello SAML 資訊的程式碼。</span><span class="sxs-lookup"><span data-stu-id="2edb3-105">hello guide builds on hello [How tooAuthenticate Web Users with Azure Access Control Service Using Eclipse](active-directory-java-authenticate-users-access-control-eclipse.md) topic, by providing code that displays hello SAML information.</span></span> <span data-ttu-id="2edb3-106">hello 完成應用程式看起來類似 toohello 下列。</span><span class="sxs-lookup"><span data-stu-id="2edb3-106">hello completed application will look similar toohello following.</span></span>

![Example SAML output][saml_output]

<span data-ttu-id="2edb3-108">如需有關 ACS 的詳細資訊，請參閱 hello[後續步驟](#next_steps)> 一節。</span><span class="sxs-lookup"><span data-stu-id="2edb3-108">For more information on ACS, see hello [Next steps](#next_steps) section.</span></span>

> [!NOTE]
> <span data-ttu-id="2edb3-109">hello Azure 存取服務控制篩選是 community technology preview。</span><span class="sxs-lookup"><span data-stu-id="2edb3-109">hello Azure Access Services Control Filter is a community technology preview.</span></span> <span data-ttu-id="2edb3-110">由於是發行前軟體，Microsoft 尚未提供正式支援。</span><span class="sxs-lookup"><span data-stu-id="2edb3-110">As pre-release software, it is not formally supported by Microsoft.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="2edb3-111">必要條件</span><span class="sxs-lookup"><span data-stu-id="2edb3-111">Prerequisites</span></span>
<span data-ttu-id="2edb3-112">完成本指南中的 toocomplete hello 工作 hello 範例：[如何 tooAuthenticate Eclipse 向 Azure 存取控制服務使用的 Web 使用者](active-directory-java-authenticate-users-access-control-eclipse.md)並以其為開始點就本教學課程中的 hello。</span><span class="sxs-lookup"><span data-stu-id="2edb3-112">toocomplete hello tasks in this guide, complete hello sample at [How tooAuthenticate Web Users with Azure Access Control Service Using Eclipse](active-directory-java-authenticate-users-access-control-eclipse.md) and use it as hello starting point for this tutorial.</span></span>

## <a name="add-hello-jspwriter-library-tooyour-build-path-and-deployment-assembly"></a><span data-ttu-id="2edb3-113">新增 hello JspWriter 庫 tooyour 組建路徑和部署組件</span><span class="sxs-lookup"><span data-stu-id="2edb3-113">Add hello JspWriter library tooyour build path and deployment assembly</span></span>
<span data-ttu-id="2edb3-114">加入包含 hello hello 文件庫**javax.servlet.jsp.JspWriter**類別 tooyour 建置的路徑和部署組件。</span><span class="sxs-lookup"><span data-stu-id="2edb3-114">Add hello library that contains hello **javax.servlet.jsp.JspWriter** class tooyour build path and deployment assembly.</span></span> <span data-ttu-id="2edb3-115">如果您使用 Tomcat，hello 程式庫是**jsp api.jar**，位於 hello Apache **lib**資料夾。</span><span class="sxs-lookup"><span data-stu-id="2edb3-115">If you are using Tomcat, hello library is **jsp-api.jar**, which is located in hello Apache **lib** folder.</span></span>

1. <span data-ttu-id="2edb3-116">在 Eclipse 的專案總管 中，以滑鼠右鍵按一下**MyACSHelloWorld**，按一下 **組建路徑**，按一下 **設定組建路徑**，按一下 hello **程式庫**索引標籤，然後再按一下**新增外部 Jar**。</span><span class="sxs-lookup"><span data-stu-id="2edb3-116">In Eclipse's Project Explorer, right-click **MyACSHelloWorld**, click **Build Path**, click **Configure Build Path**, click hello **Libraries** tab, and then click **Add External JARs**.</span></span>
2. <span data-ttu-id="2edb3-117">在 hello **JAR 選取** 對話方塊中，瀏覽 toohello 必要 JAR，並加以選取，然後按一下**開啟**。</span><span class="sxs-lookup"><span data-stu-id="2edb3-117">In hello **JAR Selection** dialog, navigate toohello necessary JAR, select it, and then click **Open**.</span></span>
3. <span data-ttu-id="2edb3-118">以 hello**屬性 MyACSHelloWorld**對話方塊仍開啟時，按一下**部署組件**。</span><span class="sxs-lookup"><span data-stu-id="2edb3-118">With hello **Properties for MyACSHelloWorld** dialog still open, click **Deployment Assembly**.</span></span>
4. <span data-ttu-id="2edb3-119">在 hello **Web 部署組件** 對話方塊中，按一下 **新增**。</span><span class="sxs-lookup"><span data-stu-id="2edb3-119">In hello **Web Deployment Assembly** dialog, click **Add**.</span></span>
5. <span data-ttu-id="2edb3-120">在 hello**新組件指示詞** 對話方塊中，按一下**Java 建置路徑項目**，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="2edb3-120">In hello **New Assembly Directive** dialog, click **Java Build Path Entries** and then click **Next**.</span></span>
6. <span data-ttu-id="2edb3-121">選取 hello 適當的程式庫，然後按一下**完成**。</span><span class="sxs-lookup"><span data-stu-id="2edb3-121">Select hello appropriate library and click **Finish**.</span></span>
7. <span data-ttu-id="2edb3-122">按一下**確定**tooclose hello**屬性 MyACSHelloWorld**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="2edb3-122">Click **OK** tooclose hello **Properties for MyACSHelloWorld** dialog.</span></span>

## <a name="modify-hello-jsp-file-toodisplay-saml"></a><span data-ttu-id="2edb3-123">修改 hello JSP 檔案 toodisplay SAML</span><span class="sxs-lookup"><span data-stu-id="2edb3-123">Modify hello JSP file toodisplay SAML</span></span>
<span data-ttu-id="2edb3-124">修改**index.jsp** toouse hello 下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="2edb3-124">Modify **index.jsp** toouse hello following code.</span></span>

    <%@ page language="java" contentType="text/html; charset=UTF-8"
        pageEncoding="UTF-8"%>
        <%@ page import="javax.xml.parsers.*"
                 import="javax.xml.transform.*"
                 import="org.w3c.dom.*"
                 import="java.io.*"
                 import="javax.xml.transform.stream.*"
                 import="javax.xml.transform.dom.*"
                 import="javax.xml.xpath.*"
                 import="javax.servlet.jsp.JspWriter" %>
    <!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
    <html>
    <head>
    <meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
    <title>Sample ACS Filter</title>
    </head>
    <body>
        <h3>SAML information from sample ACS program</h3>
        <%!
        void displaySAMLInfo(Node node, String parent, JspWriter out)
        {

            try
            {
                String nodeName;
                int nChild, i;

                nodeName = node.getNodeName();
                out.println("<br>");
                out.println("<u>Examining <b>" + parent + nodeName + "</b></u><br>");

                   // Attributes.
                   NamedNodeMap attribsMap = node.getAttributes();
                   if (null != attribsMap)
                   {
                         for (i=0; i < attribsMap.getLength(); i++)
                         {
                                Node attrib = attribsMap.item(i);
                                out.println("Attribute: <b>" + attrib.getNodeName() + "</b>: " + attrib.getNodeValue()  + "<br>");
                         }
                   }

                   // Child nodes.
                   NodeList list = node.getChildNodes();
                   if (null != list)
                    {
                          nChild = list.getLength();
                          if (nChild > 0)
                          {                    

                                 // If it is a text node, just print hello text.
                                 if (list.item(0).getNodeName() == "#text")
                                 {
                                     out.println("Text value: <b>" + list.item(0).getTextContent() + "</b><br>");
                                 }
                                 else
                                 {
                                     // Print out hello child node names.
                                     out.print("Contains " + nChild + " child node(s): ");   
                                        for (i=0; i < nChild; i++)
                                     {
                                        Node temp = list.item(i);

                                        out.print("<b>" + temp.getNodeName() + "</b>");
                                        if (i < nChild - 1)
                                        {
                                            // Separate hello names.
                                            out.print(", ");
                                        }
                                        else
                                        {
                                            // Finish hello sentence.
                                            out.print(".");
                                        }

                                     }
                                     out.println("<br>");

                                     // Process hello child nodes.
                                     for (i=0; i < nChild; i++)
                                     {
                                        Node temp = list.item(i);
                                        displaySAMLInfo(temp, parent + nodeName + "\\", out);
                                     }
                               }
                          }
                      }
                  }
                catch (Exception e)
                {
                    System.out.println("Exception encountered.");
                    e.printStackTrace();            
                }
            }
        %>

        <%
        try
        {
            String data  = (String) request.getAttribute("ACSSAML");

            DocumentBuilder docBuilder;
            Document doc = null;
            DocumentBuilderFactory docBuilderFactory = DocumentBuilderFactory.newInstance();
            docBuilderFactory.setIgnoringElementContentWhitespace(true);
            docBuilder = docBuilderFactory.newDocumentBuilder();
            byte[] xmlDATA = data.getBytes();

            ByteArrayInputStream in = new ByteArrayInputStream(xmlDATA);
            doc = docBuilder.parse(in);
            doc.getDocumentElement().normalize();

            // Iterate hello child nodes of hello doc.
            NodeList list = doc.getChildNodes();

            for (int i=0; i < list.getLength(); i++)
            {
                displaySAMLInfo(list.item(i), "", out);
            }
        }
        catch (Exception e)
        {
            out.println("Exception encountered.");
            e.printStackTrace();
        }

        %>
    </body>
    </html>

## <a name="run-hello-application"></a><span data-ttu-id="2edb3-125">執行 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="2edb3-125">Run hello application</span></span>
1. <span data-ttu-id="2edb3-126">Hello 電腦模擬器中執行您的應用程式或部署 tooAzure，使用記錄在 hello 步驟[如何 tooAuthenticate Eclipse 向 Azure 存取控制服務使用的 Web 使用者](active-directory-java-authenticate-users-access-control-eclipse.md)。</span><span class="sxs-lookup"><span data-stu-id="2edb3-126">Run your application in hello computer emulator or deploy tooAzure, using hello steps documented at [How tooAuthenticate Web Users with Azure Access Control Service Using Eclipse](active-directory-java-authenticate-users-access-control-eclipse.md).</span></span>
2. <span data-ttu-id="2edb3-127">啟動瀏覽器並開啟您的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="2edb3-127">Launch a browser and open your web application.</span></span> <span data-ttu-id="2edb3-128">登入 tooyour 應用程式之後，您會看到 SAML 資訊，包括 hello hello 身分識別提供者所提供的安全性判斷提示。</span><span class="sxs-lookup"><span data-stu-id="2edb3-128">After you log on tooyour application, you'll see SAML information, including hello security assertion provided by hello identity provider.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2edb3-129">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2edb3-129">Next steps</span></span>
<span data-ttu-id="2edb3-130">toofurther 瀏覽 ACS 的功能和 tooexperiment 更趨精密完美的情況，請參閱[Access Control Service 2.0][Access Control Service 2.0]。</span><span class="sxs-lookup"><span data-stu-id="2edb3-130">toofurther explore ACS's functionality and tooexperiment with more sophisticated scenarios, see [Access Control Service 2.0][Access Control Service 2.0].</span></span>

[Prerequisites]: #pre
[Modify hello JSP file toodisplay SAML]: #modify_jsp
[Add hello JspWriter library tooyour build path and deployment assembly]: #add_library
[Run hello application]: #run_application
[Next steps]: #next_steps
[Access Control Service 2.0]: http://go.microsoft.com/fwlink/?LinkID=212360
[How tooAuthenticate Web Users with Azure Access Control Service Using Eclipse]: active-directory-java-authenticate-users-access-control-eclipse
[saml_output]: ./media/active-directory-java-view-saml-returned-by-access-control/SAML_Output.png
