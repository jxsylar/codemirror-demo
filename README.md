# codemirror-demo
这是一个codemirror的简单使用测试(python编辑器)

参考资料:  
codemirror 官网: https://codemirror.net/  
vue-codemirror: https://www.diycode.cc/projects/surmon-china/vue-codemirror  
TAB转space: https://wxaxiaoyao.cn/article/53 / https://blog.csdn.net/weixin_30381317/article/details/99079277  

```
{ // 此对象为 codemirror 配置选项对象, 下面仅对选项的快捷键相关部分做说明
    extraKeys: {
        Tab: (cm) => {
            if (cm.somethingSelected()) {      // 存在文本选择
                cm.indentSelection('add');    // 正向缩进文本
            } else {                    // 无文本选择  
                //cm.indentLine(cm.getCursor().line, "add");  // 整行缩进 不符合预期
                cm.replaceSelection(Array(cm.getOption("indentUnit") + 1).join(" "), "end", "+input");  // 光标处插入 indentUnit 个空格
            }   
        },  
        "Shift-Tab": (cm) => {              // 反向缩进   
            if (cm.somethingSelected()) {
                cm.indentSelection('subtract');  // 反向缩进
            } else {
                // cm.indentLine(cm.getCursor().line, "subtract");  // 直接缩进整行
                const cursor = cm.getCursor();
                cm.setCursor({line: cursor.line, ch: cursor.ch - 4});  // 光标回退 indexUnit 字符
            }   
            return ;
        },  
    }
}
```

```
extraKeys: {
  Tab: (cm) => {
    var spaces = Array(cm.getOption("indentUnit") + 1).join(" ");
    if (cm.somethingSelected()) {
      cm.indentSelection('add');
    } else { 
      cm.replaceSelection(spaces);
    }   
  },
  "Shift-Tab": (cm) => {
    cm.indentSelection('subtract');
  },  
},
```
