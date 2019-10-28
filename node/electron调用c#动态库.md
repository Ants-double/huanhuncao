# electron调用c#动态库

## 新建C#动态库

- 方法要以异步任务的方式，可以直接包装，也可以写成天然异步

- 代码如下

  ``` c#
  public class Class1
      {
          public async Task<Object> Invoke(object input)
          {
              return Helper.SayHi("Invoke1:" + (string)input);
          }
  
          public async Task<Object> Invoke2(object input)
          {
              return  Helper.SayHi("Invoke2:" + (string)input);
          }
  
          static class Helper
          {
              public static string SayHi(string param)
              {
                  return ".NET Welcomes " + param;
              }
          }
  ```


##  安装electron-edge-js模块

- 调用代码如下

  ``` javascript
  
  const edge = require('electron-edge-js');
  console.info("call c#")
  
  var DemoDll = edge.func({
      assemblyFile: "electronedge.dll",
      typeName: "electronedge.Class1",
      methodName: "Invoke"
  });
  var DemoDll2 = edge.func({
      assemblyFile: "electronedge.dll",
      typeName: "electronedge.Class1",
      methodName: "Invoke2"
  });
  // module.exports.DemoDll = DemoDll;
  module.exports.DemoDll = {
      demo: DemoDll,
      demo2:DemoDll2
  };
  
  
  ```

  

- node引用如下

  ``` javascript
  const DemoDll = require("./csharputil.js");
  
  DemoDll.DemoDll.demo("test", (err, value)=> {
    log.debug(value);
  
  });
  ```

  

- 页面js引用如下

  

  - 包装如下

    ``` javascript
    function init() {
        const DemoDll = require("F:/yanghuaihua/electronedge/csharputil.js");
    
    
        return {
            demo: DemoDll.DemoDll.demo,
            demo2:DemoDll.DemoDll.demo2
           
        };
    }
    const initRequire = init();
    ```

    

  - 引用如下

    ```javascript
    
        <script>window.$ = window.jQuery = require('./js/jquery-3.4.1.min.js');</script>
        <script type="text/javascript" src="./js/init.js"></script>
        <script type="text/javascript" src="./js/index.js"></script>
        <script type="text/javascript">
            $("#btn").click(function () {
                initRequire.demo("test", (err, value) => {
                    $("#demo").append(value);
                    $("#demo").text(value);
                });
                setInterval(()=>{
                    initRequire.demo2("test", (err, value) => {
                    $("#demo").append(value);
                    $("#demo").text(value);
                });
                }, 1500);
               
            });
    
        </script>
    ```

    

##  源码地址

[ https://github.com/Ants-double/yumi/tree/master/electronedge ]( https://github.com/Ants-double/yumi/tree/master/electronedge )