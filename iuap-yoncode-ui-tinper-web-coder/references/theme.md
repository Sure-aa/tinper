---
tags:
  - TinperNext
---
## 主题颜色定制


tinper-next 设计规范和技术上支持灵活的样式定制，以满足业务和品牌上多样化的视觉需求，包括全局和指定组件的视觉定制


以下是所有相关css变量的说明

## 全局css变量

| 变量名称 | 默认值 | 描述  | 影响组件 |
| ---- | --- | --- | ---- |
| --wui-base-bg-color | var(--ynfw-color-bg-global-default, #fff) |  | button,card,carousel,cascader,checkbox,collapse,colorpicker,layout,table,timeline,tree |
| --wui-base-bg-color-disabled | var(--ynfw-color-bg-global-disabled, #f7f7f7) |  | button,cascader,checkbox,menu,slider,tree |
| --wui-base-border-color | var(--ynfw-color-border-default, #d9d9d9) |  | badge,calendar,card,checkbox,colorpicker,datepicker,divider,menu,radio,tag,upload |
| --wui-base-border-color-disabled | var(--ynfw-color-border-disabled, #e4e4e4) |  | cascader,slider,tree |
| --wui-base-clear-icon-color | var(--ynfw-color-icon-input-suffix, #ccc) |  | cascader,datepicker,input,input-number,select,slider,timepicker,transfer |
| --wui-base-clear-icon-color-hover | var(--ynfw-color-icon-input-suffix-hover, #505766) |  | cascader,datepicker,input,input-number,select,slider,timepicker,transfer |
| --wui-base-clear-icon-font-size | var(--ynfw-font-size-icon-input, 16px) |  | cascader,datepicker,input,input-number,slider,timepicker,transfer |
| --wui-base-close-icon-color | var(--ynfw-color-icon-input-suffix, #999) |  | cascader,select,table,tag |
| --wui-base-close-icon-color-hover | var(--ynfw-color-icon-input-suffix-hover, #505766) |  | cascader,select,table,tag,upload |
| --wui-base-input-border-radius | var(--ynfw-border-radius-input, 4px) |  | cascader,datepicker,input-group,input-number,timepicker |
| --wui-base-input-border-radius | var(--ynfw-border-radius-input, 4px) |  | cascader,datepicker,input,input-number,timepicker |
| --wui-base-input-border-style | var(--ynfw-border-style-input, solid) |  | cascader,datepicker,form,input-group,input-number,timepicker |
| --wui-base-input-border-style | var(--ynfw-border-style-input, solid) |  | cascader,datepicker,form,input,input-number,timepicker |
| --wui-base-input-border-width | var(--ynfw-border-width-input, 1px) |  | cascader,datepicker,form,input-group,input-number,timepicker |
| --wui-base-input-border-width | var(--ynfw-border-width-input, 1px) |  | cascader,datepicker,form,input,input-number,timepicker |
| --wui-base-input-caret-color | var(--ynfw-color-cursor, #111) |  | cascader,datepicker,input,input-number,timepicker |
| --wui-base-input-font-size | var(--wui-input-font-size, 12px) |  | cascader,input,input-number |
| --wui-base-input-font-weight | var(--ynfw-font-weight-input, 400) |  | cascader,datepicker,input,input-number |
| --wui-base-input-lg-height |  |  | cascader,datepicker,form,input,input-number,timepicker,treeselect |
| --wui-base-input-md-height | var(--ynfw-size-height-input, 28px) |  | cascader,datepicker,form,input-group,input-number,timepicker |
| --wui-base-input-md-height | var(--ynfw-size-height-input, 28px) |  | cascader,datepicker,form,input,input-number,timepicker |
| --wui-base-input-nm-height | 32px |  | cascader,datepicker,form,input,input-number,timepicker |
| --wui-base-input-sm-height | 26px |  | cascader,datepicker,form,input-group,input-number,timepicker |
| --wui-base-input-sm-height | 26px |  | cascader,datepicker,form,input,input-number,timepicker |
| --wui-base-input-xs-height | 20px |  | cascader,datepicker,form,input,input-number,timepicker |
| --wui-base-item-color-active | var(--ynfw-color-primary, var(--wui-primary-color)) |  | datepicker,timepicker |
| --wui-base-item-color-disabled | var(--ynfw-color-text-option-panel-disabled, var(--wui-base-text-color-disabled)) |  | cascader,menu,tree |
| --wui-base-panel-bg-color | var(--ynfw-color-bg-panel, var(--wui-base-bg-color)) |  | modal,upload |
| --wui-base-text-color | var(--ynfw-color-text-option-panel, #111) |  | button,calendar,card,clipboard,collapse,colorpicker,datepicker,divider,drawer,form,input-number,layout,list,menu,modal,popover,spin,table,tabs,timepicker,typography,upload |
| --wui-base-text-color-disabled | var(--ynfw-color-text-option-panel-disabled, #999) |  | checkbox,menu,radio,select,steps,tabs |
| --wui-base-textarea-line-height | var(--ynfw-font-line-height-input, 20px) |  | cascader,input,input-number |
| --wui-border-radius-option-panel | var(--ynfw-border-radius-option-panel, 4px) |  | cascader,dropdown,select,treeselect |
| --wui-border-width-option-panel | var(--ynfw-border-width-option-panel, 1px) |  | cascader,dropdown,select,treeselect |
| --wui-box-shadow-option-panel | var(--ynfw-box-shadow-option-panel, 0 2px 4px 0 rgba(0,0,0,.16)) |  | cascader,dropdown,select,treeselect |
| --wui-button-border-radius | var(--ynfw-border-radius-btn, 4px) |  | button,space |
| --wui-button-default-bg-color-hover | var(--ynfw-color-bg-btn-hover, #F3F5F9) |  | button,calendar |
| --wui-button-default-color | var(--ynfw-color-text-btn-default, #505766) |  | button,dropdown |
| --wui-button-default-height | var(--ynfw-size-height-btn, 28px) |  | button,skeleton |
| --wui-button-text-color | var(--ynfw-color-text-textbtn-default, #0033cc) |  | button,cascader,input,input-number |
| --wui-button-text-color-active | var(--ynfw-color-text-textbtn-pressed,#0066ff) |  | button,cascader,input,input-number |
| --wui-button-text-color-hover | var(--ynfw-color-text-textbtn-hover, #0066ff) |  | button,cascader,input,input-number |
| --wui-checkbox-color-bg-fill-checkbox-selected-disabled | var(--ynfw-color-bg-fill-checkbox-selected-disabled, #F79099) |  | cascader,checkbox |
| --wui-checkbox-color-bg-mark-fill-selected | var(--ynfw-color-bg-mark-fill-checkbox-selected, #FFFFFF) |  | cascader,checkbox,tree |
| --wui-checkbox-color-bg-mark-selected | var(--ynfw-color-bg-mark-checkbox-selected, var(--wui-primary-color)) |  | checkbox,tree |
| --wui-checkbox-color-bg-mark-selected-disabled | var(--ynfw-color-bg-mark-checkbox-selected-disabled, #CCCCCC) |  | checkbox,tree,treeselect |
| --wui-collapse-inverse-content-text-color |  |  | popover,slider,tooltip |
| --wui-color-bg-option-hover | var(--ynfw-color-bg-option-hover, var(--wui-base-item-bg-hover)) |  | calendar,cascader,input-number,menu,select,table,transfer,tree,treeselect |
| --wui-color-bg-option-panel | var(--ynfw-color-bg-option-panel, var(--wui-base-panel-bg-color)) |  | cascader,select,treeselect |
| --wui-color-bg-option-selected | var(--ynfw-color-bg-option-selected, var(--wui-base-item-bg-selected)) |  | calendar,cascader,menu,select,table,transfer,tree,treeselect |
| --wui-color-bg-option-selected-hover | var(--ynfw-color-bg-option-selected-hover, var(--wui-base-item-bg-selected-hover)) |  | cascader,menu,select,table,transfer,tree,treeselect |
| --wui-color-border-option-panel | var(--ynfw-color-border-option-panel, #D9D9D9) |  | cascader,dropdown,select,treeselect |
| --wui-color-danger | var(--ynfw-color-danger, var(--wui-danger-color)) |  | modal,notification,upload |
| --wui-color-icon-close-feedback | var(--ynfw-color-icon-close-feedback, var(--wui-base-close-icon-color)) |  | drawer,message,modal,notification,upload |
| --wui-color-icon-close-feedback-hover | var(--ynfw-color-icon-close-feedback-hover, var(--wui-base-close-icon-color-hover)) |  | drawer,message,modal,notification,upload |
| --wui-color-icon-global-hover | var(--ynfw-color-icon-collapse-tree-hover, #4B5563) |  | table,tree |
| --wui-color-info | var(--ynfw-color-info, var(--wui-info-color)) |  | modal,notification,upload |
| --wui-color-success | var(--ynfw-color-success, var(--wui-success-color)) |  | modal,notification,upload |
| --wui-color-warning | var(--ynfw-color-warning, var(--wui-warning-color)) |  | modal,notification,popover,upload |
| --wui-danger-color | var(--ynfw-color-danger, #ff5735) |  | badge,button,checkbox,colorpicker,form,progress,radio,steps,switch,table,timeline,upload |
| --wui-danger-color-hover | var(--ynfw-color-danger, #cc452a) |  | button,checkbox,radio |
| --wui-dark-color | var(--ynfw-color-dark, #505766) |  | badge,button,calendar,cascader,checkbox,colorpicker,menu,message,popover,progress,radio,select,slider,switch,tag,tooltip,tree |
| --wui-dark-color-active | var(--ynfw-color-dark-pressed, #404551) |  | button,popover |
| --wui-dark-color-hover | var(--ynfw-color-dark-hover, #404551) |  | button,checkbox,radio |
| --wui-font-size-feedback | var(--ynfw-font-size-feedback, 12px) |  | drawer,message,modal,notification,upload |
| --wui-icon-font-family |  |  | cascader,checkbox,icon,menu,message,progress,radio,steps,table,transfer,tree,treeselect,upload |
| --wui-info-color | var(--ynfw-color-info, #588ce9) |  | autocomplete,badge,button,card,checkbox,datepicker,form,layout,radio,steps,switch,table,timeline,timepicker,upload |
| --wui-info-color-active | var(--ynfw-color-info, #4670ba) |  | button,datepicker,table |
| --wui-info-color-hover | var(--ynfw-color-info-hover, #4670ba) |  | button,checkbox,radio,table |
| --wui-input-bg | var(--ynfw-color-bg-input, var(--wui-base-bg-color)) |  | cascader,datepicker,input-group,input-number,timepicker |
| --wui-input-bg | var(--ynfw-color-bg-input, var(--wui-base-bg-color)) |  | cascader,datepicker,input,input-number,timepicker |
| --wui-input-bg-color-required | var(--ynfw-color-bg-input-required, #fffcea) |  | cascader,datepicker,form,input,input-number,timepicker |
| --wui-input-bg-disabled | var(--ynfw-color-bg-global-disabled, var(--wui-base-bg-color-disabled)) |  | cascader,datepicker,form,input,input-number,timepicker |
| --wui-input-bg-readonly | var(--ynfw-color-bg-global-readonly, var(--wui-base-bg-color-readonly)) |  | cascader,datepicker,input,input-number,timepicker |
| --wui-input-border-bottom-color | var(--ynfw-color-border-input-required, #F59E0B) |  | cascader,datepicker,input,input-number,timepicker |
| --wui-input-border-color | var(--ynfw-color-border-input, rgba(80, 87, 102, 0.35)) |  | cascader,datepicker,form,input-group,input-number,timepicker,transfer |
| --wui-input-border-color | var(--ynfw-color-border-input, rgba(80, 87, 102, 0.35)) |  | cascader,datepicker,form,input,input-number,timepicker,transfer |
| --wui-input-border-color-disabled | var(--ynfw-color-border-input-disabled, rgba(80, 87, 102, 0.2)) |  | cascader,checkbox,datepicker,form,input,input-number,rate,timepicker |
| --wui-input-border-color-focus | var(--ynfw-color-border-focused, #0091ff) |  | cascader,datepicker,form,input,input-number,timepicker |
| --wui-input-border-color-hover | var(--ynfw-color-border-input-hover, rgba(80, 87, 102, 0.8)) |  | cascader,datepicker,input,input-number,timepicker |
| --wui-input-color | var(--ynfw-color-text-primary-global, #111) |  | cascader,datepicker,input,input-number,select |
| --wui-input-color-disabled | var(--ynfw-color-text-disabled, var(--wui-base-text-color-disabled)) |  | cascader,datepicker,input,input-number |
| --wui-input-font-size | var(--ynfw-font-size-input, 12px) |  | cascader,input,input-number,treeselect |
| --wui-input-placeholder-color | var(--ynfw-color-text-input-placeholder, #ccc) |  | cascader,datepicker,input,input-number,select,timepicker |
| --wui-input-placeholder-font-size | var(--ynfw-font-size-input, 12px) |  | cascader,datepicker,input,input-number,timepicker |
| --wui-input-suffix-icon-background-color-hover | var(--ynfw-color-bg-icon-input-hover, transparent) |  | cascader,datepicker,input,input-number,timepicker |
| --wui-input-suffix-icon-color | var(--ynfw-color-icon-input-suffix, rgba(80, 87, 102, 0.6)) |  | cascader,datepicker,input-group,input-number,menu,select,table,timepicker |
| --wui-input-suffix-icon-color | var(--ynfw-color-icon-input-suffix, rgba(80, 87, 102, 0.6)) |  | cascader,datepicker,input,input-number,menu,select,table,timepicker |
| --wui-input-suffix-icon-color-active | var(--ynfw-color-icon-input-suffix-pressed, rgba(80, 87, 102, 1)) |  | cascader,datepicker,input,input-number,timepicker |
| --wui-input-suffix-icon-color-disabled | var(--ynfw-color-icon-input-suffix-disabled, #ccc) |  | cascader,datepicker,input,input-number,select,timepicker |
| --wui-input-suffix-icon-color-hover | var(--ynfw-color-icon-input-suffix-hover, rgba(80, 87, 102, 1)) |  | cascader,datepicker,input-group,input-number,timepicker |
| --wui-input-suffix-icon-color-hover | var(--ynfw-color-icon-input-suffix-hover, rgba(80, 87, 102, 1)) |  | cascader,datepicker,input,input-number,timepicker |
| --wui-input-suffix-icon-color-readonly | var(--ynfw-color-icon-input-suffix-disabled, #ccc) |  | cascader,datepicker,input,input-number,timepicker |
| --wui-input-suffix-icon-font-size | var(--ynfw-font-size-icon-input, 16px) |  | cascader,datepicker,input,input-number,select,timepicker |
| --wui-menu-separate-hover | var(--ynfw-color-deepen-item-menu-hover , #E7EAEE) |  | menu,table |
| --wui-modal-border-radius | var(--ynfw-border-radius-modal, 4px) |  | modal,upload |
| --wui-modal-border-style | var(--ynfw-border-style-modal, solid) |  | modal,upload |
| --wui-modal-border-width | var(--ynfw-border-width-modal, 1px) |  | modal,upload |
| --wui-modal-box-shadow | var(--ynfw-box-shadow-modal, 0 0 10px 0 rgba(0, 0, 0, 0.2)) |  | modal,upload |
| --wui-modal-color-bg | var(--ynfw-color-bg-modal, var(--wui-base-panel-bg-color)) |  | modal,upload |
| --wui-modal-color-border | var(--ynfw-color-border-modal, var(--wui-base-border-color)) |  | modal,upload |
| --wui-modal-color-text-content | var(--ynfw-color-text-content-modal, var(--wui-base-text-color)) |  | modal,upload |
| --wui-modal-color-text-title | var(--ynfw-color-text-title-modal, var(--wui-base-text-color)) |  | modal,upload |
| --wui-modal-font-size-content | var(--ynfw-font-size-content-modal, 12px) |  | modal,upload |
| --wui-modal-font-size-icon-info | var(--ynfw-font-size-icon-info-modal, 18px) |  | modal,notification,upload |
| --wui-modal-font-size-title | var(--ynfw-font-size-title-modal, 14px) |  | modal,upload |
| --wui-modal-font-weight-content | var(--ynfw-font-weight-content-modal, 400) |  | modal,upload |
| --wui-modal-font-weight-title | var(--ynfw-font-weight-title-modal, 600) |  | modal,upload |
| --wui-picker-border-radius-cell | var(--ynfw-border-radius-cell-datepicker, 4px) |  | calendar,datepicker |
| --wui-picker-border-radius-panel | var(--ynfw-border-radius-panel-picker, 4px) |  | calendar,datepicker,timepicker |
| --wui-picker-border-style-panel | var(--ynfw-border-style-panel-picker, solid) |  | calendar,datepicker,timepicker |
| --wui-picker-border-width-panel | var(--ynfw-border-width-panel-picker, 1px) |  | calendar,datepicker,timepicker |
| --wui-picker-box-shadow-panel | var(--ynfw-box-shadow-panel-picker, 0 2px 4px 0 rgba(0,0,0,.16)) |  | calendar,datepicker,timepicker |
| --wui-picker-cell-bg-color-hover | var(--ynfw-color-bg-calendar-cell-hover, var(--wui-primary-color-light)) |  | datepicker,timepicker |
| --wui-picker-cell-size | var(--ynfw-size-height-cell-datepicker, 24px) |  | calendar,datepicker |
| --wui-picker-color-bg-cell-focus | var(--ynfw-color-bg-cell-datepicker-focus, var(--wui-primary-color)) |  | calendar,datepicker |
| --wui-picker-color-bg-cell-hover | var(--ynfw-color-bg-cell-datepicker-hover, var(--wui-primary-color-light)) |  | calendar,datepicker |
| --wui-picker-color-bg-cell-selected | var(--ynfw-color-bg-cell-datepicker-selected, var(--wui-primary-color)) |  | calendar,datepicker |
| --wui-picker-color-bg-panel | var(--ynfw-color-bg-panel-picker, var(--wui-base-panel-bg-color)) |  | calendar,datepicker |
| --wui-picker-color-border-panel | var(--ynfw-color-border-panel-picker, var(--wui-base-border-color)) |  | calendar,datepicker,timepicker |
| --wui-picker-color-icon-panel-hover | var(--ynfw-color-icon-panel-datepicker-hover, #505f79) |  | calendar,datepicker |
| --wui-picker-color-text-content-hover | var(--ynfw-color-text-content-datepicker-hover, var(--wui-base-item-color-active)) |  | datepicker,timepicker |
| --wui-picker-font-size-content | var(--ynfw-font-size-content-datepicker, 14px) |  | datepicker,timepicker |
| --wui-picker-font-size-header | var(--ynfw-font-size-header-datepicker, 14px) |  | calendar,datepicker |
| --wui-picker-font-size-panel | var(--ynfw-font-size-panel-datepicker, 12px) |  | calendar,datepicker |
| --wui-picker-size-width-cell | var(--ynfw-size-width-cell-datepicker, 24px) |  | calendar,datepicker |
| --wui-primary-color | var(--ynfw-color-primary, rgb(238, 34, 51)) |  | anchor,badge,button,calendar,cascader,checkbox,colorpicker,datepicker,menu,progress,select,spin,steps,switch,tabs,timeline,transfer,tree,upload |
| --wui-primary-color-hover | var(--ynfw-color-primary-hover, rgb(190, 27, 40)) |  | button,checkbox,tree |
| --wui-progress-bg-color | var(--ynfw-color-bg-line-progress, rgba(229,231,235,0.45)) |  | progress,upload |
| --wui-progress-border-radius | var(--ynfw-border-radius-line-progress, 100px) |  | progress,upload |
| --wui-progress-color-text | var(--ynfw-color-text-progress, var(--wui-base-text-color)) |  | progress,upload |
| --wui-progress-finished-bg-color | var(--ynfw-color-bg-line-progress-finished, var(--wui-info-color)) |  | progress,upload |
| --wui-progress-font-size | var(--ynfw-font-size-progress, 12px) |  | progress,upload |
| --wui-progress-font-weight | var(--ynfw-font-weight-progress, 400) |  | progress,upload |
| --wui-radio-border-radius-button | var(--ynfw-border-radius-button-radio, 4px) |  | checkbox,radio |
| --wui-radio-border-width-button | var(--ynfw-border-width-button-radio, 1px) |  | checkbox,radio |
| --wui-radio-button-color-text | var(--ynfw-color-text-radiobutton, var(--wui-dark-color)) |  | checkbox,radio |
| --wui-radio-button-color-text-disabled | var(--ynfw-color-text-radiobutton-disabled, #999) |  | checkbox,radio |
| --wui-radio-button-color-text-selected | var(--ynfw-color-text-radiobutton-selected, #111) |  | checkbox,radio |
| --wui-radio-button-font-size | var(--ynfw-font-size-radiobutton, 12px) |  | checkbox,radio |
| --wui-radio-button-font-weight | var(--ynfw-font-weight-radiobutton, 400) |  | checkbox,radio |
| --wui-radio-color-bg-button | var(--ynfw-color-bg-button-radio, #FFFFFF) |  | checkbox,radio |
| --wui-radio-color-bg-button-hover | var(--ynfw-color-bg-button-radio-hover, #f3f5f9) |  | checkbox,radio |
| --wui-radio-color-border-button | var(--ynfw-color-border-button-radio, var(--wui-base-border-color)) |  | checkbox,radio |
| --wui-radio-color-border-button-hover | var(--ynfw-color-border-button-radio-hover, #989ea8) |  | checkbox,radio |
| --wui-scrollbar-bg-color | var(--ynfw-color-bg-scrollbg-scrollbar, #f4f4f4) |  | calendar,cascader,datepicker,drawer,dropdown,error-message,layout,menu,modal,popover,select,slider,table,tabs,timepicker,tooltip,transfer,tree,upload |
| --wui-scrollbar-border-color | var(--ynfw-color-border-scrollbar, #dedede) |  | calendar,cascader,datepicker,drawer,dropdown,error-message,layout,menu,modal,popover,select,slider,table,tabs,timepicker,tooltip,transfer,tree,upload |
| --wui-scrollbar-color | var(--ynfw-color-bg-scroll-scrollbar, #99a3b0) |  | calendar,cascader,datepicker,drawer,dropdown,error-message,input,input-number,layout,menu,modal,popover,select,slider,table,tabs,timepicker,tooltip,transfer,tree,upload |
| --wui-scrollbar-hover-color | var(--ynfw-color-bg-scroll-scrollbar-hover, #687281) |  | calendar,cascader,datepicker,drawer,dropdown,error-message,input,input-number,layout,menu,modal,popover,select,slider,table,tabs,timepicker,tooltip,transfer,tree,upload |
| --wui-scrollbar-width | var(--ynfw-size-width-scroll-scrollbar, 8px) |  | calendar,cascader,drawer,dropdown,layout,modal,popover,select,table,tabs,transfer,tree,upload |
| --wui-secondary-color | var(--ynfw-color-bg-secondary, #dbe0e5) |  | button,table |
| --wui-select-color-text | var(--ynfw-color-text-select, var(--wui-base-item-color)) |  | select,treeselect |
| --wui-select-color-text-group | var(--ynfw-color-text-group-select, #999) |  | select,treeselect |
| --wui-select-font-size | var(--ynfw-font-size-select, 12px) |  | select,treeselect |
| --wui-select-font-size-group | var(--ynfw-font-size-group-select, 12px) |  | select,treeselect |
| --wui-select-font-weight | var(--ynfw-font-weight-select, 400) |  | select,treeselect |
| --wui-select-font-weight-group | var(--ynfw-font-weight-group-select, 400) |  | select,treeselect |
| --wui-select-loading-bg-color | var(--ynfw-color-border-light, #eee) |  | select,treeselect |
| --wui-select-loading-color | var(--ynfw-color-border-bold, #aaa) |  | select,treeselect |
| --wui-success-color | var(--ynfw-color-success, #18b681) |  | badge,button,checkbox,form,progress,radio,spin,steps,switch,timeline,upload |
| --wui-success-color-hover | var(--ynfw-color-success, #139167) |  | button,checkbox,radio |
| --wui-tooltip-border-color-feedback | var(--ynfw-color-border-feedback, #d9d9d9) |  | popover,slider,tooltip |
| --wui-tooltip-border-radius | var(--ynfw-border-radius-tooltip, 4px) |  | popover,slider,tooltip |
| --wui-tooltip-border-style-feedback | var(--ynfw-border-style-feedback, solid) |  | popover,slider,tooltip |
| --wui-tooltip-border-width-feedback | var(--ynfw-border-width-feedback, 1px) |  | popover,slider,tooltip |
| --wui-tooltip-box-shadow | var(--ynfw-box-shadow-tooltip, 0 1px 5px rgb(224,224,224)) |  | popover,slider,tooltip |
| --wui-tooltip-color-bg | var(--ynfw-color-bg-tooltip, var(--wui-dark-color)) |  | popover,slider,tooltip |
| --wui-tooltip-color-text | var(--ynfw-color-text-tooltip, #FFF) |  | popover,slider,tooltip |
| --wui-tooltip-custom-color |  |  | popover,slider,tooltip |
| --wui-tooltip-font-size | var(--ynfw-font-size-tooltip, 12px) |  | popover,slider,tooltip |
| --wui-tooltip-font-weight | var(--ynfw-font-weight-tooltip, 400) |  | popover,slider,tooltip |
| --wui-tree-color-text | var(--ynfw-color-text-tree, var(--wui-base-text-color)) |  | tree,treeselect |
| --wui-tree-font-size | var(--ynfw-font-size-tree, 12px) |  | tree,treeselect |
| --wui-tree-font-weight | var(--ynfw-font-weight-tree, 400) |  | tree,treeselect |
| --wui-warning-color | var(--ynfw-color-warning, #ffa600) |  | badge,button,checkbox,form,progress,radio,spin,switch,timeline |
| --wui-warning-color-hover | var(--ynfw-color-warning, #cc8400) |  | button,checkbox,radio |

## 组件css变量

### anchor

| 变量名称 | 默认值 | 描述  |
| ---- | --- | --- |
| --wui-anchor-nav-more-icon-font-size | var(--ynfw-font-size-icon-more-nav, 16px) |  |
| --wui-anchor-font-size | var(--ynfw-font-size-anchor, 12px) |  |
| --wui-anchor-font-weight | var(--ynfw-font-weight-anchor, 400) |  |
| --wui-anchor-line-border-width | var(--ynfw-border-width-line-anchor, 2px) |  |
| --wui-anchor-line-border-color | var(--ynfw-color-border-line-anchor, #f0f0f0) |  |
| --wui-anchor-color-text | var(--ynfw-color-text-anchor, var(--wui-base-text-color)) |  |
| --wui-anchor-color-text-hover | var(--ynfw-color-text-anchor-hover, var(--wui-primary-color)) |  |
| --wui-anchor-color-text-selected | var(--ynfw-color-text-anchor-selected, var(--wui-primary-color)) |  |
| --wui-anchor-selected-width | var(--ynfw-size-width-anchor-selected, 8px) |  |
| --wui-anchor-selected-height | var(--ynfw-size-height-anchor-selected, 8px) |  |
| --wui-anchor-focus-border-width | var(--ynfw-border-width-anchor-focus, 2px) |  |
| --wui-anchor-focus-border-color | var(--ynfw-color-border-anchor-focus, var(--wui-primary-color)) |  |
| --wui-anchor-focus-border-radius | var(--ynfw-border-radius-anchor-focus, 8px) |  |
| --wui-anchor-nav-more-icon-color-hover | var(--ynfw-color-icon-more-nav-hover, #505766) |  |
| --wui-anchor-nav-more-icon-color | var(--ynfw-color-icon-more-nav, #9CA3AF) |  |
| --wui-anchor-nav-more-icon-color-disbled | var(--ynfw-color-icon-anchor-disabled, #E5E7EB) |  |
| --wui-anchor-font-size-horizoncal | var(--ynfw-font-size-horizoncal-anchor, 16px) |  |
| --wui-anchor-font-weight-selected | var(--ynfw-font-weight-anchor-selected, 600) |  |
| --wui-anchor-crosswise-line-border-style | var(--ynfw-border-style-line-crosswise-anchor, dashed) |  |

### autocomplete

| 变量名称 | 默认值 | 描述  |
| ---- | --- | --- |
| --wui-base-item-color | var(--ynfw-color-text-option-panel, var(--wui-base-text-color)) |  |

### avatar

| 变量名称 | 默认值 | 描述  |
| ---- | --- | --- |
| --wui-avatar-color | var(--ynfw-color-text-avatar,#fff) |  |
| --wui-avatar-bg-color | var(--ynfw-color-bg-avatar, #ccc) |  |
| --wui-avatar-font-size | var(--ynfw-font-size-avatar, 14px) |  |
| --wui-avatar-border-color | var(--ynfw-color-border-avatar, #fff) |  |

### backtop

| 变量名称 | 默认值 | 描述  |
| ---- | --- | --- |
| --wui-back-top-size-width | var(--ynfw-size-width-backtop, 48px) |  |
| --wui-back-top-size-height | var(--ynfw-size-height-backtop, 48px) |  |
| --wui-back-top-border-radius | var(--ynfw-border-radius-backtop, 4px) |  |
| --wui-back-top-border-color | var(--ynfw-color-border-backtop, #D4D4D4) |  |
| --wui-back-top-border-color-hover | var(--ynfw-color-border-backtop-hover, #505766) |  |
| --wui-back-top-border-width | var(--ynfw-border-width-backtop, 1px) |  |
| --wui-back-top-border-style | var(--ynfw-border-style-backtop, solid) |  |
| --wui-back-top-bg-color | var(--ynfw-color-bg-backtop, #fff) |  |
| --wui-back-top-bg-color-hover | var(--ynfw-color-bg-backtop-hover, #F0F0F0) |  |
| --wui-back-top-font-size | var(--ynfw-font-size-backtop, 24px) |  |
| --wui-back-top-font-color | var(--ynfw-color-icon-backtop, #505766) |  |

### badge

| 变量名称 | 默认值 | 描述  |
| ---- | --- | --- |
| --wui-badge-size-height | var(--ynfw-size-height-badge, 16px) |  |
| --wui-badge-border-radius | var(--ynfw-border-radius-badge, 8px) |  |
| --wui-badge-bg-color | var(--ynfw-color-bg-badge, var(--wui-primary-color)) |  |
| --wui-badge-color-text | var(--ynfw-color-text-badge, #FFF) |  |
| --wui-badge-font-weight | var(--ynfw-font-weight-badge, 400) |  |

### breadcrumb

| 变量名称 | 默认值 | 描述  |
| ---- | --- | --- |
| --wui-breadcrumb-bg-color | var(--ynfw-color-bg-breadcrumb, #f5f5f5) |  |
| --wui-breadcrumb-border-radius | var(--ynfw-border-radius-breadcrumb, 4px) |  |
| --wui-breadcrumb-color-text-disabled | var(--ynfw-color-text-breadcrumb-disabled, #999) |  |
| --wui-breadcrumb-font-size | var(--ynfw-font-size-breadcrumb, 14px) |  |
| --wui-breadcrumb-font-weight | var(--ynfw-font-weight-breadcrumb, 400) |  |
| --wui-breadcrumb-color-text-hover | var(--ynfw-color-text-breadcrumb-hover, #333) |  |
| --wui-breadcrumb-color-text | var(--ynfw-color-text-breadcrumb, #333) |  |

### button

| 变量名称 | 默认值 | 描述  |
| ---- | --- | --- |
| --wui-button-default-border-color | var(--ynfw-color-border-sideline-btn-default, #bbb) |  |
| --wui-button-default-font-size | var(--ynfw-font-size-btn, 12px) |  |
| --wui-button-default-font-weight | var(--ynfw-font-weight-btn, 400) |  |
| --wui-button-default-color-hover | var(--ynfw-color-text-btn-hover, #373c47) |  |
| --wui-button-default-border-color-hover | var(--ynfw-color-border-sideline-btn-hover, #505766) |  |
| --wui-button-default-color-active | var(--ynfw-color-text-btn-pressed, #373c47) |  |
| --wui-button-default-border-color-active | var(--ynfw-color-border-sideline-btn-pressed, #505766) |  |
| --wui-button-default-bg-color-disabled | var(--ynfw-color-bg-btn-disabled, #FFF) |  |
| --wui-button-text-color-disabled | var(--ynfw-color-text-textbtn-disabled, #ccc) |  |
| --wui-button-default-border-color-disabled | var(--ynfw-color-border-sideline-btn-disable, #DDD) |  |
| --wui-button-secondary-bg-color-disabled | var(--ynfw-color-bg-secondary-btn-disabled, #EDF0F2) |  |
| --wui-button-primary-bg-color-disabled | var(--ynfw-color-primary-disabled, #f79099) |  |
| --wui-button-link-font-weight | var(--ynfw-font-weight-textbtn, 400) |  |
| --wui-button-link-font-size | var(--ynfw-font-size-textbtn, 12px) |  |
| --wui-primary-color-active | var(--ynfw-color-primary-pressed, rgb(190, 27, 40)) |  |
| --wui-secondary-color-hover | var(--ynfw-color-bg-secondary-hover, #c4c9cd) |  |
| --wui-secondary-color-active | var(--ynfw-color-bg-secondary-pressed, #c4c9cd) |  |
| --wui-warning-color-active | var(--ynfw-color-warning, #cc8400) |  |
| --wui-success-color-active | var(--ynfw-color-success, #139167) |  |
| --wui-danger-color-active | var(--ynfw-color-danger, #cc452a) |  |
| --wui-button-text-inverse-color | var(--ynfw-color-text-inverse-textbtn, #3d8df9) |  |
| --wui-button-text-inverse-color-hover | var(--ynfw-color-text-inverse-textbtn-hover, #67aefb) |  |

### button-group

| 变量名称 | 默认值 | 描述  |
| ---- | --- | --- |
| --wui-button-default-font-size | var(--ynfw-font-size-btn, 12px) |  |

### calendar

| 变量名称 | 默认值 | 描述  |
| ---- | --- | --- |
| --wui-calendar-font-weight-week | var(--ynfw-font-weight-week-calendar, 400) |  |
| --wui-calendar-color-text-week | var(--ynfw-color-text-week-calendar, #111) |  |
| --wui-calendar-font-size-week | var(--ynfw-font-size-week-calendar, 12px) |  |
| --wui-calendar-color-text-content | var(--ynfw-color-text-content-calendar, #111) |  |
| --wui-calendar-color-text-content-hover | var(--ynfw-color-text-content-calendar-hover, var(--wui-primary-color)) |  |
| --wui-calendar-font-size-content | var(--ynfw-font-size-content-calendar, 14px) |  |
| --wui-calendar-font-weight-content | var(--ynfw-font-weight-content-calendar, 400) |  |
| --wui-calendar-color-text-content-disabled | var(--ynfw-color-text-content-calendar-disabled, var(--wui-base-item-color-disabled)) |  |
| --wui-calendar-color-text-content-selected | var(--ynfw-color-text-content-card-calendar-selected, #fff) |  |
| --wui-calendar-color-text-header | var(--ynfw-color-text-header-calendar, #111111) |  |
| --wui-calendar-font-size-header | var(--ynfw-font-size-header-calendar, 12px) |  |
| --wui-calendar-font-weight-header | var(--ynfw-font-weight-header-calendar, 400) |  |
| --wui-calendar-table-header-border-color | var(--ynfw-color-border-calendar-header, #505766) |  |
| --wui-calendar-table-header-bg-color | var(--ynfw-color-bg-calendar-header, #f7f9fd) |  |
| --wui-base-item-bg-hover | var(--ynfw-color-bg-global-hover, #f0f0f0) |  |
| --wui-primary-color-light | var(--ynfw-color-primary-light, rgba(238, 34, 51, 0.1)) |  |
| --wui-picker-color-icon-panel | var(--ynfw-color-icon-panel-datepicker, var(--wui-input-color-disabled)) |  |

### card

| 变量名称 | 默认值 | 描述  |
| ---- | --- | --- |
| --wui-card-color-bg-body | var(--ynfw-color-bg-body-card, var(--wui-base-bg-color)) |  |
| --wui-card-border-radius | var(--ynfw-border-radius-card, 4px) |  |
| --wui-card-border-width | var(--ynfw-border-width-card, 1px) |  |
| --wui-card-border-style | var(--ynfw-border-style-card, solid) |  |
| --wui-card-color-text-title | var(--ynfw-color-text-title-card, var(--wui-base-text-color)) |  |
| --wui-card-font-weight-title | var(--ynfw-font-weight-title-card, 500) |  |
| --wui-card-font-size-title | var(--ynfw-font-size-title-card, 16px) |  |
| --wui-card-color-bg-header | var(--ynfw-color-bg-header-card, var(--wui-base-bg-color)) |  |
| --wui-card-border-width-header | var(--ynfw-border-width-header-card, 1px) |  |
| --wui-card-border-style-header | var(--ynfw-border-style-header-card, solid) |  |
| --wui-card-color-border-header | var(--ynfw-color-border-header-card, var(--wui-base-border-color)) |  |
| --wui-card-color-text-content | var(--ynfw-color-text-content-card, #111) |  |
| --wui-card-font-weight-content | var(--ynfw-font-weight-content-card, 400) |  |
| --wui-card-font-size-content | var(--ynfw-font-size-content-card, 12px) |  |
| --wui-card-head-bg-color | var(--ynfw-color-bg-card-header, #fafafa) |  |

### cascader

| 变量名称 | 默认值 | 描述  |
| ---- | --- | --- |
| --wui-cascader-size-width | var(--ynfw-size-width-cascader, 120px) |  |
| --wui-cascader-border-width-divider | var(--ynfw-border-width-divider-cascader, 1px) |  |
| --wui-cascader-border-style-divider | var(--ynfw-border-style-divider-cascader, solid) |  |
| --wui-cascader-color-divider | var(--ynfw-color-divider-cascader, #E9E9E9) |  |
| --wui-cascader-color-text | var(--ynfw-color-text-cascader, var(--wui-base-item-color)) |  |
| --wui-cascader-color-text-disabled | var(--ynfw-color-text-cascader-disabled, var(--wui-base-item-color-disabled)) |  |
| --wui-cascader-font-size-icon | var(--ynfw-font-size-icon-cascader, 12px) |  |
| --wui-cascader-color-icon | var(--ynfw-color-icon-cascader, #A8ABB3) |  |
| --wui-cascader-color-icon-hover | var(--ynfw-color-icon-cascader-hover, #505766) |  |
| --wui-cascader-color-icon-pressed | var(--ynfw-color-icon-cascader-pressed, #505766) |  |
| --wui-cascader-font-size | var(--ynfw-font-size-cascader, 12px) |  |
| --wui-cascader-font-weight | var(--ynfw-font-weight-cascader, 400) |  |

### checkbox

| 变量名称 | 默认值 | 描述  |
| ---- | --- | --- |
| --wui-checkbox-font-size | var(--ynfw-font-size-checkbox, 12px) |  |
| --wui-checkbox-font-weight | var(--ynfw-font-weight-checkbox, 400) |  |
| --wui-checkbox-color-bg-fill-checkbox-selected | var(--ynfw-color-bg-fill-checkbox-selected, #EE2233) |  |
| --wui-checkbox-border-radius | var(--ynfw-border-radius-checkbox, 2px) |  |
| --wui-checkbox-color-border | var(--ynfw-color-border-checkbox, var(--wui-input-border-color)) |  |
| --wui-checkbox-color-bg | var(--ynfw-color-bg-checkbox, var(--wui-base-bg-color)) |  |
| --wui-checkbox-color-bg-fill-checkbox-selected-hover | var(--ynfw-color-bg-fill-checkbox-selected-hover, #be1b28) |  |
| --wui-checkbox-color-border-hover | var(--ynfw-color-border-checkbox-hover, var(--wui-input-border-color-hover)) |  |
| --wui-checkbox-color-bg-fill-checkbox-disabled | var(--ynfw-color-bg-fill-checkbox-disabled, #F7f7f7) |  |
| --wui-checkbox-color-border-fill-checkbox-disabled | var(--ynfw-color-border-fill-checkbox-disabled, #D1D5DB) |  |
| --wui-checkbox-color-bg-disabled | var(--ynfw-color-bg-checkbox-disabled, var(--wui-base-bg-color-disabled)) |  |
| --wui-checkbox-color-text | var(--ynfw-color-text-checkbox, var(--wui-base-text-color)) |  |
| --wui-checkbox-color-border-fill-checkbox | var(--ynfw-color-border-fill-checkbox, #D4D4D4) |  |
| --wui-checkbox-color-bg-fill-checkbox | #FFF |  |
| --wui-checkbox-color-text-disabled | var(--ynfw-color-text-checkbox-disabled, var(--wui-base-item-color-disabled)) |  |
| --wui-checkbox-color-border-disabled | var(--ynfw-color-border-checkbox-disabled, var(--wui-input-border-color-disabled)) |  |
| --theme-color-disabled |  |  |
| --wui-checkbox-color-border-fill-checkbox-hover | var(--ynfw-color-border-fill-checkbox-hover, #505766) |  |
| --wui-checkbox-size-height-lg-button | var(--ynfw-size-height-lg-button-checkbox, 32px) |  |
| --wui-checkbox-size-height-md-button | var(--ynfw-size-height-md-button-checkbox, 28px) |  |
| --wui-checkbox-size-height-xs-button | var(--ynfw-size-height-xs-button-checkbox, 20px) |  |

### collapse

| 变量名称 | 默认值 | 描述  |
| ---- | --- | --- |
| --wui-collapse-color-bg-body | var(--ynfw-color-bg-body-collapse, var(--wui-base-bg-color)) |  |
| --wui-collapse-border-radius | var(--ynfw-border-radius-collapse, 4px) |  |
| --wui-collapse-border-width | var(--ynfw-border-width-collapse, 1px) |  |
| --wui-collapse-border-style | var(--ynfw-border-style-collapse, solid) |  |
| --wui-collapse-color-border | var(--ynfw-color-border-collapse, var(--wui-base-border-color)) |  |
| --wui-collapse-font-size-title | var(--ynfw-font-size-title-collapse, 14px) |  |
| --wui-collapse-font-weight-title | var(--ynfw-font-weight-title-collapse, 400) |  |
| --wui-collapse-color-text-title | var(--ynfw-color-text-title-collapse, var(--wui-base-text-color)) |  |
| --wui-collapse-size-height-header | var(--ynfw-size-height-header-collapse, 40px) |  |
| --wui-collapse-font-size-content | var(--ynfw-font-size-content-collapse, 12px) |  |
| --wui-collapse-font-weight-content | var(--ynfw-font-weight-content-collapse, 400) |  |
| --wui-collapse-color-text-content | var(--ynfw-color-text-content-collapse, var(--wui-base-text-color)) |  |
| --wui-collapse-list-bg-color | var(--ynfw-color-bg-list-collapse, #F9FBFF) |  |
| --wui-collapse-list-text-color | var(--ynfw-color-text-title-list-collapse, #111) |  |
| --wui-collapse-list-text-font-size | var(--ynfw-font-size-title-list-collapse, 13px) |  |
| --wui-collapse-list-text-font-weight | var(--ynfw-font-weight-title-list-collapse, 700) |  |
| --wui-collapse-list-title-height | var(--ynfw-size-height-title-list-collapse, 32px) |  |
| --wui-collapse-header-icon-color | var(--ynfw-color-bg-icon-title-card-collapse, #9CA3AF) |  |
| --wui-collapse-list-divider-width | var(--ynfw-border-width-divider-list-collapse, 1px) |  |
| --wui-collapse-list-divider-style | var(--ynfw-border-style-divider-list-collapse, dashed) |  |
| --wui-collapse-list-divider-color | var(--ynfw-color-border-divider-list-collapse, #d4d4d4) |  |
| --wui-collapse-card-bg-color | var(--ynfw-color-bg-card-collapse, #F9FBFF) |  |
| --wui-collapse-card-text-color | var(--ynfw-color-text-title-card-collapse, #111) |  |
| --wui-collapse-card-text-font-size | var(--ynfw-font-size-title-card-collapse, 16px) |  |
| --wui-collapse-card-text-font-weight | var(--ynfw-font-weight-title-card-collapse, 700) |  |
| --wui-collapse-card-title-height | var(--ynfw-size-height-title-card-collapse, 32px) |  |
| --wui-collapse-card-icon-size | var(--ynfw-font-size-icon-card-collapse, 16px) |  |
| --wui-collapse-list-content-text-color | var(--ynfw-color-text-content-list-collapse, #333) |  |
| --wui-collapse-list-content-text-font-size | var(--ynfw-font-size-content-list-collapse, 13px) |  |
| --wui-collapse-list-content-font-weight | var(--ynfw-font-weight-content-list-collapse, 400) |  |
| --wui-collapse-card-content-text-color | var(--ynfw-color-text-content-card-collapse, #333) |  |
| --wui-collapse-card-content-text-font-size | var(--ynfw-font-size-content-card-collapse, 13px) |  |
| --wui-collapse-card-content-font-weight | var(--ynfw-font-weight-content-card-collapse, 400) |  |
| --wui-collapse-card2-color-bg | var(--ynfw-color-bg-card2-collapse, #eff6ff) |  |
| --wui-collapse-list2-color-border | var(--ynfw-color-border-list2-collapse, #ef4444) |  |
| --wui-collapse-list2-color-bg | var(--ynfw-color-bg-list2-collapse, #ffffff) |  |
| --wui-collapse-color-bg-header | var(--ynfw-color-bg-header-collapse, var(--wui-base-bg-color)) |  |

### datepicker

| 变量名称 | 默认值 | 描述  |
| ---- | --- | --- |
| --wui-picker-cell-bg-color-selected | var(--ynfw-color-bg-calendar-cell-selected, var(--wui-primary-color-light)) |  |
| --wui-picker-size-height-header-panel | var(--ynfw-size-height-header-panel-datepicker, 40px) |  |
| --wui-picker-font-weight-header | var(--ynfw-font-weight-header-datepicker, 400) |  |
| --wui-picker-color-text-header | var(--ynfw-color-text-header-datepicker, var(--wui-base-text-color)) |  |
| --wui-picker-font-weight-week | var(--ynfw-font-weight-week-datepicker, 400) |  |
| --wui-picker-font-size-week | var(--ynfw-font-size-week-datepicker, 14px) |  |
| --wui-picker-color-text-week | var(--ynfw-color-text-week-datepicker, var(--wui-base-text-color)) |  |
| --wui-picker-color-text-content-disabled | var(--ynfw-color-text-content-datepicker-disabled, var(--wui-input-color-disabled)) |  |
| --wui-picker-color-text-content | var(--ynfw-color-text-content-datepicker, var(--wui-base-text-color)) |  |
| --wui-picker-size-height-footer | var(--ynfw-size-height-footer-picker, 40px) |  |
| --wui-picker-font-size-textbtn-footer | var(--ynfw-font-size-textbtn-footer-picker, 14px) |  |
| --wui-picker-input-font-size | var(--ynfw-font-size-input, var(--wui-input-font-size)) |  |
| --wui-picker-font-weight-content | var(--ynfw-font-weight-content-datepicker, 400) |  |
| --wui-input-active-bg-color | var(--ynfw-input-active-bg-color, #DBEAFE) |  |

### drawer

| 变量名称 | 默认值 | 描述  |
| ---- | --- | --- |
| --wui-drawer-color-bg | var(--ynfw-color-bg-drawer, var(--wui-base-panel-bg-color)) |  |
| --wui-drawer-border-width | var(--ynfw-border-width-drawer, 1px) |  |
| --wui-drawer-border-style | var(--ynfw-border-style-drawer, solid) |  |
| --wui-drawer-color-border | var(--ynfw-color-border-drawer, var(--wui-base-border-color)) |  |
| --wui-drawer-border-radius | var(--ynfw-border-radius-drawer, 8px) |  |
| --wui-drawer-box-shadow | var(--ynfw-box-shadow-drawer, 0 0 15px rgba(80, 87, 102, .2)) |  |
| --wui-drawer-font-size-title | var(--ynfw-font-size-title-drawer, 14px) |  |
| --wui-drawer-font-weight-title | var(--ynfw-font-weight-title-drawer, 600) |  |
| --wui-drawer-color-text-title | var(--ynfw-color-text-title-drawer, var(--wui-base-text-color)) |  |

### empty

| 变量名称 | 默认值 | 描述  |
| ---- | --- | --- |
| --wui-empty-color-text | var(--ynfw-color-text-empty, var(--wui-base-close-icon-color)) |  |
| --wui-empty-font-size | var(--ynfw-font-size-empty, 14px) |  |
| --wui-empty-font-weight | var(--ynfw-font-weight-empty, 400) |  |

### form

| 变量名称 | 默认值 | 描述  |
| ---- | --- | --- |
| --wui-form-label-font-size | var(--ynfw-font-size-text, 12px) |  |
| --wui-form-label-font-weight | var(--ynfw-font-weight-text, 400) |  |
| --wui-form-extra-font-size | var(--ynfw-font-size-error-text, 12px) |  |
| --wui-form-color-bg-underline-form-error | var(--ynfw-color-bg-input-danger, #FFF1F2) |  |

### input-number

| 变量名称 | 默认值 | 描述  |
| ---- | --- | --- |
| --wui-browser-border-bottom-color | var(--ynfw-color-border-value-form, #E5E7EB) |  |

### list

| 变量名称 | 默认值 | 描述  |
| ---- | --- | --- |
| --wui-list-color-text-title | var(--ynfw-color-text-title-list, var(--wui-base-text-color)) |  |
| --wui-list-font-size-title | var(--ynfw-font-size-title-list, 16px) |  |
| --wui-list-font-weight-title | var(--ynfw-font-weight-title-list, 400) |  |
| --wui-list-color-text-content | var(--ynfw-color-text-content-list, var(--wui-base-text-color)) |  |
| --wui-list-font-size-content | var(--ynfw-font-size-content-list, 14px) |  |
| --wui-list-font-weight-content | var(--ynfw-font-weight-content-list, 400) |  |
| --wui-list-color-border | var(--ynfw-color-border-list, #D9D9D9) |  |
| --wui-list-border-style | var(--ynfw-border-style-list, solid) |  |
| --wui-list-border-width | var(--ynfw-border-width-list, 1px) |  |
| --wui-list-border-radius | var(--ynfw-border-radius-list, 2px) |  |
| --wui-list-color-border-item | var(--ynfw-color-border-item-list, #f0f0f0) |  |
| --wui-list-border-style-item | var(--ynfw-border-style-item-list, solid) |  |
| --wui-list-border-width-item | var(--ynfw-border-width-item-list, 1px) |  |

### menu

| 变量名称 | 默认值 | 描述  |
| ---- | --- | --- |
| --wui-menu-font-size | var(--ynfw-font-size-menu, 12px) |  |
| --wui-menu-color-text | var(--ynfw-color-text-menu, var(--wui-base-item-color)) |  |
| --wui-menu-bg-color | var(--ynfw-color-bg-menu, #FFF) |  |
| --wui-menu-border-width | var(--ynfw-border-width-menu, 1px) |  |
| --wui-menu-border-color | var(--ynfw-color-border-menu, #d9d9d9) |  |
| --wui-menu-border-radius | var(--ynfw-border-radius-menu, 4px) |  |
| --wui-menu-color-text-disabled | var(--ynfw-color-text-menu-disabled, var(--wui-base-item-color-disabled)) |  |
| --wui-menu-arrow-icon-font-size | var(--ynfw-font-size-arrow-item-menu, 12px) |  |
| --wui-menu-font-weight | var(--ynfw-font-weight-menu, 400) |  |
| --wui-menu-item-bg-color-hover | var(--ynfw-color-bg-item-menu-hover, #F0F0F0) |  |
| --wui-menu-color-text-selected | var(--ynfw-color-text-menu-selected, var(--wui-primary-color)) |  |
| --wui-menu-item-bg-color-selected | var(--ynfw-color-bg-item-menu-selected, #E9F0FA) |  |
| --wui-menu-item-bg-color-selected-hover | var(--ynfw-color-bg-item-menu-selected-hover, #DBE0E5) |  |
| --wui-menu-arrow-icon-color | var(--ynfw-color-icon-arrow-item-menu, rgba(80, 87, 102, 0.6)) |  |
| --wui-menu-arrow-icon-color-hover | var(--ynfw-color-icon-arrow-item-menu-hover, #505766) |  |
| --wui-menu-horizontal-underline-selected-border-color | var(--ynfw-color-border-underline-horizontal-menu-selected, var(--wui-primary-color)) |  |
| --wui-menu-item-border-width-selected | var(--ynfw-border-width-item-menu-selected, 3px) |  |
| --wui-menu-item-border-color-selected | var(--ynfw-color-border-item-menu-selected, var(--wui-primary-color)) |  |
| --wui-menu-item-size-height | var(--ynfw-size-height-item-menu, 42px) |  |
| --wui-menu-dark-bg-color | var(--ynfw-color-bg-dark-menu, #2e3c61) |  |
| --wui-menu-horizontal-underline-border-width | var(--ynfw-border-width-underline-horizontal-menu, 1px) |  |
| --wui-menu-horizontal-underline-border-color | var(--ynfw-color-border-underline-horizontal-menu, #d9d9d9) |  |
| --wui-menu-dark-bg-color-hover | var(--ynfw-color-bg-dark-menu-hover, rgba(0, 0, 0, 0.2)) |  |
| --wui-menu-dark-arrow-icon-color-hover | var(--ynfw-color-icon-arrow-item-menu-dark-hover, #FFF) |  |
| --wui-menu-dark-bg-color-selected | var(--ynfw-color-bg-dark-menu-selected, #000c17) |  |
| --ynfw-font-size-option-panel |  |  |
| --ynfw-font-weight-option-panel |  |  |

### message

| 变量名称 | 默认值 | 描述  |
| ---- | --- | --- |
| --wui-message-border-radius | var(--ynfw-border-radius-message, 4px) |  |
| --wui-message-border-width | var(--ynfw-border-width-message, 1px) |  |
| --wui-message-border-style | var(--ynfw-border-style-message, solid) |  |
| --wui-message-box-shadow | var(--ynfw-box-shadow-message, 0 4px 10px 0 rgba(0,0,0,0.15)) |  |
| --wui-message-color-text | var(--ynfw-color-text-message, #111) |  |
| --wui-message-font-size | var(--ynfw-font-size-message, 14px) |  |
| --wui-message-font-weight | var(--ynfw-font-weight-message, 400) |  |
| --wui-message-font-size-icon-info | var(--ynfw-font-size-icon-info-message, 18px) |  |
| --wui-message-color-text-inverse-fill | var(--ynfw-color-text-inverse-fill-message, #FFF) |  |
| --wui-message-color-bg | var(--ynfw-color-bg-message, #f7f9fb) |  |
| --wui-message-color-border | var(--ynfw-color-border-message, var(--wui-base-border-color)) |  |
| --wui-message-color-bg-fill-success | var(--ynfw-color-bg-fill-message-success, var(--wui-success-color)) |  |
| --wui-message-color-icon-inverse-fill | var(--ynfw-color-icon-inverse-fill-message, #FFF) |  |
| --wui-message-color-bg-fill-danger | var(--ynfw-color-bg-fill-message-danger, var(--wui-danger-color)) |  |
| --wui-message-color-bg-fill-info | var(--ynfw-color-bg-fill-message-info, var(--wui-info-color)) |  |
| --wui-message-color-bg-fill-warning | var(--ynfw-color-bg-fill-message-warning, var(--wui-warning-color)) |  |
| --wui-message-color-bg-success | var(--ynfw-color-bg-message-success, #eef9f5) |  |
| --wui-message-color-border-success | var(--ynfw-color-border-message-success, var(--wui-success-color)) |  |
| --wui-message-color-icon-success | var(--ynfw-color-icon-message-success, var(--wui-success-color)) |  |
| --wui-message-color-bg-danger | var(--ynfw-color-bg-message-danger, #fff4f2) |  |
| --wui-message-color-border-danger | var(--ynfw-color-border-message-danger, var(--wui-danger-color)) |  |
| --wui-message-color-icon-danger | var(--ynfw-color-icon-message-danger, var(--wui-danger-color)) |  |
| --wui-message-color-bg-info | var(--ynfw-color-bg-message-info, #edf4ff) |  |
| --wui-message-color-border-info | var(--ynfw-color-border-message-info, var(--wui-info-color)) |  |
| --wui-message-color-icon-info | var(--ynfw-color-icon-message-info, var(--wui-info-color)) |  |
| --wui-message-color-bg-warning | var(--ynfw-color-bg-message-warning, #fff7e8) |  |
| --wui-message-color-border-warning | var(--ynfw-color-border-message-warning, var(--wui-warning-color)) |  |
| --wui-message-color-icon-warning | var(--ynfw-color-icon-message-warning, var(--wui-warning-color)) |  |

### notification

| 变量名称 | 默认值 | 描述  |
| ---- | --- | --- |
| --wui-notification-border-radius | var(--ynfw-border-radius-notification, 4px) |  |
| --wui-notification-font-size-title | var(--ynfw-font-size-title-notification, 14px) |  |
| --wui-notification-font-weight-title | var(--ynfw-font-weight-title-notification, 600) |  |
| --wui-notification-color-text-title | var(--ynfw-color-text-title-notification, #111) |  |
| --wui-notification-font-size-content | var(--ynfw-font-size-content-notification, 14px) |  |
| --wui-notification-font-weight-content | var(--ynfw-font-weight-content-notification, 400) |  |
| --wui-notification-color-text-content | var(--ynfw-color-text-content-notification, #333) |  |
| --wui-notification-color-text-inverse-title | var(--ynfw-color-text-inverse-title-notification, #fff) |  |
| --wui-notification-color-text-inverse-content | var(--ynfw-color-text-inverse-content-notification, #fff) |  |
| --wui-notification-color-bg | var(--ynfw-color-bg-notification, #FFF) |  |

### pagination

| 变量名称 | 默认值 | 描述  |
| ---- | --- | --- |
| --wui-pagination-font-size | var(--ynfw-font-size-pagination, 12px) |  |
| --wui-pagination-font-weight | var(--ynfw-font-weight-pagination, 400) |  |
| --wui-pagination-color-text | var(--ynfw-color-text-pagination, var(--wui-pagination-color)) |  |
| --wui-pagination-color | var(--ynfw-color-text-primary-global, var(--wui-base-text-color)) |  |
| --wui-pagination-nointerval-border-color | var(--ynfw-color-border-pagenumber-nointerval-pagination, rgba(80, 87, 102, 0.35)) |  |
| --wui-pagination-pagenumber-bg-color | var(--ynfw-color-bg-pagenumber-pagination, #FFF) |  |
| --wui-pagination-nointerval-border-radius | var(--ynfw-border-radius-pagenumber-nointerval-pagination, 0) |  |
| --wui-pagination-pagenumber-border-radius | var(--ynfw-border-radius-pagenumber-pagination, 3px) |  |
| --wui-pagination-border-color | var(--ynfw-color-border-pagination-arrow-default, var(--wui-base-border-color)) |  |
| --wui-pagination-arrow-icon-color-hover | var(--ynfw-color-icon-arrow-pagination-hover, #111) |  |
| --wui-pagination-pagenumber-bg-color-hover | var(--ynfw-color-bg-pagenumber-pagination-hover, #edf1f7) |  |
| --wui-pagination-nointerval-border-color-hover | var(--ynfw-color-border-pagenumber-nointerval-pagination-hover, rgba(80, 87, 102, 0.8)) |  |
| --wui-pagination-arrow-icon-color | var(--ynfw-color-icon-arrow-pagination, #111) |  |
| --wui-pagination-color-active | var(--ynfw-color-text-pagination-selected, #fff) |  |
| --wui-pagination-pagenumber-bg-color-selected | var(--ynfw-color-bg-pagenumber-pagination-selected, #adb4bc) |  |
| --wui-pagination-pagenumber-bg-color-selected-hover | var(--ynfw-color-bg-pagenumber-pagination-selected-hover, #6A7280) |  |
| --wui-pagination-color-disabled | var(--ynfw-color-text-tertiary-global, #777) |  |
| --wui-pagination-bg-color-disabled | var(--ynfw-color-bg-pagination-arrow-disabled, transparent) |  |
| --wui-pagination-border-color-disabled | var(--ynfw-color-border-disabled, var(--wui-base-border-color-disabled)) |  |
| --wui-pagination-arrow-icon-color-disabled | var(--ynfw-color-icon-arrow-pagination-disabled, #c1c7d0) |  |
| --wui-pagination-bg-color | var(--ynfw-color-bg-pagination-arrow-default, transparent) |  |
| --wui-pagination-input-size-width | var(--ynfw-size-width-input-pagination, 60px) |  |
| --wui-pagination-input-border-width | var(--ynfw-border-width-input-pagination, 1px) |  |
| --wui-pagination-pagenumber-size-height | var(--ynfw-size-height-pagenumber-pagination, 20px) |  |
| --wui-pagination-pagenumber-size-width | var(--ynfw-size-width-pagenumber-pagination, 20px) |  |
| --wui-pagination-bg-color-hover | var(--ynfw-color-bg-pagination-arrow-hover, #edf1f7) |  |

### popconfirm

| 变量名称 | 默认值 | 描述  |
| ---- | --- | --- |
| --wui-popconfirm-color-text-title | var(--ynfw-color-text-title-popconfirm, var(--wui-base-text-color)) |  |
| --wui-popconfirm-font-size-title | var(--ynfw-font-size-title-popconfirm, 14px) |  |
| --wui-popconfirm-font-weight-title | var(--ynfw-font-weight-title-popconfirm, 600) |  |
| --wui-popconfirm-color-text-content | var(--ynfw-color-text-content-popconfirm, var(--wui-base-text-color)) |  |
| --wui-popconfirm-font-size-content | var(--ynfw-font-size-content-popconfirm, 12px) |  |
| --wui-popconfirm-font-weight-content | var(--ynfw-font-weight-content-popconfirm, 400) |  |
| --wui-popconfirm-inverse-title-text-color | var(--ynfw-color-text-inverse-title-popconfirm, #fff) |  |

### popover

| 变量名称 | 默认值 | 描述  |
| ---- | --- | --- |
| --wui-popover-color-text-title | var(--ynfw-color-text-title-popover, var(--wui-base-text-color)) |  |
| --wui-popover-font-size-title | var(--ynfw-font-size-title-popover, 16px) |  |
| --wui-popover-font-weight-title | var(--ynfw-font-weight-title-popover, 600) |  |
| --wui-popover-color-text-content | var(--ynfw-color-text-content-popover, var(--wui-base-text-color)) |  |
| --wui-popover-font-size-content | var(--ynfw-font-size-content-popover, 14px) |  |
| --wui-popover-font-weight-content | var(--ynfw-font-weight-content-popover, 400) |  |
| --wui-popconfirm-font-size-icon-info | var(--ynfw-font-size-icon-info-popconfirm, 14px) |  |
| --wui-popover-box-shadow | var(--ynfw-box-shadow-popover, 0 1px 5px rgb(224,224,224)) |  |
| --wui-popover-border-radius | var(--ynfw-border-radius-popover, 4px) |  |
| --wui-popover-color-bg | var(--ynfw-color-bg-popover, var(--wui-base-panel-bg-color)) |  |
| --wui-popover-inverse-content-text-color | var(--ynfw-color-text-inverse-content-popover, #fff) |  |
| --wui-popover-custom-color |  |  |

### radio

| 变量名称 | 默认值 | 描述  |
| ---- | --- | --- |
| --wui-radio-size-height-xs-button | var(--ynfw-size-height-xs-button-radio, 20px) |  |
| --wui-radio-size-height-lg-button | var(--ynfw-size-height-lg-button-radio, 32px) |  |
| --wui-radio-size-height-md-button | var(--ynfw-size-height-md-button-radio, 28px) |  |
| --wui-radio-color-bg-button-selected | var(--ynfw-color-bg-button-radio-selected, #FFFFFF) |  |
| --wui-radio-color-border-button-disabled | var(--ynfw-color-border-button-radio-disabled, #eee) |  |
| --wui-radio-bg-button-radio-disabled-selected | var(--ynfw-color-bg-button-radio-disabled-selected, #c1c7d0) |  |
| --wui-radio-color-bg-button-disabled | var(--ynfw-color-bg-button-radio-disabled, #f7f7f7) |  |
| --wui-radio-color-bg-fill-radio-selected | var(--ynfw-color-bg-fill-radio-selected, #EE2233) |  |
| --wui-radio-color-bg-dot-fill-selected | var(--ynfw-color-bg-dot-fill-radio-selected, #FFFFFF) |  |
| --wui-radio-color-bg-fill-radio-selected-hover | var(--ynfw-color-bg-fill-radio-selected-hover, #be1b28) |  |
| --wui-radio-color-bg-fill-selected | var(--ynfw-color-bg-fill-radio-selected, var(--wui-primary-color)) |  |
| --wui-radio-color-border-hover | var(--ynfw-color-border-radio-hover, var(--wui-input-border-color-hover)) |  |
| --wui-radio-color-bg-fill-radio-selected-disabled | var(--ynfw-color-bg-fill-radio-selected-disabled, #F79099) |  |
| --wui-radio-color-border-disabled | var(--ynfw-color-border-radio-disabled, var(--wui-input-border-color-disabled)) |  |
| --wui-radio-color-bg-disabled | var(--ynfw-color-bg-radio-disabled, var(--wui-base-bg-color-disabled)) |  |
| --wui-radio-color-text-disabled | var(--ynfw-color-text-radio-disabled, var(--wui-base-item-color-disabled)) |  |
| --wui-radio-color-border-fill-radio-disabled | var(--ynfw-color-border-fill-radio-disabled, #D1D5DB) |  |
| --wui-radio-color-bg-fill-radio-disabled | var(--ynfw-color-bg-fill-radio-disabled, #F7F7F7) |  |
| --wui-radio-font-size | var(--ynfw-font-size-radio, 12px) |  |
| --wui-radio-font-weight | var(--ynfw-font-weight-radio, 400) |  |
| --wui-radio-color-text | var(--ynfw-color-text-radio, var(--wui-base-text-color)) |  |
| --wui-radio-color-border-fill-radio | var(--ynfw-color-border-fill-radio, #D4D4D4) |  |
| --wui-radio-color-bg-fill-radio | #FFF |  |
| --wui-radio-color-border | var(--ynfw-color-border-radio, var(--wui-input-border-color)) |  |
| --wui-radio-color-bg | var(--ynfw-color-bg-radio, var(--wui-base-bg-color)) |  |
| --wui-radio-color-border-fill-radio-hover | var(--ynfw-color-border-fill-radio-hover, #505766) |  |
| --wui-radio-color-border-button-selected | var(--ynfw-color-border-button-radio-selected, var(--wui-dark-color)) |  |
| --wui-radio-bg-button-disabled |  |  |

### rate

| 变量名称 | 默认值 | 描述  |
| ---- | --- | --- |
| --wui-rate-item-font-size | var(--ynfw-font-size-item-rate, 16px) |  |
| --wui-rate-item-selected-color-bg | var(--ynfw-color-bg-item-rate-selected, #FFD400) |  |
| --wui-rate-color-text |  |  |
| --wui-rate-font-size | var(--ynfw-font-size-rate, 14px) |  |
| --wui-rate-font-weight | var(--ynfw-font-weight-rate, 400) |  |
| --wui-rate-item-border-color | var(--ynfw-color-border-item-rate, #d9d9d9) |  |

### skeleton

| 变量名称 | 默认值 | 描述  |
| ---- | --- | --- |
| --wui-skeleton-bg-color | var(--ynfw-color-bg-skeleton, rgba(190, 190, 190, 0.2)) |  |
| --wui-skeleton-bg-to-color | var(--ynfw-color-bg-skeleton-bold, rgba(129, 129, 129, 0.24)) |  |

### slider

| 变量名称 | 默认值 | 描述  |
| ---- | --- | --- |
| --wui-slider-color-text | var(--ynfw-color-text-slider, #666) |  |
| --wui-slider-color-text-disabled | var(--ynfw-color-text-slider-disabled, #999) |  |
| --wui-slider-font-size | var(--ynfw-font-size-slider, 12px) |  |
| --wui-slider-font-weight | var(--ynfw-font-weight-slider, 400) |  |
| --wui-slider-font-weight-selected | var(--ynfw-font-weight-slider-selected, 600) |  |
| --wui-slider-line-size-height | var(--ynfw-size-height-line-slider, 4px) |  |
| --wui-slider-handle-border-radius | var(--ynfw-border-radius-handle-slider, 6px) |  |
| --wui-slider-line-bg-color | var(--ynfw-color-bg-line-slider, #e9e9e9) |  |
| --wui-slider-line-finished-bg-color | var(--ynfw-color-bg-line-slider-finished, var(--wui-info-color)) |  |
| --wui-slider-handle-size-width | var(--ynfw-size-width-handle-slider, 14px) |  |
| --wui-slider-handle-size-height | var(--ynfw-size-height-handle-slider, 14px) |  |
| --wui-slider-handle-bg-color | var(--ynfw-color-bg-handle-slider, #fff) |  |
| --wui-slider-handle-borfer-color | var(--ynfw-color-border-handle-slider, var(--wui-info-color)) |  |
| --wui-slider-handle-border-width | var(--ynfw-border-width-handle-slider, 2px) |  |

### spin

| 变量名称 | 默认值 | 描述  |
| ---- | --- | --- |
| --wui-spin-backdrop-bg-color | rgba(255,255,255,0.4) |  |
| --wui-spin-color-text | var(--ynfw-color-text-spin, var(--wui-primary-color)) |  |
| --wui-spin-font-size | var(--ynfw-font-size-spin, 12px) |  |
| --wui-spin-size-width | var(--ynfw-size-width-spin, 32px) |  |
| --wui-spin-size-height | var(--ynfw-size-height-spin, 32px) |  |
| --wui-spin-icon-color | var(--ynfw-color-icon-spin, var(--wui-primary-color)) |  |

### steps

| 变量名称 | 默认值 | 描述  |
| ---- | --- | --- |
| --wui-steps-font-size | var(--ynfw-font-size-steps, 12px) |  |
| --wui-steps-color-text | var(--ynfw-color-text-steps, var(--wui-base-text-color)) |  |
| --wui-steps-font-weight | var(--ynfw-font-weight-steps, 400) |  |
| --wui-steps-icon-font-size | var(--ynfw-font-size-icon-steps, 14px) |  |
| --wui-steps-icon-font-weight | var(--ynfw-font-weight-icon-default-steps, 400) |  |
| --wui-steps-line-default-border-width | var(--ynfw-border-width-line-default-steps, 1px) |  |
| --wui-steps-line-default-border-color | var(--ynfw-color-border-line-default-steps, #e8e8e8) |  |
| --wui-steps-number-waited-line-border-color | var(--ynfw-color-border-number-steps-waited, #d8d8d8) |  |
| --wui-steps-default-waited-icon-color | var(--ynfw-color-icon-default-steps-waited, #dfe1e6) |  |
| --wui-steps-dot-waited-icon-color | var(--ynfw-color-icon-dot-steps-waited, #bfbfbf) |  |
| --wui-steps-dot-finished-icon-color | var(--ynfw-color-icon-dot-steps-finished, var(--wui-primary-color)) |  |
| --wui-steps-font-weight-selected | var(--ynfw-font-weight-steps-selected, 500) |  |
| --wui-steps-default-finished-icon-color | var(--ynfw-color-icon-default-steps-finished, var(--wui-success-color)) |  |
| --wui-steps-default-ing-icon-color | var(--ynfw-color-icon-default-steps-ing, var(--wui-info-color)) |  |
| --wui-steps-color-text-disabled | var(--ynfw-color-text-steps-disabled, var(--wui-base-text-color-disabled)) |  |
| --wui-steps-default-danger-icon-color | var(--ynfw-color-icon-default-steps-danger, var(--wui-danger-color)) |  |
| --wui-steps-dot-line-finished-border-color | var(--ynfw-color-border-line-dot-steps-finished, #a5adba) |  |
| --wui-steps-dot-line-border-width | var(--ynfw-border-width-line-dot-steps, 3px) |  |
| --wui-steps-dot-item-size-width | var(--ynfw-size-width-item-dot-steps, 8px) |  |
| --wui-steps-dot-item-size-height | var(--ynfw-size-height-item-dot-steps, 8px) |  |
| --wui-steps-dot-item-size-width-focus | var(--ynfw-size-width-item-dot-steps-focus, 10px) |  |
| --wui-steps-dot-item-size-height-focus | var(--ynfw-size-height-item-dot-steps-focus, 10px) |  |
| --wui-steps-more-icon-font-size | var(--ynfw-font-size-icon-more-nav, 14px) |  |
| --wui-steps-more-icon-color | var(--ynfw-color-icon-more-nav, rgba(80, 87, 102, 0.65)) |  |
| --wui-steps-more-icon-color-hover | var(--ynfw-color-icon-more-nav-hover, #505766) |  |
| --wui-steps-number-item-size-width | var(--ynfw-size-width-item-number-steps, 30px) |  |
| --wui-steps-number-item-size-height | var(--ynfw-size-height-item-number-steps, 30px) |  |
| --wui-steps-number-finished-item-border-radius | var(--ynfw-border-radius-item-number-steps-finished, 50%) |  |
| --wui-steps-number-waited-item-bg-color | var(--ynfw-color-bg-number-steps-waited, #EEE) |  |
| --wui-steps-color-text-tertiary | var(--ynfw-color-text-tertiary-steps, #666) |  |
| --wui-steps-number-waited-text-color | var(--ynfw-color-text-number-steps-waited, #999) |  |
| --wui-steps-number-font-size | var(--ynfw-font-size-number-steps, 16px) |  |
| --wui-steps-number-ing-item-bg-color | var(--ynfw-color-bg-number-steps-ing, var(--wui-primary-color)) |  |
| --wui-steps-number-ing-text-color | var(--ynfw-color-text-number-steps-ing, #FFF) |  |
| --wui-steps-number-finished-line-border-color | var(--ynfw-color-border-line-number-steps-finished, var(--wui-primary-color)) |  |
| --wui-steps-number-finished-item-bg-color | var(--ynfw-color-bg-number-steps-finished, #FFF) |  |
| --wui-steps-number-finished-item-border-width | var(--ynfw-border-width-item-number-steps-finished, 1px) |  |
| --wui-steps-number-finished-item-border-style | var(--ynfw-border-style-item-number-steps-finished, solid) |  |
| --wui-steps-number-finished-item-border-color | var(--ynfw-color-border-item-number-steps-finished, var(--wui-primary-color)) |  |
| --wui-steps-number-finished-text-color | var(--ynfw-color-text-number-steps-finished, var(--wui-primary-color)) |  |
| --wui-steps-arrow-item-waited-text-color | var(--ynfw-color-text-item-arrow-steps-waited, #111) |  |
| --wui-steps-arrow-waited-bg-color | var(--ynfw-color-bg-arrow-steps-waited, #f4f4f4) |  |
| --wui-steps-arrow-waited-bg-color-hover | var(--ynfw-color-bg-arrow-steps-waited-hover, #ddd) |  |
| --wui-steps-arrow-item-size-width | var(--ynfw-size-width-item-arrow-steps, 18px) |  |
| --wui-steps-arrow-item-size-height | var(--ynfw-size-height-item-arrow-steps, 18px) |  |
| --wui-steps-arrow-item-border-radius | var(--ynfw-border-radius-item-arrow-steps, 50%) |  |
| --wui-steps-arrow-item-bg-color | var(--ynfw-color-bg-item-arrow-steps, #fff) |  |
| --wui-steps-arrow-item-font-size | var(--ynfw-font-size-item-arrow-steps, 14px) |  |
| --wui-steps-title-font-size | var(--ynfw-font-size-title-steps, 14px) |  |
| --wui-steps-arrow-finished-bg-color | var(--ynfw-color-bg-arrow-steps-finished, #e7f8f2) |  |
| --wui-steps-arrow-finished-bg-color-hover | var(--ynfw-color-bg-arrow-steps-finished-hover, #ace5cd) |  |
| --wui-steps-arrow-item-finished-text-color | var(--ynfw-color-text-item-arrow-steps-finished, #18b681) |  |
| --wui-steps-arrow-warning-bg | var(--ynfw-color-bg-arrow-steps-warning, #fff9f0) |  |
| --wui-steps-arrow-warning-bg-hover | var(--ynfw-color-bg-arrow-steps-warning-hover, #ffecc6) |  |
| --wui-steps-arrow-item-warning-text-color | var(--ynfw-color-text-item-arrow-steps-warning, #ffa600) |  |
| --wui-steps-arrow-ing-bg-color | var(--ynfw-color-bg-arrow-steps-ing, #77a1ee) |  |
| --wui-steps-arrow-ing-bg-color-hover | var(--ynfw-color-bg-arrow-steps-ing-hover, #0754e2) |  |

### switch

| 变量名称 | 默认值 | 描述  |
| ---- | --- | --- |
| --wui-switch-border-radius | var(--ynfw-border-radius-switch, 7px) |  |
| --wui-switch-default-bg-color | var(--ynfw-color-bg-switch-default, linear-gradient(90deg, #858A94 0%, #B9BCC2 100%)) |  |
| --wui-switch-handle-bg-color | var(--ynfw-color-bg-handle-switch, #FFF) |  |
| --wui-switch-actived-bg-color | var(--ynfw-color-bg-switch-actived, var(--wui-primary-color)) |  |
| --wui-switch-back-bg-color-disabled | var(--ynfw-color-bg-switch-disabled, #D9D9D9) |  |
| --wui-switch-size-width | var(--ynfw-size-width-switch, 32px) |  |
| --wui-switch-size-height | var(--ynfw-size-height-switch, 14px) |  |
| --wui-switch-handle-height | var(--ynfw-size-height-handle-switch, 14px) |  |
| --wui-switch-handle-box-shadow | var(--ynfw-box-shadow-handle-switch, 0px 1px 4px 0px rgba(80, 87, 102, 0.3)) |  |
| --wui-switch-color-text | var(--ynfw-color-text-switch, #FFF) |  |
| --wui-switch-font-size | var(--ynfw-font-size-switch, 14px) |  |
| --wui-switch-font-weight | var(--ynfw-font-weight-switch, 400) |  |

### table

| 变量名称 | 默认值 | 描述  |
| ---- | --- | --- |
| --wui-table-body-font-size | var(--ynfw-font-size-cell-table, 12px) |  |
| --wui-table-border-top-width | var(--ynfw-border-width-top-table, 1px) |  |
| --wui-table-border-top-color | var(--ynfw-color-border-top-table, #505766) |  |
| --wui-table-border-width | var(--ynfw-border-width-table, 1px) |  |
| --wui-table-border-color | var(--ynfw-color-border-cell-table-default, #dbe0e5) |  |
| --wui-table-striped-color | var(--ynfw-color-bg-striped-table, #f7f7f7) |  |
| --wui-table-bg-find | var(--ynfw-color-bg-row-table-find, #FDF3E1) |  |
| --wui-table-bg-find-select | var(--ynfw-color-bg-row-table-find-selected, #FFECC6) |  |
| --wui-table-bg-total | var(--ynfw-color-bg-subtotal-table, #FFFBF3) |  |
| --wui-table-font-size-total | var(--ynfw-font-size-total-table, 13PX) |  |
| --wui-table-font-weight-total | var(--ynfw-font-weight-total-table, 400) |  |
| --wui-table-head-bg-color | var(--ynfw-color-bg-header-table, #eff1f6) |  |
| --wui-table-header-font-weight | var(--ynfw-font-weight-header-table, 600) |  |
| --wui-table-header-font-size | var(--ynfw-font-size-header-table, 13px) |  |
| --wui-table-header-icon-font-size | var(--ynfw-font-size-icon-header-table, 16px) |  |
| --wui-table-body-font-weight | var(--ynfw-font-weight-cell-table, 400) |  |
| --wui-table-select-background-color | var(--ynfw-color-bg-table-click, #F0F0F0) |  |
| --wui-table-select-border-width | var(--ynfw-border-width-table-click, 1px) |  |
| --wui-table-select-border-color | var(--ynfw-color-border-table-click, #0033CC) |  |
| --wui-table-expanded-row-bg-color-hover | var(--ynfw-color-bg-row-table-expanded-hover, #fff) |  |

### tabs

| 变量名称 | 默认值 | 描述  |
| ---- | --- | --- |
| --wui-tabs-color-text-trangle | var(--ynfw-color-text-trangle-tabs, #333) |  |
| --wui-tabs-font-size-trangle | var(--ynfw-font-size-trangle-tabs, 12px) |  |
| --wui-tabs-font-weight-trangle | var(--ynfw-font-weight-trangle-tabs, 600) |  |
| --wui-tabs-color-text-trangle-hover | var(--ynfw-color-text-trangle-tabs-hover, var(--wui-primary-color)) |  |
| --wui-tabs-color-text-trangle-selected | var(--ynfw-color-text-trangle-tabs-selected, var(--wui-primary-color)) |  |
| --wui-tabs-font-weight-trangle-selected | var(--ynfw-font-weight-trangle-tabs-selected, 600) |  |
| --wui-tabs-color-icon-tabs | var(--ynfw-color-icon-tabs, #9ca3af) |  |
| --wui-tabs-color-icon-tabs-hover | var(--ynfw-color-icon-tabs-hover, #4b5563) |  |
| --wui-tabs-trangle-border-color | var(--ynfw-color-border-down-trangle-tabs, #505766) |  |
| --wui-tabs-trangle-border-width | var(--ynfw-border-width-down-trangle-tabs, 1px) |  |
| --wui-tabs-font-size-line | var(--ynfw-font-size-line-tabs, 12px) |  |
| --wui-tabs-font-weight-line | var(--ynfw-font-weight-line-tabs, 400) |  |
| --wui-tabs-line-color-default | var(--ynfw-color-text-line-tabs, #666) |  |
| --wui-tabs-font-weight-line-selected | var(--ynfw-font-weight-line-tabs-selected, 600) |  |
| --wui-tabs-line-color-active | var(--ynfw-color-text-line-tabs-selected, #111) |  |
| --wui-tabs-line-bg-color-hover | var(--ynfw-color-bg-tabs-linemode-hover, #f4f4f4) |  |
| --wui-tabs-color-bg-primary | var(--ynfw-color-bg-primary-tabs, #f5f5f5) |  |
| --wui-tabs-color-bg-primary-unselected | var(--ynfw-color-bg-primary-tabs-unselected, #fff) |  |
| --wui-tabs-border-radius-item-primary | var(--ynfw-border-radius-item-primary-tabs, 0) |  |
| --wui-tabs-color-bg-primary-selected | var(--ynfw-color-bg-primary-tabs-selected, var(--wui-primary-color)) |  |
| --wui-tabs-color-text-line-hover | var(--ynfw-color-text-line-tabs-hover, var(--wui-primary-color)) |  |
| --wui-tabs-card-nav-bg-color | var(--ynfw-color-bg-card-tabs, #f7f9fd) |  |
| --wui-tabs-card-border-color | var(--ynfw-color-border-down-card-tabs, #e4e4e4) |  |
| --wui-tabs-color | var(--ynfw-color-text-tabs, #505766) |  |
| --wui-tabs-font-size-card | var(--ynfw-font-size-card-tabs, 12px) |  |
| --wui-tabs-font-weight-card | var(--ynfw-font-weight-card-tabs, 600) |  |
| --wui-tabs-color-text-card-selected | var(--ynfw-color-text-card-tabs-selected, var(--wui-tabs-color)) |  |
| --wui-tabs-font-weight-card-selected | var(--ynfw-font-weight-card-tabs-selected, 600) |  |
| --wui-tabs-border-width-leftright-card | var(--ynfw-border-width-leftright-card-tabs, 1px) |  |
| --wui-tabs-color-border-leftright-card | var(--ynfw-color-border-leftright-card-tabs, #e4e4e4) |  |
| --wui-tabs-color-text-card-hover | var(--ynfw-color-text-card-tabs-hover, var(--wui-primary-color)) |  |
| --wui-tabs-card-bg-color-hover | var(--ynfw-color-bg-card-tabs-hover, #eceff4) |  |
| --wui-tabs-card-bg-color-active | var(--ynfw-color-bg-card-tabs-selected, #FFF) |  |
| --wui-tabs-card-border-width-active | var(--ynfw-border-width-top-card-tabs-selected, 1px) |  |
| --wui-tabs-card-border-color-active | var(--ynfw-color-border-top-card-tabs-selected, #505766) |  |
| --wui-tabs-color-bg-trapezoid | var(--ynfw-color-bg-trapezoid-tabs, #f5f5f5) |  |
| --wui-tabs-color-text-trapezoid | var(--ynfw-color-text-trapezoid-tabs, #111827) |  |
| --wui-tabs-font-size-trapezoid | var(--ynfw-font-size-trapezoid-tabs, 12px) |  |
| --wui-tabs-font-weight-trapezoid | var(--ynfw-font-weight-trapezoid-tabs, 600) |  |
| --wui-tabs-color-border-card-tabs | var(--ynfw-color-border-card-tabs, #e5e7eb) |  |
| --wui-tabs-border-width-card-tabs | var(--ynfw-border-width-card-tabs, 1px) |  |
| --wui-tabs-color-bg-trapezoid-tabs-hover | var(--ynfw-color-bg-trapezoid-tabs-hover, #dbeafe) |  |
| --wui-tabs-color-text-trapezoid-hover | var(--ynfw-color-text-trapezoid-tabs-hover, #374151) |  |
| --wui-tabs-font-weight-trapezoid-selected | var(--ynfw-font-weight-trapezoid-tabs-selected, 600) |  |
| --wui-tabs-color-text-trapezoid-selected | var(--ynfw-color-text-trapezoid-tabs-selected, #4b5563) |  |
| --wui-tabs-color-bg-trapezoid-tabs-selected | var(--ynfw-color-bg-trapezoid-tabs-selected, #fff) |  |
| --wui-tabs-border-radius-fill | var(--ynfw-border-radius-fill-tabs, 8px) |  |
| --wui-tabs-color-text-fill-line-tabs | var(--ynfw-color-text-fill-line-tabs, #374145) |  |
| --wui-tabs-font-size-fill-line | var(--ynfw-font-size-fill-line-tabs, 12px) |  |
| --wui-tabs-font-weight-fill-line-tabs | var(--ynfw-font-weight-fill-line-tabs, 600) |  |
| --wui-tabs-color-bg-fill-line-tabs-hover | var(--ynfw-color-bg-fill-line-tabs-hover, #dbeafe) |  |
| --wui-tabs-color-text-fill-line-tabs-hover | var(--ynfw-color-text-fill-line-tabs-hover, #374151) |  |
| --wui-tabs-font-weight-fill-line-tabs-selected | var(--ynfw-font-weight-fill-line-tabs-selected, 600) |  |
| --wui-tabs-color-text-fill-line-tabs-selected | var(--ynfw-color-text-fill-line-tabs-selected, #111827) |  |
| --wui-tabs-color-bg-fill-line-tabs-selected | var(--ynfw-color-bg-fill-line-tabs-selected, #fff) |  |
| --wui-tabs-color-bg-fill-line-tabs | var(--ynfw-color-bg-fill-line-tabs, #eff6ff) |  |
| --wui-tabs-border-width-down-fill | var(--ynfw-border-width-down-fill-tabs, 1px) |  |
| --wui-tabs-border-style-fill | var(--ynfw-border-style-fill-tabs, solid) |  |
| --wui-tabs-color-border-down-fill | var(--ynfw-color-border-down-fill-tabs, #f0f0f0) |  |
| --wui-tabs-color-bg-fill | var(--ynfw-color-bg-fill-tabs, #FFF) |  |
| --wui-tabs-color-text-fill | var(--ynfw-color-text-fill-tabs, #666) |  |
| --wui-tabs-font-size-fill | var(--ynfw-font-size-fill-tabs, 12px) |  |
| --wui-tabs-font-weight-fill | var(--ynfw-font-weight-fill-tabs, 600) |  |
| --wui-tabs-color-text-fill-hover | var(--ynfw-color-text-fill-tabs-hover, var(--wui-primary-color)) |  |
| --wui-tabs-color-bg-fill-selected | var(--ynfw-color-bg-fill-tabs-selected, var(--wui-primary-color)) |  |
| --wui-tabs-font-weight-fill-selected | var(--ynfw-font-weight-fill-tabs-selected, 600) |  |
| --wui-tabs-color-text-fill-selected | var(--ynfw-color-text-fill-tabs-selected, #fff) |  |
| --wui-tabs-overflow-btn-color | var(--ynfw-color-text-tabs-overflow-btn, #505766) |  |
| --wui-tabs-editable-border-color | var(--ynfw-color-border-editablecard-tabs, #e9e9e9) |  |
| --wui-tabs-color-text-editablecard | var(--ynfw-color-text-editablecard-tabs, #666) |  |
| --wui-tabs-font-size-editablecard | var(--ynfw-font-size-editablecard-tabs, 12px) |  |
| --wui-tabs-font-weight-editablecard | var(--ynfw-font-weight-editablecard-tabs, 400) |  |
| --wui-tabs-editable-bg-color | var(--ynfw-color-bg-editablecard-tabs, #f5f5f5) |  |
| --wui-tabs-editable-size-icon | var(--ynfw-font-size-icon-tabs, 12px) |  |
| --wui-tabs-editable-color-icon | var(--ynfw-color-icon-tabs, #969aa3) |  |
| --wui-tabs-color-text-editablecard-hover | var(--ynfw-color-text-editablecard-tabs-hover, var(--wui-primary-color)) |  |
| --wui-tabs-color-text-editablecard-selected | var(--ynfw-color-text-editablecard-tabs-selected, var(--wui-primary-color)) |  |
| --wui-tabs-font-weight-editablecard-selected | var(--ynfw-font-weight-editablecard-tabs-selected, 600) |  |
| --wui-tabs-editable-border-color-selected | var(--ynfw-color-border-editablecard-tabs-selected, #e9e9e9) |  |
| --wui-tabs-editable-bg-color-selected | var(--ynfw-color-bg-editablecard-tabs-selected, #fff) |  |
| --wui-tabs-editable-color-icon-selected | var(--ynfw-color-icon-tabs-hover, #505766) |  |
| --wui-tabs-color-bg-fade | var(--ynfw-color-bg-fade-tabs, #e4e7eb) |  |
| --wui-tabs-border-radius-fade | var(--ynfw-border-radius-fade-tabs, 4px) |  |
| --wui-tabs-fade-color | var(--ynfw-color-text-fade-tabs, var(--wui-tabs-color-text-fade)) |  |
| --wui-tabs-fade-font-weight | var(--ynfw-font-weight-fade-tabs, 400) |  |
| --wui-tabs-font-size-fade | var(--ynfw-font-size-fade-tabs, 12px) |  |
| --wui-tabs-size-height-item-fade | var(--ynfw-size-height-item-fade-tabs, 30px) |  |
| --wui-tabs-color-bg-fade-selected | var(--ynfw-color-bg-fade-tabs-selected, #FFF) |  |
| --wui-tabs-color-text-fade-selected | var(--ynfw-color-text-fade-tabs-selected, #666) |  |
| --wui-tabs-fade-font-weight-selected | var(--ynfw-font-weight-fade-tabs-selected, 600) |  |
| --wui-tabs-border-radius-fade-selected | var(--ynfw-border-radius-fade-tabs-selected, 2px) |  |
| --wui-tabs-color-text-fade-hover | var(--ynfw-color-text-fade-tabs-hover, var(--wui-primary-color)) |  |
| --wui-tabs-font-weight-tabs-more | var(--ynfw-font-weight-tabs, 600) |  |
| --wui-tabs-color-border-underline-line | var(--ynfw-color-border-underline-line-tabs, var(--wui-primary-color)) |  |

### tag

| 变量名称 | 默认值 | 描述  |
| ---- | --- | --- |
| --wui-tag-info-bg | var(--ynfw-color-bg-info-tag, #EFF6FF) |  |
| --wui-tag-warning-bg | var(--ynfw-color-bg-warning-tag, #FFFBEB) |  |
| --wui-tag-success-bg | var(--ynfw-color-bg-success-tag, #ECFDF5) |  |
| --wui-tag-danger-bg | var(--ynfw-color-bg-danger-tag, #FFF1F2) |  |
| --wui-tag-invalid-bg | var(--ynfw-color-bg-invalid-tag, #F3F4F6) |  |
| --wui-tag-start-bg | var(--ynfw-color-bg-start-tag, #F0F9FF) |  |
| --wui-tag-light-bg | var(--ynfw-color-bg-tag, #F3F4F6) |  |
| --wui-tag-dark-bg | var(--ynfw-color-bg-tag-dark, #4B5563) |  |
| --wui-tag-info-border | var(--ynfw-color-border-info-tag, #DBEAFE) |  |
| --wui-tag-warning-border | var(--ynfw-color-border-warning-tag, #FEF3C7) |  |
| --wui-tag-success-border | var(--ynfw-color-border-success-tag, #D1FAE5) |  |
| --wui-tag-danger-border | var(--ynfw-color-border-danger-tag, #FEE2E2) |  |
| --wui-tag-invalid-border | var(--ynfw-color-border-invalid-tag, #E5E7EB) |  |
| --wui-tag-start-border | var(--ynfw-color-border-start-tag, #BAE6FD) |  |
| --wui-tag-light-border | var(--ynfw-color-border-tag, transparent) |  |
| --wui-tag-dark-border | var(--ynfw-color-border-tag-dark, transparent) |  |
| --wui-tag-info-text | var(--ynfw-color-text-info-tag, #3B82F6) |  |
| --wui-tag-warning-text | var(--ynfw-color-text-warning-tag, #F59E0B) |  |
| --wui-tag-success-text | var(--ynfw-color-text-success-tag, #10B981) |  |
| --wui-tag-danger-text | var(--ynfw-color-text-danger-tag, #EF4444) |  |
| --wui-tag-invalid-text | var(--ynfw-color-text-invalid-tag, #4B5563) |  |
| --wui-tag-start-text | var(--ynfw-color-text-start-tag, #0EA5E9) |  |
| --wui-tag-dark-text | var(--ynfw-color-text-tag-dark, #FFF) |  |
| --wui-tag-font-weight | var(--ynfw-font-weight-semantic-tag, 600) |  |
| --wui-tag-color-text | var(--ynfw-color-text-tag, var(--wui-dark-color)) |  |
| --wui-tag-color-text-disabled | var(--ynfw-color-text-tag-disabled, #999) |  |
| --wui-tag-color-text-dark | var(--ynfw-color-text-tag-dark, #FFF) |  |
| --wui-tag-font-size | var(--ynfw-font-size-tag, 12px) |  |
| --wui-tag-font-size-icon | var(--ynfw-font-size-icon-tag, 12px) |  |

### timeline

| 变量名称 | 默认值 | 描述  |
| ---- | --- | --- |
| --wui-timeline-line-border-width | var(--ynfw-border-width-line-timeline, 2px) |  |
| --wui-timeline-line-border-style | var(--ynfw-border-style-line-timeline, solid) |  |
| --wui-timeline-line-border-color | var(--ynfw-color-border-line-timeline, #e9e9e9) |  |
| --wui-timeline-item-width | var(--ynfw-size-width-item-timeline, 12px) |  |
| --wui-timeline-item-height | var(--ynfw-size-height-item-timeline, 12px) |  |
| --wui-timeline-item-bg-color | var(--ynfw-color-bg-item-timeline, #fff) |  |
| --wui-timeline-item-border-radius | var(--ynfw-border-radius-item-timeline, 100px) |  |
| --wui-timeline-item-border-width | var(--ynfw-border-width-item-timeline, 2px) |  |
| --wui-timeline-font-size-content | var(--ynfw-font-size-content-timeline, 12px) |  |
| --wui-timeline-font-weight-content | var(--ynfw-font-weight-content-timeline,400) |  |
| --wui-timeline-color-text-content | var(--ynfw-color-text-content-timeline, var(--wui-base-text-color)) |  |
| --wui-timeline-color-text-time | var(--ynfw-color-text-time-timeline, #999) |  |
| --wui-timeline-font-size-time | var(--ynfw-font-size-time-timeline, 12px) |  |
| --wui-timeline-font-weight-time | var(--ynfw-font-weight-time-timeline, 400) |  |

### timepicker

| 变量名称 | 默认值 | 描述  |
| ---- | --- | --- |
| --wui-time-picker-color-text | var(--ynfw-color-text-timepicker, var(--wui-base-text-color)) |  |
| --wui-time-picker-color-text-disabled | var(--ynfw-color-text-timepicker-disabled, var(--wui-input-color-disabled)) |  |
| --wui-time-picker-font-size | var(--ynfw-font-size-timepicker, 12px) |  |
| --wui-time-picker-font-weight | var(--ynfw-font-weight-timepicker, var(--wui-base-input-font-weight)) |  |
| --wui-picker-color-bg-cell | var(--ynfw-color-bg-cell-picker, var(--wui-base-panel-bg-color)) |  |
| --wui-time-picker-color-bg-cell-hover | var(--ynfw-color-bg-cell-timepicker-hover, #FFF) |  |
| --wui-time-picker-color-bg-cell-selected | var(--ynfw-color-bg-cell-timepicker-selected, var(--wui-picker-cell-bg-color-selected)) |  |
| --wui-time-picker-size-width-cell | var(--ynfw-size-width-cell-timepicker, 48px) |  |
| --wui-time-picker-size-height-cell | var(--ynfw-size-height-cell-timepicker, 24px) |  |
| --wui-time-picker-border-radius-cell | var(--ynfw-border-radius-cell-timepicker, 4px) |  |
| --wui-time-picker-border-width-rightborder-panel | var(--ynfw-border-width-rightborder-panel-timepicker, 0) |  |

### transfer

| 变量名称 | 默认值 | 描述  |
| ---- | --- | --- |
| --wui-transfer-border-width | var(--ynfw-border-width-transfer, 1px) |  |
| --wui-transfer-color-border | var(--ynfw-color-border-transfer, var(--wui-input-border-color)) |  |
| --wui-transfer-border-radius | var(--ynfw-border-radius-transfer, 4px) |  |
| --wui-transfer-color-bg | var(--ynfw-color-bg-transfer, var(--wui-base-bg-color)) |  |
| --wui-transfer-color-text-header | var(--ynfw-color-text-header-transfer, var(--wui-base-text-color)) |  |
| --wui-transfer-font-size-header | var(--ynfw-font-size-header-transfer, 12px) |  |
| --wui-transfer-font-weight-header | var(--ynfw-font-weight-header-transfer, 400) |  |
| --wui-transfer-font-size-content | var(--ynfw-font-size-content-transfer, 12) |  |
| --wui-transfer-font-weight-content | var(--ynfw-font-weight-content-transfer, 400) |  |
| --wui-transfer-color-text-content | var(--ynfw-color-text-content-transfer, var(--wui-base-text-color)) |  |
| --wui-transfer-color-text-content-disabled | var(--ynfw-color-text-content-transfer-disabled, var(--wui-base-item-color-disabled)) |  |
| --wui-transfer-size-width-icon | var(--ynfw-size-width-icon-transfer, 28px) |  |
| --wui-transfer-size-height-icon | var(--ynfw-size-height-icon-transfer, 34px) |  |
| --wui-transfer-color-bg-icon | var(--ynfw-color-bg-icon-transfer, #edf1f7) |  |
| --wui-transfer-color-icon | var(--ynfw-color-icon-transfer, var(--wui-dark-color)) |  |
| --wui-transfer-border-radius-bg-icon | var(--ynfw-border-radius-bg-icon-transfer, 4px) |  |
| --wui-transfer-color-bg-icon-disabled | var(--ynfw-color-bg-icon-transfer-disabled, #f7f7f7) |  |
| --wui-transfer-color-icon-disabled | var(--ynfw-color-icon-transfer-disabled, var(--wui-base-text-color-disabled)) |  |
| --wui-transfer-color-bg-icon-hover | var(--ynfw-color-bg-icon-transfer-hover, #dbe0e5) |  |
| --wui-transfer-font-size-icon | var(--ynfw-font-size-icon-transfer, 12px) |  |

### tree

| 变量名称 | 默认值 | 描述  |
| ---- | --- | --- |
| --wui-tree-color-icon | var(--ynfw-color-icon-tree, var(--wui-base-text-color)) |  |
| --wui-tree-font-size-icon | var(--ynfw-font-size-icon-tree, 16px) |  |
| --wui-color-icon-global-normal | var(--ynfw-color-icon-collapse-tree, #D1D5DB) |  |

### treeselect

| 变量名称 | 默认值 | 描述  |
| ---- | --- | --- |
| --ynfw-color-primary |  |  |
| --ynfw-color-primary-hover |  |  |
| --ynfw-color-primary-pressed |  |  |
| --ynfw-color-primary-light |  |  |
| --ynfw-color-bg-secondary |  |  |
| --ynfw-color-bg-secondary-hover |  |  |
| --ynfw-color-bg-secondary-pressed |  |  |
| --ynfw-color-success |  |  |
| --ynfw-color-info |  |  |
| --ynfw-color-info-hover |  |  |
| --ynfw-color-warning |  |  |
| --ynfw-color-danger |  |  |
| --ynfw-color-dark |  |  |
| --ynfw-color-dark-hover |  |  |
| --ynfw-color-dark-pressed |  |  |
| --ynfw-color-text-option-panel |  |  |
| --ynfw-color-text-option-panel-disabled |  |  |
| --ynfw-color-border-default |  |  |
| --ynfw-color-border-disabled |  |  |
| --ynfw-color-bg-global-default |  |  |
| --ynfw-color-bg-global-disabled |  |  |
| --ynfw-color-bg-panel |  |  |
| --ynfw-color-bg-global-hover |  |  |
| --ynfw-color-bg-global-selected |  |  |
| --ynfw-color-bg-global-selected-hover |  |  |
| --ynfw-color-icon-input-suffix |  |  |
| --ynfw-color-icon-input-suffix-hover |  |  |
| --ynfw-color-text-primary-global |  |  |
| --ynfw-color-text-disabled |  |  |
| --ynfw-color-bg-input |  |  |
| --ynfw-color-bg-input-required |  |  |
| --ynfw-color-bg-global-readonly |  |  |
| --ynfw-color-border-input-required |  |  |
| --ynfw-color-border-input |  |  |
| --ynfw-color-border-input-hover |  |  |
| --ynfw-color-border-focused |  |  |
| --ynfw-color-border-input-disabled |  |  |
| --ynfw-color-text-input-placeholder |  |  |
| --ynfw-font-size-input |  |  |
| --ynfw-color-icon-input-suffix-disabled |  |  |
| --ynfw-border-width-input |  |  |
| --ynfw-border-style-input |  |  |
| --ynfw-border-radius-input |  |  |
| --ynfw-color-cursor |  |  |
| --ynfw-font-weight-input |  |  |
| --ynfw-font-line-height-input |  |  |
| --ynfw-color-icon-input-suffix-pressed |  |  |
| --ynfw-color-bg-icon-input-hover |  |  |
| --ynfw-size-height-row-table |  |  |
| --ynfw-size-height-header-table |  |  |
| --ynfw-color-bg-info-tag |  |  |
| --ynfw-color-bg-warning-tag |  |  |
| --ynfw-color-bg-success-tag |  |  |
| --ynfw-color-bg-danger-tag |  |  |
| --ynfw-color-bg-invalid-tag |  |  |
| --ynfw-color-bg-start-tag |  |  |
| --ynfw-color-bg-tag |  |  |
| --ynfw-color-bg-tag-dark |  |  |
| --ynfw-color-border-info-tag |  |  |
| --ynfw-color-border-warning-tag |  |  |
| --ynfw-color-border-success-tag |  |  |
| --ynfw-color-border-danger-tag |  |  |
| --ynfw-color-border-invalid-tag |  |  |
| --ynfw-color-border-start-tag |  |  |
| --ynfw-color-border-tag |  |  |
| --ynfw-color-border-tag-dark |  |  |
| --ynfw-color-text-info-tag |  |  |
| --ynfw-color-text-warning-tag |  |  |
| --ynfw-color-text-success-tag |  |  |
| --ynfw-color-text-danger-tag |  |  |
| --ynfw-color-text-invalid-tag |  |  |
| --ynfw-color-text-start-tag |  |  |
| --ynfw-color-text-tag-dark |  |  |
| --ynfw-font-weight-semantic-tag |  |  |
| --ynfw-color-bg-scrollbg-scrollbar |  |  |
| --ynfw-size-width-bg-scrollbar |  |  |
| --ynfw-color-border-scrollbar |  |  |
| --ynfw-color-bg-scroll-scrollbar |  |  |
| --ynfw-size-width-scroll-scrollbar |  |  |
| --ynfw-color-bg-scroll-scrollbar-hover |  |  |
| --ynfw-size-width-scroll-scrollbar-hover |  |  |
| --ynfw-font-size-value-form |  |  |
| --ynfw-font-weight-value-form |  |  |
| --ynfw-color-border-value-form |  |  |
| --ynfw-color-bg-form |  |  |
| --ynfw-color-text-value-form |  |  |
| --ynfw-font-size-icon-input |  |  |
| --ynfw-size-height-input |  |  |
| --ynfw-color-bg-item-multiple-select |  |  |
| --ynfw-color-border-item-multiple-select |  |  |

### upload

| 变量名称 | 默认值 | 描述  |
| ---- | --- | --- |
| --wui-upload-font-size | var(--ynfw-font-size-upload, 14px) |  |
| --wui-upload-font-weight | var(--ynfw-font-weight-upload, 400) |  |
| --wui-upload-color-text | var(--ynfw-color-text-upload, #111) |  |
| --wui-upload-font-size-hint | var(--ynfw-font-size-hint-upload, 12px) |  |
| --wui-upload-font-weight-hint | var(--ynfw-font-weight-hint-upload, 400) |  |
| --wui-upload-color-text-hint | var(--ynfw-color-text-hint-upload, #666) |  |

## 定制方式


原理上是使用css变量定义的方式对全局变量或组件变量重新定义，用户可使用以下方式进行主题颜色定制


使用:root对变量进行自定义

```css
:root{
--wui-base-bg-color: #fff;
--wui-base-text-color: rgb(190, 27, 28);
--wui-base-border-color: rgb(190, 27, 28);
}
```
