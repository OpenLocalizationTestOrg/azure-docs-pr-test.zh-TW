### <a name="install-via-composer"></a><span data-ttu-id="cdfc0-101">透過編輯器安裝</span><span class="sxs-lookup"><span data-stu-id="cdfc0-101">Install via Composer</span></span>
1. <span data-ttu-id="cdfc0-102">[安裝 Git][install-git]。</span><span class="sxs-lookup"><span data-stu-id="cdfc0-102">[Install Git][install-git].</span></span> <span data-ttu-id="cdfc0-103">請注意，在 Windows 中，您也必須加入 hello Git 可執行檔 tooyour PATH 環境變數。</span><span class="sxs-lookup"><span data-stu-id="cdfc0-103">Note that on Windows, you must also add hello Git executable tooyour PATH environment variable.</span></span> 
2. <span data-ttu-id="cdfc0-104">建立名為**composer.json**在 hello 您專案的根目錄，並加入下列程式碼 tooit hello:</span><span class="sxs-lookup"><span data-stu-id="cdfc0-104">Create a file named **composer.json** in hello root of your project and add hello following code tooit:</span></span>
   
    ```json
    {
      "require": {
        "microsoft/windowsazure": "^0.4"
      }
    }
    ```
3. <span data-ttu-id="cdfc0-105">將 **[composer.phar][composer-phar]** 下載到專案根目錄中。</span><span class="sxs-lookup"><span data-stu-id="cdfc0-105">Download **[composer.phar][composer-phar]** in your project root.</span></span>
4. <span data-ttu-id="cdfc0-106">開啟命令提示字元並執行下列命令，在專案根目錄中的 hello</span><span class="sxs-lookup"><span data-stu-id="cdfc0-106">Open a command prompt and execute hello following command in your project root</span></span>
   
    ```
    php composer.phar install
    ```

[php-sdk-github]: http://go.microsoft.com/fwlink/?LinkId=252719
[install-git]: http://git-scm.com/book/en/Getting-Started-Installing-Git
[download-SDK-PHP]: ../articles/php-download-sdk.md
[composer-phar]: http://getcomposer.org/composer.phar
