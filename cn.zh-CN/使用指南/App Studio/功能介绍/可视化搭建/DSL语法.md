# DSL语法 {#concept_tyk_lqh_dhb .concept}

DSL是一种以React JSX与Vue template的语言特性为基础，更符合UI编排的组件化语言。

## JSX {#section_btc_vqh_dhb .section}

DSL语法类似于React.render方法中的JSX部分，JSX的简单理解如下：

-   通过`{}`，将HTML作用域切换为JS作用域。JS作用域可以写任何合法的JS表达式，返回值会输出到页面上，例如`<div>{'Hello' + ' Relim'}</div>`。

    **说明：** `{ }`内可以写任何计算语句或字面量等JS表达式。

-   通过HTML标签，将JS作用域切换为HTML作用域，例如`{<div>Hello Relim</div>}`。
-   HTML和JS作用域切换可以嵌套进行，例如`{<div>{'Hello' + ' Relim'}</div>}`。

JSX的更多详情请参见[React JSX](https://reactjs.org/docs/introducing-jsx.html)。

## 合法的JS表达式 {#section_zbo_1le_ir4 .section}

``` {#codeblock_cr3_j66_90s}
//计算语句的情形
{aaa} // √   变量aaa需要有定义
{aaa * 111} // √
{1 == 1 ? 1 : 0} // √
{/^123/.test(aa)} // √
{[1,2,3].join('')} // √
{(()=>{return 1})()} //自执行函数 √

//字面量
{1}
{true}
{[11,22,33]} // √
{{aa:"11",bb:"22"}} // √
{()=>1} //描述一个函数，合法，但无意义 √
```

**说明：** 如果遇到较为复杂的逻辑，一条计算语句不能实现，需拆分为多条语句的需求。可以将其包装为自执行函数，自执行函数是合法的表达式。示例如下：

``` {#codeblock_x1p_su7_jbb}
{(function(){
    //将一个数字数组的偶数为求和。
    var input = [1,2,3,4,5,6,7,8,9,10];
    var temp = input.filter(i => i % 2 == 0)
    return temp.reduce((buf, cur) => buf + cur, 0)
})()}
```

## 非法的JS表达式 {#section_xkd_prh_dhb .section}

``` {#codeblock_vnc_vex_1vi}
{ var a = 1 } // 赋值语句。
{ aaa * 111; 2} // 出现分号的多条语句。
```

