---
tags:
  - TinperNextPro
  - Editor组件
---
# Editor 富文本组件

## 粘贴带格式Excel文件
设置paste_as_text: false，增加paste_preprocess回调处理

```js
/* eslint-disable comma-dangle */
import React from 'react';
import Editor from 'tne-tinpernextpro-fe/Editor';

const example5 = () => {
  // 获取剪切板内容
  const getHTMLFromClipboardContents = async () => {
    navigator.clipboard.read().then(value => console.log(value));
    const clipboardContents = await navigator.clipboard.read();
    for (const item of clipboardContents) {
      if (item.types.includes("text/html")) {
        const blob = await item.getType("text/html");
        const blobText = await blob.text();
        return blobText;
      }
    }
    return null;
  };

  // 判断剪切板内容来源
  const detectContentSource = pastedContent => {
    if (pastedContent.includes("mso-cellspacing") || pastedContent.includes("<table")) {
      return "Excel";
    }
    if (pastedContent.includes("mso-") || pastedContent.includes("MsoNormal")) {
      return "MS Office";
    }
    return null;
  };

  return (
    <React.Fragment>
      <Editor
        id="demo5"
        init={{
          height: 500,
          language: 'zh_CN',
          menubar: false, // 顶部菜单栏
          statusbar: true, // 底部状态栏
          paste_as_text: false, // 如需粘贴带格式word文本，请将此参数设置为false
          paste_preprocess: async function (editor, data) {
            const isMs = detectContentSource(data.content);
            const clipboardContent = await getHTMLFromClipboardContents();
            if (isMs) {
              const editorContent = editor.getContent();
              const tableStart = editorContent.lastIndexOf('<table ');
              const tableEnd = editorContent.lastIndexOf('</table>');
              const prefixContent = editorContent.substring(0, tableStart);
              const suffixContent = editorContent.substring(tableEnd + 8);
              const newContent = prefixContent + clipboardContent + suffixContent;
              editor.setContent(newContent)
            }
          }
        }}
      />
    </React.Fragment>
  )
}

export default example5;
```
