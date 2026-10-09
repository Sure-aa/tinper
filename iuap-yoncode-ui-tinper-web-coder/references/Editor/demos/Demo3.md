---
tags:
  - TinperNextPro
  - Editor组件
---
# Editor 富文本组件

## 设置字体、大小
font_family_formats设置字体；font_size_formats配合content_style配置，设置字体大小

```js
/* eslint-disable comma-dangle */
import React, { useEffect, useRef } from 'react';
import Editor from 'tne-tinpernextpro-fe/Editor';

const example3 = () => {
  const onEditorChange = () => {
    console.log('onEditorChange')
  }
  const editorRef = useRef(null);
  useEffect(() => {
    console.log(editorRef.current.editor)
  }, [])

  return (
    <React.Fragment>
      {/* <YNFLoader providerPackage="tne-tinpernextpro-fe" providerEntry="Editor" */}
      <Editor
        style={{ FontSize: '18px' }}
        ref={editorRef}
        initialValue='仿宋，楷体，方正楷体简体，微软雅黑，宋体，黑体'
        id="demo3"
        scriptLoading={{ async: false }} // 异步加载
        onEditorChange={onEditorChange}
        init={{
          height: 500,
          language: 'zh_CN',
          menubar: false, // 顶部菜单栏
          statusbar: true, // 底部状态栏
          content_style: 'body { font-size:20px; text-indent: 2em; }' /** 字体大小，配合font-size-formats食用可固定字体大小 */,
          font_size_formats: '20px' /** 空格分割的font-size列表 '12px 16px 20px'，只有一个值时配合content_style食用可固定字体大小 */,
          font_family: '方正楷体简体, Microsoft YaHei, 微软雅黑',
          font_family_formats: '微软雅黑=Microsoft YaHei;方正楷体简体=方正楷体简体;宋体=SimSun;黑体=SimHei;仿宋=FangSong;楷体=KaiTi;隶书=LiSu;幼圆=YouYuan;' /** 字体列表，空格分割 */,
          default_link_target: '_blank',
          image_title: true,
          plugins: 'formatpainter wordlimit preview searchreplace autolink directionality visualblocks visualchars fullscreen image imagetools link media template code codesample table charmap pagebreak nonbreaking anchor insertdatetime advlist lists wordcount help emoticons autosave', /** !!! 注意：advlist使用时必须配合lists插件，否则控制台报错后ymc扫描会提jira给领域。 */
          toolbar: 'undo redo | formatpainter removeformat | blocks fontfamily fontsize bold italic underline strikethrough | forecolor backcolor | alignleft aligncenter alignright alignjustify lineheight outdent indent | bullist numlist | link unlink | table image media | hr pagebreak | fullscreen',
          paste_data_images: true,
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
    </React.Fragment>
  )
}

export default example3;
```
