---
tags:
  - TinperNextPro
  - Editor组件
---
# Editor 富文本组件

## 限制输入长度
wordlimit插件配置size。如需对粘贴的文本生效，则paste_as_text应设置为true

```js
/* eslint-disable comma-dangle */
import { Button, Message } from '@tinper/next-ui';
import React, { useEffect, useRef } from 'react';
import Editor from 'tne-tinpernextpro-fe/Editor';

const example2 = () => {
  const editorRef = useRef(null);
  const [copyHtml, setCopyHtml] = React.useState('');
  const [copyText, setCopyText] = React.useState('');

  const onEditorChange = () => {
    console.log('onEditorChange')
  }

  const copy = () => {
    const html = editorRef.current.editor.getContent()
    const text = editorRef.current.editor.getContent({ format: 'text' })
    setCopyHtml('HTML格式: ' + html)
    setCopyText('纯文本格式: ' + text)
  }

  useEffect(() => {
    console.log(editorRef.current.editor)
  }, [])

  return (
    <React.Fragment>
      {/* <YNFLoader providerPackage="tne-tinpernextpro-fe" providerEntry="Editor" */}
      <Editor
        style={{ FontSize: '18px' }}
        ref={editorRef}
        initialValue='我是初始化文本'
        id="demo2"
        scriptLoading={{ async: false }} // 异步加载
        onEditorChange={onEditorChange}
        init={{
          height: 500,
          language: 'zh_CN',
          menubar: false, // 顶部菜单栏
          statusbar: true, // 底部状态栏
          default_link_target: '_blank',
          font_size_formats: '12px 16px 20px 24px 36px',
          image_title: true,
          plugins: 'formatpainter wordlimit preview searchreplace autolink directionality visualblocks visualchars fullscreen image imagetools link media template code codesample table charmap pagebreak nonbreaking anchor insertdatetime advlist lists wordcount help emoticons autosave', /** !!! 注意：advlist使用时必须配合lists插件，否则控制台报错后ymc扫描会提jira给领域。 */
          toolbar: 'undo redo | formatpainter removeformat | blocks fontfamily fontsize bold italic underline strikethrough | forecolor backcolor | alignleft aligncenter alignright alignjustify lineheight outdent indent | bullist numlist | link unlink | table image media | hr pagebreak | fullscreen',
          paste_data_images: true,
          paste_as_text: true, // 做为纯文本粘贴时wordlimit配置才生效
          wordlimit: {
            size: 3, /** 字数限制 */
            /** 非必填字段，用户可自定义字数超出后的处理逻辑，如error提示，删除超出文本等 */
            callback: (editor, txt, num) => {
              console.log('wordlimit', editor, txt, num)
              Message.error(`不能超出${num}个字符！`)
              editor.setContent(txt.slice(0, num))
              // 将光标移动到内容的末尾
              editor.selection.select(editor.getBody(), true);
              editor.selection.collapse(false); // false表示光标在选区的末尾
            }
          },
          images_upload_handler: function (blobInfo, success, failure) {
            // 这个函数主要处理word中的图片，并自动完成上传；
            // ajaxUpload是自己定义的一个函数；在回调中，记得调用success函数，传入上传好的图片地址；
            // blobInfo.blob() 得到图片的file对象；
            // ajaxUpload(blobInfo.blob()).then((data) => {
            //   // 上传成功后，调用success函数传入图片地址
            //   success(data.uploadedImageUrl)
            // })
          },
          imageUpload: {
            maxBanchSize: 33,
            onUpload: async (files) => {
              const uploadList = []
              const readFileAsync = file => new Promise((resolve, reject) => {
                const reader = new FileReader()
                reader.onload = evt => resolve(evt.target.result)
                reader.onerror = evt => reject(evt.target.result + '读取失败')
                reader.readAsDataURL(file)
              })

              for (let i = 0; i < files.length; i++) {
                uploadList.push(await readFileAsync(files[i]))
              }

              console.log('uploadList', uploadList);

              return uploadList
            }
          },
          onMediaUpload: async (files) => {
            // 转成 blob url, 只在浏览器有效, 想长久保存还需要上传到后端获取url
            const uploadList = Array.from(files).map(file => URL.createObjectURL(file))
            console.log('uploadList', uploadList);
            return uploadList
          },
        }}
      />
      <Button type='primary' onClick={copy}>复制富文本内容</Button>
      <div className='copyHtml'>{copyHtml}</div>
      <div className='copyText'>{copyText}</div>
    </React.Fragment>
  )
}

export default example2;
```
