# Automatic Directories?


# Nesscary Infos

- This is a solution to the [QR code component challenge on Frontend Mentor](https://www.frontendmentor.io/challenges/qr-code-component-iux_sIO_H). 
- Live Site URL && Solution URL: [Add live site URL here](https://ZZQ323.github.io/font-end-practice\qr-code-component-main\index.html)

# My process

## Built with

- Semantic HTML5 markup
- CSS custom properties
- Flexbox

## What I learned

1. Basically having an general riew of the unfimilair section -- Flex Layout --- without using `flex:` properties.

```CSS
flex:2  --> flex:2 1 0
flex:auto  --> flex:1 1 auto
flex:none  --> flex:0 0 auto
```

```CSS
body {
    background-color: hsl(212, 45%, 89%);
    display: flex;
    align-items: center;
    justify-content: center;
    height: 100vh;
    row-gap: 10px;
}
```



## Continued development

1. I would like to use grid , and I'm working to finish these again by these.



2. And, I fail to explain that why items in the flex boxes can not set it's float option , when I try to realize a front end pack up function for the "click" event happening on butto --- considerd to be quite helpful for others to help me.


```CSS
/* in CSS */
body {
    background-color: hsl(212, 45%, 89%);
    display: flex;
    align-items: center;
    justify-content: center;
    height: 100vh;
    row-gap: 10px;
}
.downloader {
    /* float: left; */
    position: fixed;
    top: 30px;
    left: 30px;
    width: 130px;
    
    font-family: Outfit;
    font-size: 13px;
}

/* in html */
<body>
    <button class="downloader"> Click to download this file, if u are in need of the source package! </button>
    ....
</body>
```

3. following the 2 , I can not understand what these Js means for I seldomly use the library. --- but I'm keep using it.


```Js
<script>
const downloadBtn = document.querySelector(".downloader");
downloadBtn.addEventListener("click", async () => {
    const zip = new JSZip();
    try {
        // 根目录
        const rootFolder = zip.folder("qr-code-component-main");

        // 1) 添加 index.html
        {
            const url = "./index.html";
            const fileData = await fetchAsArrayBuffer(url);
            rootFolder.file("index.html", fileData);
        }

        // 2) 打包 design 文件夹
        {
            const designFolder = rootFolder.folder("design");
            // 需要打包的文件列表
            const designFiles = ["desktop-design.jpg", "mobile-design.jpg"];
            for (const fileName of designFiles) {
                const url = `./design/${fileName}`;
                const fileData = await fetchAsArrayBuffer(url);
                designFolder.file(fileName, fileData);
            }
        }

        // 3) 打包 images 文件夹
        {
            const imagesFolder = rootFolder.folder("images");
            // 需要打包的文件列表
            const imageFiles = ["favicon-32x32.png", "image-qr-code.png"];
            for (const fileName of imageFiles) {
                const url = `./images/${fileName}`;
                const fileData = await fetchAsArrayBuffer(url);
                imagesFolder.file(fileName, fileData);
            }
        }

        // ... 如果还有其他文件（.gitignore, README-template.md 等），同样的逻辑

        // 4) 生成 ZIP 文件（Blob）
        const content = await zip.generateAsync({ type: "blob" });
        triggerDownload(content, "qr-code-component-main.zip");

    } catch (err) {
        console.error("打包出错：", err);
    }
});

/**
 * 使用 fetch 获取文件内容并返回 ArrayBuffer
 */
async function fetchAsArrayBuffer(url) {
    const response = await fetch(url);
    if (!response.ok) {
        throw new Error(`Fetch ${url} failed with status ${response.status}`);
    }
    return await response.arrayBuffer();
}

/**
 * 将 Blob 触发为下载
 */
function triggerDownload(blob, filename) {
    const url = URL.createObjectURL(blob);
    const a = document.createElement("a");
    a.href = url;
    a.download = filename;
    a.click();
    // 释放对象URL
    URL.revokeObjectURL(url);
}
</script>
```

## Useful resources



## Acknowledgments || Reference


## Author??
Perhasp not ... it's not ready yet.
