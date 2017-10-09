
hello 所有指定的函式應用程式中的 hello 函式的程式碼位於根資料夾，其中包含主機設定檔和一或多個子資料夾，其中每個包含個別的函式，如 hello 下列範例所示為 hello 程式碼：

```
wwwroot
 | - host.json
 | - mynodefunction
 | | - function.json
 | | - index.js
 | | - node_modules
 | | | - ... packages ...
 | | - package.json
 | - mycsharpfunction
 | | - function.json
 | | - run.csx
```

hello *host.json*檔案包含某些執行階段特定的組態，而且處於 hello 的 hello 函式應用程式的根資料夾中。 如需可用設定的資訊，請參閱[host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) hello WebJobs.Script 儲存機制 wiki 中。

每個函數都有包含一或多個程式碼檔案、 hello function.json 組態以及其他相依性的資料夾。

