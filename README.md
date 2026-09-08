**Windows 用户可下载该仓库的所有文件并以以下方法打开进行阅读，Android 用户请移步 [BH3-Visual-Novels-Package-Android](https://github.com/Escosis/BH3-Visual-Novels-Package-Android) 仓库。二者均可以直接访问 [BH3-Visual-Novels](https://escosis.github.io/BH3-Visual-Novels/) 进行预览。**

### 方法一：在电脑浏览器中打开`htm/html`直接阅读，但需要禁用浏览器的 CORS 策略才可正常使用，否则将由于该策略限制无法访问资源文件。

**禁用方法一：**  
在浏览器地址栏输入 chrome://flags/ 或 edge://flags/，搜索 CORS 找到 Block insecure private network requests. 这个选项，改为 Disabled，重启浏览器。

**禁用方法二：**  
创建一个新目录作为数据目录，在浏览器的某个快捷方式属性栏的目标后添加 --disable-web-security --user-data-dir=`<新数据目录路径>`，使用以此快捷方式打开的浏览器进行阅读。  
例如，浏览器快捷方式的目标原本是：  
"C:\Program Files (x86)\Microsoft\Edge\Application\msedge.exe"  
创建C:\EdgeDevData作为数据目录，将此栏改为：  
"C:\Program Files (x86)\Microsoft\Edge\Application\msedge.exe" --disable-web-security --user-data-dir=C:\EdgeDevData  
（注意双引号后有一个空格）

**禁用方法三：**  
新建一个`bat`文件，内容如下：（应根据情况修改路径）
```batch
@echo off
start "" "C:\Program Files (x86)\Microsoft\Edge\Application\msedge.exe" --disable-web-security --user-data-dir="C:\EdgeDevData" --allow-file-access-from-files "%~1"
```
然后可使用 BatToExeConverter 转为`exe`并设置为`htm/html`的打开方式，之后直接点开即可

### 方法二：启动一个本地服务器，从中访问`htm/html`

## 改动：
1. 重定向所有资源路径至本地，移除网络请求
2. 在 game.js 和 gameDurandal.js 末尾添加代码，使得存档使用 file 协议能利用的 localStorage 存储，并且将成就请求重定向至本地，默认全成就（神州折剑录本来用的就是 localStorage 所以不用改）
3. 修复 gameDurandal.js 一处错误（ tryAudio 误写为 tryAudioPlay ）以及`视觉小说目录/index.htm`中一处警告（width=750px 中 px 是多余的）
4. 神州折剑录文件较混乱，进行微调，设置 achievements 文件夹，其余资源都放在 contentweb 文件夹
