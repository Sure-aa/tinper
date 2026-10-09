---
tags:
  - TinperNextPro
  - Editor组件
---
# Editor 富文本组件

## 基本富文本使用
继承于tinymce。

```js
/* eslint-disable comma-dangle */
import React, { useEffect, useRef } from 'react';
import Editor from 'tne-tinpernextpro-fe/Editor';

const example1 = () => {
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
        initialValue={`梅里雪山，属于横断山脉—怒山山脉，位于云南省迪庆藏族自治州德钦县境内。地处滇、川、藏三省结合部，横断山脉中段怒江与澜沧江之间。 [6]梅里雪山平均海拔在6000米以上的有十三座山峰，俗称“太子十三峰”。主峰卡瓦格博峰，海拔6740米。 [4]

          梅里雪山属高原性寒温带山地气候， [6]梅里雪山是云南生物多样性最丰富的地区之一，也是中国和世界温带地区生物多样性最丰富的地区之一和中国生物多样性保护17个关键区域之一。 [6]
          梅里雪山景区由五大板块构成：包括位于三江并流云南保护地、被列入世界自然遗产名录的金沙江大湾景区，拍摄梅里雪山全景最佳位置的雾浓顶迎宾台，进梅里雪山或雨崩的重要枢纽的飞来寺观景台，可观神瀑、冰湖的雨崩景区，低纬度热带季风海洋性现代冰川的明永冰川景区。 [5]
          形成演变
          梅里雪山地区，在地质构造上，处于古地槽三江印支褶皱系弧形转弯受急剧挤压而变窄的部位。在中生代侏罗纪以前，属于古地槽印支褶皱系，是构造上的活动区，当时是汪洋的古地中海深海区。印支—燕山运动期间，古特提斯海洋盆闭合，上升成陆地。 [11]
          区域位置
          位置境域
          梅里雪山位于云南省迪庆藏族自治州德钦县境内。地处滇、川、藏三省结合部，横断山脉中段怒江与澜沧江之间，梅里雪山属青藏高原东南缘、澜沧江与怒江之间的滇藏边界的怒山山脉， [6]北连西藏阿冬格尼山，南与碧罗雪山相接。它也是三江并流世界自然遗产腹心地，总面积960平方千米。 [4]区域范围
          梅里雪山有广义和狭义之分。广义的梅里雪山是指坐落在云南省迪庆州德钦县境内的四蟒大雪山，，主峰为海拔6740米的云南省第一峰卡格博峰，范围在北纬28°16’—28°53'，东经98°30’ —98°52'之间，分为梅里雪山（狭义）、太子雪山两段。
          狭义梅里雪山仅指广义梅里雪山的北段，北达西藏芒康县境内，南至太子雪山芒框腊卡峰一带，主峰为海拔5295米的说拉曾归面布。 [11]

          地理环境
          地形地貌
          梅里雪山地处横断山脉的腹地， [6]。雪山相对高差4740米。 [4]
          在地质构造上，梅里雪山处于古地槽三江印支褶皱系弧形转弯受急剧挤压而变窄的部位；在地形地貌上，北段山体宽厚，地形起伏相对不剧烈，没有终年积雪的山峰和发育完全的冰川，但高山流石滩地貌极为发达，而南段山地狭窄，地形剧烈起伏，形成极为发育的高山和冰川地貌。 [1] [6]
          气候特点
          梅里雪山属高原性寒温带山地气候，全年温度较低，干湿季节分明，立体气候较为突出，具有太阳辐射强烈、干湿季分明、气候垂直变化显著的特点。 [6]
          1990—2020年梅里雪山地区多年平均气温为6.02℃，且该区四季及年均气温均呈升温趋势，夏季和年际升温显著，冬季增温幅度最大。 [7]
          1990—2020年梅里雪山地区多年平均降水为798.95毫米，梅里雪山地区年降水减少幅度在空间上表现为“南部大北部小”“西坡大东坡小”的特点；在季节上，降水主要分布在夏季（330.41毫米），春、秋次之（211.84毫米、153.83毫米），冬季最少（82.98毫米）。季风降水是年降水总量的主要贡献者（约占67%）。
          植被类型
          在云南植被区划上，梅里雪山地处青藏高原高寒植被区域，青藏高原东南部山地寒温性针叶林、草甸地带。由于极其特殊的地理环境、复杂的地质地貌、多样的气候类型，构成了梅里雪山风景名胜区植物种类繁多，植被类型多样的特点，按照《云南植被》的分类系统可分为9种植被型、13种植被亚型、32个群系，分别占云南植被型的75.0％、植被亚型的38.2％和群系的18.9％；值得重点保护的类型有针阔混交林、硬叶栎类林、黄杉林、落叶松林、云杉和冷杉林、藏柏林、沙棘林、高山灌丛和高山流石滩疏生植被。 [6]
          冰川
          梅里雪山共有明永，斯农，纽巴和浓松四条大冰川，属世界稀有的低纬、低温（零下5℃）、低海拔（2700米）的现代冰川，其中最长最大的冰川，是明永冰川。
          明永冰川从海拔6740米的梅里雪山往下呈弧形一直铺展到2600米的原始森林地带，绵延11.7千米，平均宽度500米，面积为13平方千米，年融水量2.32亿立方米。 [8]
          山脉关系
          所属山脉
          梅里雪山属于横断山脉—怒山山脉，横断山脉（群）位于中国地势第二级阶梯与第一级阶梯交界处，是中国第一﹑第二阶梯的分界线。为中国四川、云南两省西部和西藏自治区东部一系列南北向平行山脉的总称。山岭海拔多在4000—5000米，岭谷高差一般在1000—2000米以上。平均海拔4000米以上。山高谷深，横断东西间交通，故名横断山。 [10]

          主要山峰
          梅里雪山平均海拔在6000米以上的有十三座山峰，俗称“太子十三峰”。 [4]
          2009年7月，梅里雪山国家公园成立；同年10月，梅里雪山景区正式开园和接收。 [4]
          梅里雪山景区由五大板块构成：包括位于三江并流云南保护地、被列入世界自然遗产名录的金沙江大湾景区，拍摄梅里雪山全景最佳位置的雾浓顶迎宾台，进梅里雪山或雨崩的重要枢纽的飞来寺观景台，可观神瀑、冰湖的雨崩景区，低纬度热带季风海洋性现代冰川的明永冰川景区。 [5]
          月亮湾
          月亮湾别称金沙江大湾、金沙江大拐弯、金沙江第一湾，位于迪庆州德钦县奔子栏镇，是一个美丽的“Ω”字形大拐弯，现建有观景台，站在观景台上放眼四周，非常震撼，所以也被称为“天下奇观”。
          飞来寺
          飞来寺别称吉祥飞来寺，始建于明朝万历42年，因修建时“柱梁飞来自立”而得名，现由子孙殿、关圣殿、海潮殿、两厢、两耳、四配殿组成，是观赏、拍摄日照金山奇观的最佳去处之一。
          雾浓顶
          雾浓顶因地处雾浓顶村而得名，建有迎宾十三塔、观景台等，对面就是雄起壮丽的梅里雪山，也是观赏、拍摄日照金山奇观的最佳去处之一，雾浓顶村有一种独特的婚姻制度“一夫多妻”。
          明永冰川
          明永冰川位于卡瓦格博峰下，是具有数万年历史的天然冰体，绵延数千米，因地处明永村而得名，当地藏族人称其为“明永恰”，是为云南省最大、最长和末端海拔最低的山谷冰川。
          雨崩景区
          雨崩景区是深藏在梅里雪山深处的神秘藏族古村落，以前只能靠徒步或骑马、骑骡子进入，现已开通公路，不过都是盘山公路比较危险，有神瀑、冰湖、神湖等景点，被誉为“世外桃园”“徒步者的天堂”“云南最后一处秘境”。`
        }
        id="demo1"
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
          content_style: 'body { font-size:20px; text-indent: 2em; }' /** 字体大小，配合font-size-formats食用可固定字体大小 */,
          plugins: 'formatpainter wordlimit preview searchreplace autolink directionality visualblocks visualchars fullscreen image imagetools link media template code codesample table charmap pagebreak nonbreaking anchor insertdatetime advlist lists wordcount help emoticons autosave', /** !!! 注意：advlist使用时必须配合lists插件，否则控制台报错后ymc扫描会提jira给领域。 */
          contextmenu: 'copy paste link', // 右键快捷键
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

export default example1;
```
