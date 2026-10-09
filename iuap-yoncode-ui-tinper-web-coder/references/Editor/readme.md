---
tags:
  - TinperNextPro
  - Editor组件
---

# Editor 富文本组件

<!--Editor-->
## API

- 默认继承[Tinymce](http://tinymce.ax-z.cn/general/localize-your-language.php)
- 特有属性如下：

| 参数             | 说明                                           | 类型                      | 默认值      | 版本 |
| ---------------- | ---------------------------------------------- | ------------------------- | ----------- | ---- |
| onUpload     | 上传图片调用接口（tinymce的init参数中加入imageUpload属性后图片模块会增加上传按钮，imageUpload的类型为json， 有以下属性：imageUpload: { onUpload: async (file) => promise  string - 显示图片的url }）               | -               | -          | 1.0  |


- Init配置项
- 选择器配置
  
| 参数             | 说明                                           | 类型                      | 默认值      | 版本 |
| ---------------- | ---------------------------------------------- | ------------------------- | ----------- | ---- |
| selector     |     CSS选择器语法来确定页面上哪个元素被TinyMCE替换成编辑器           | string               | -          | 1.0  |
| inline     |     内联模式(不使用iframe)           | boolean               | false         | 1.0  |



- 插件配置
  
| 参数             | 说明                                           | 类型                      | 默认值      | 版本 |
| ---------------- | ---------------------------------------------- | ------------------------- | ----------- | ---- |
| plugins     |     指定哪些插件被用在当前编辑器实例中           | string               | -          | 1.0  |


### 常用插件
| 参数             | 说明                                           | 版本 |
| ---------------- | ---------------------------------------------- | ---- |
| advlist     | advlist插件扩展默认的list插件，添加UL（bullist）和OL（numlist）的样式选择功能。该插件激活后可在工具栏添加两个控件bullist和numlist | 1.0  |
| anchor     | 在工具栏添加一个锚点/书签按钮，该按钮还出现在菜单的插入列表中 | 1.0  |
| autolink     | 当用户输入有效的完整URL时，autolink插件会自动创建超链接 | 1.0  |
| autoresize     | 该插件提供自动调整编辑器大小的方法以适应内容 | 1.0  |
| autosave     | 添加了一个“恢复草稿”选项，在工具栏添加一个“恢复草稿”的可选按钮，同时如果用户修改了编辑区内的原始内容，在跳转URL之前，其还会弹出一个提示框，提醒用户修改的内容没有提交 | 1.0  |
| bbcode     | 可以通过使用类似[b]这样的bbcode转换为html的strong标签显示，在用户提交内容时再返回bbcode | 1.0  |
| charmap     | 自动在“插入”菜单中添加“特殊字符...”工具，点击后出现一个包含许多特殊字符的窗口，点击可插入相应的特殊字符 | 1.0  |
| code     | 可在工具栏提供一个按钮，该功能也可通过菜单“工具”中选取 | 1.0  |
| directionality     | 适应不同语言的书写方式，ltr文字方向从左到右，rtl从右到左 | 1.0  |
| emoticons     | 可在内容区插入unicode字符表情 | 1.0  |
| fullpage     | 编辑元数据和文档属性，包含title，keywords，description和文档编码charset | 1.0  |
| fullscreen     | 全屏功能，将编辑器铺满当前浏览器窗口 | 1.0  |
| help     | 提供一个帮助组件，提示快捷键的用法 | 1.0  |
| image     | 提供上传图片功能 | 1.0  |
| imagetools     | 图片编辑工具 | 1.0  |
| insertdatetime     | 插入当前日期时间 | 1.0  |
| link     | 添加超链接 | 1.0  |
| lists     | 提供有序列表和无序列表两个工具栏按钮 | 1.0  |
| media     | 插入音频或视频，使用的是HTML5的audio标签和video标签 | 1.0  |
| nonbreaking     | 插入不间断空格 | 1.0  |
| noneditable     | 将带有 mceNonEditable类的内容设为不可编辑（但可以删掉） | 1.0  |
| pagebreak     | 插入特定的分页符，用于使用CMS系统时将内容拆分为数个页面 | 1.0  |
| paste     | 此插件将过滤/清除从Word粘贴过来的内容 | 1.0  |
| preview     | 在弹出的拟态窗口中预览当前编辑区的内容 | 1.0  |
| print     | 调用当前浏览器的打印设置界面，打印当前编辑区的内容 | 1.0  |
| quickbars     | 提供一个新的UI组件以帮助快速创建内容 | 1.0  |
| save     | 在工具栏添加了一个保存提交按钮，点击它将提交编辑器所在的表单 | 1.0  |
| searchreplace     | 提供一个可在内容区进行查找/替换的功能 | 1.0  |
| tabfocus     | 按tab切入切出TinyMCE | 1.0  |
| table     | 提供了相当强大的表格编辑功能 | 1.0  |
| template     | 实现了自定义内容模板 | 1.0  |
| textpattern     | 实现类似markdown类的文本语法结构 | 1.0  |
| toc     | 该功能类似word的目录功能，即根据内容区的标题标签（通常为h1~h3），在当前光标位置生成可手动更新的目录结构 | 1.0  |
| visualchars     | 显示不可见字符 | 1.0  |
| wordcount     | 该插件提供工具栏按钮和菜单栏选项，同时还在状态栏右下实时展示当前字词个数 | 1.0  |



- 工具栏配置
  
| 参数             | 说明                                           | 类型                      | 默认值      | 版本 |
| ---------------- | ---------------------------------------------- | ------------------------- | ----------- | ---- |
| toolbar     |     使用toolbar来配置工具栏上可用的按钮，多个控件使用空格分隔，使用`\|`来创建分组           | string               | -          | 1.0  |


### 工具栏默认配置
| 参数             | 说明                                           | 版本 |
| ---------------- | ---------------------------------------------- | ---- |
| lineheight     | 行高  | 1.0  |
| newdocument     | 新文档 | 1.0  |
| bold     | 加粗 | 1.0  |
| italic     | 斜体 | 1.0  |
| underline     | 下划线 | 1.0  |
| strikethrough     | 删除线 | 1.0  |
| alignleft     | 左对齐 | 1.0  |
| aligncenter     | 居中对齐 | 1.0  |
| alignright     | 右对齐 | 1.0  |
| alignjustify     | 两端对齐 | 1.0  |
| styleselect     | 格式设置 | 1.0  |
| formatselect     | 段落格式 | 1.0  |
| fontselect     | 字体选择 | 1.0  |
| fontsizeselect     | 字号选择 | 1.0  |
| cut     | 剪切 | 1.0  |
| copy     | 复制 | 1.0  |
| paste     | 粘贴 | 1.0  |
| bullist     | 项目列表UL | 1.0  |
| numlist     | 编号列表OL | 1.0  |
| outdent     | 减少缩进 | 1.0  |
| indent     | 增加缩进 | 1.0  |
| blockquote     | 引用 | 1.0  |
| undo     | 撤销 | 1.0  |
| redo     | 重做/重复 | 1.0  |
| removeformat     | 清除格式 | 1.0  |
| subscript     | 下角标 | 1.0  |
| superscript     | 上角标 | 1.0  |

### API默认值
| 参数             |说明| 默认值                                           |
| ---------------- |---| ---------------------------------------------- |
| highlight_on_focus | focus时高亮编辑器 | false |
| readonly | 只读编辑器 | false |
| block_formats | 格式blocks | 'Paragraph=p; Heading 1=h1; Heading 2=h2; Heading 3=h3; Heading 4=h4; Heading 5=h5; Heading 6=h6;' |
| default_font_stack | 默认字体堆栈 | [ '-apple-system', 'Segoe UI', 'Roboto', 'Helvetica Neue', 'sans-serif' ] |
| font_family_formats     |字体列表| 'Andale Mono=andale mono,times; Arial=arial,helvetica,sans-serif; Arial Black=arial black,avant garde; Book Antiqua=book antiqua,palatino; Comic Sans MS=comic sans ms,sans-serif; Courier New=courier new,courier; Georgia=georgia,palatino; Helvetica=helvetica; Impact=impact,chicago; Symbol=symbol; Tahoma=tahoma,arial,helvetica,sans-serif; Terminal=terminal,monaco; Times New Roman=times new roman,times; Trebuchet MS=trebuchet ms,geneva; Verdana=verdana,geneva; Webdings=webdings; Wingdings=wingdings,zapf dingbats'  |
| font_size_formats     |文字大小列表| '8pt 10pt 12pt 14pt 18pt 24pt 36pt' |
| font_size_input_default_unit     |设置字体大小的默认度量单位| pt |
| line_height_formats     | 行高列表|'1 1.1 1.2 1.3 1.4 1.5 2' |
| width     |宽度| 100% |
| height     |高度| 400或目标元素的大小（如果大于 400 像素） |
| min_height     |最小高度| 100 |
| preview_styles     |菜单[格式]预览样式| 'font-family font-size font-weight font-style text-decoration text-transform color background-color border border-radius outline text-shadow' |
| quickbars_selection_toolbar     |快捷工具栏| 'bold italic \| quicklink h2 h3 blockquote' |
| quickbars_insert_toolbar     |快速插入工具栏| 'quickimage quicktable' |
| quickbars_image_toolbar     |快速图像工具栏| 'alignleft aligncenter alignright' |
| editimage_toolbar     |图像编辑工具栏| 'rotateleft rotateright \| flipv fliph \| editimage imageoptions' |
| link_context_toolbar     |上下文工具栏| false |
| table_toolbar     |表格工具栏| 'tableprops tabledelete \| tableinsertrowbefore tableinsertrowafter tabledeleterow \| tableinsertcolbefore tableinsertcolafter tabledeletecol' |
| resize     | 调整编辑器大小工具| true |
| statusbar     | 显示隐藏状态栏| true |
| elementpath     | 编辑器底部状态栏内的元素路径| true |
| style_formats_merge     | 合并附加到自定义段落样式列表| false |
| style_formats_autohide     | 隐藏当前不可用的样式列表| false |
| toolbar_mode     | 工具栏模式| floating |
| toolbar_location     | 工具栏位置，可实现在底部| auto |
| toolbar_persist     | 内联模式始终显示工具栏| false |
| toolbar_sticky     | 粘性工具栏| false |
| toolbar_sticky_offset     | 工具栏根据工具栏位置粘贴或停靠在距视口顶部或底部的指定偏移处 | 0 |
| inline_boundaries     | 内置样式开关| true |
| inline_boundaries_selector     | 使用内置样式的元素| a[href],code |
| color_map     | 调色盘颜色列表（默认22种） | \[ '#BFEDD2', 'Light Green', '#FBEEB8', 'Light Yellow', '#F8CAC6', 'Light Red', '#ECCAFA', 'Light Purple', '#C2E0F4', 'Light Blue', '#2DC26B', 'Green', '#F1C40F', 'Yellow', '#E03E2D', 'Red', '#B96AD9', 'Purple', '#3598DB', 'Blue', '#169179', 'Dark Turquoise', '#E67E23', 'Orange', '#BA372A', 'Dark Red', '#843FA1', 'Dark Purple', '#236FA1', 'Dark Blue', '#ECF0F1', 'Light Gray', '#CED4D9', 'Medium Gray', '#95A5A6', 'Gray', '#7E8C8D', 'Dark Gray', '#34495E', 'Navy Blue', '#000000', 'Black', '#ffffff', 'White' \] |
| custom_colors     | 调色盘开关| true |
| visual     | 网格线开关| true |
| allow_conditional_comments     | 允许条件注释| false |
| allow_html_in_named_anchor     | 允许name锚点| false |
| allow_unsafe_link_target     | 允许不安全的目标链接| false |
| element_format     | 元素为XHTML/HTML| html |
| entity_encoding     | 实体类型| named |
| fix_list_elements     | 修复列表元素| false |
| forced_root_block     | 强制根节点块元素| p |
| keep_styles     | 保持样式| true |
| remove_trailing_brs     | 删除最尾的br| true |
| pad_empty_with_br     | 使用&nbsp;作为空块元素内的占位符| false |
| schema     | 模式| html5 |
| images_file_types     | 图像文件格式| 'jpeg,jpg,jpe,jfi,jif,jfif,png,gif,bmp,webp' |
| formats.wrapper     | 指定当前格式是块元素| false |
| formats.block_expand     | 操作选择是否应向上扩展到最接近的匹配块元素| false |
| formats.deep     | 在选择范围内深度清除当前样式| false |
| format_empty_lines     | 将内联格式应用于多行选择的空行| false |
| indentation     | 缩进| 40px |
| indent_use_margin     | 默认缩进使用padding，该选项为true时会使用margin| false |
| automatic_uploads     | 插入图片和文件到内容区的方式| true |
| init_content_sync     | 同步初始化| false |
| file_picker_types     | 文件选择器的使用场景| 'file image media' |
| images_reuse_filename     | 使用图片文件实际的文件名，而不是每次随即生成一个新的| false |
| images_upload_credentials     | 上传时是否传递cookie等跨域的凭据| false |
| directionality     | ltr / rtl| ltr |
| language     | 界面语言| en |
| allow_script_urls     | 允许链接和图像url使用js| false |
| convert_urls     | 自动转换URL| true |
| document_base_url     | 设置URL的base目录| 当前目录 |
| remove_script_host     | 删除URL的域名部分| true |
| nowrap     | 不能换行| false |
| typeahead_urls     | 键入网址判断| true |
| ui_mode     | 应随编辑器滚动的所有 UI 元素的位置| combined |
| draggable_modal     | 启用模态对话框的拖动| false |
| newline_behavior     | 按下 Enter 或 Return 键的行为| default |
| object_resizing     | 图像、表格或媒体对象上的调整大小 | true |
| text_patterns     | 启用基本 Markdown 模式 | markdown基本规则 |
| paste_as_text     |  HTML 内容粘贴到编辑器时的处理方式 | false |
| paste_block_drop     |  禁用拖放到编辑器中的内容 | false |
| paste_merge_formats     |  粘贴内容时启用合并格式 | true |
| paste_tab_spaces     |  粘贴纯文本内容时使用多少个空格来表示 HTML 中的制表符 | 4 |
| smart_paste     | URL文本更改为超链接或图像 | true |
| paste_data_images     | 允许粘贴图像 | true |
| paste_remove_styles_if_webkit     | webkit样式默认粘贴过滤器 | true |
| paste_webkit_styles     | 在 WebKit 中粘贴时要保留的样式 | none |
| browser_spellcheck     | 使用浏览器的本机拼写检查 | false |
| table_use_colgroups     | 添加colgroup元素col以指定列宽 | true |
| table_default_attributes | 表的默认属性 | { border: '1' } |
| table_default_styles     | 表格的默认样式 | { 'border-collapse': 'collapse', 'width': '100%' } |
| table_tab_navigation     | 单元格之间的默认制表符功能 | true |
| table_header_type     | 行设置为标题行时dom结构表现 | section |
| table_sizing_mode     | 表格大小调整方法 | auto |
| table_column_resizing     | 用户调整表列大小、插入或删除表列时是否调整表或其他列的大小 | preservetable |
| table_resize_bars     | 拖动两列或行之间的边框来调整表格列和行大小 | true |
| link_default_protocol     | 链接默认协议 | https |

### CSS默认样式
| 参数             |说明| 默认值                                           |
| ---------------- |---| ---------------------------------------------- |
| font-size | 字体大小 | 16px |
| font-weight | 字重 | 400 |
| font-family | 字体 | sans-serif |
| line-height | 行高 | 1.4 |
| color | 字体颜色 | 系统默认，dark模式为#fff |
| overflow-wrap | -- | break-word |
| word-wrap | -- | break-word |
