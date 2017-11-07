<template>
  <div class="hello">
    <h1 @click="onClick">{{ msg }}</h1>
    <h2>Essential Links</h2>
    <ul>
      <li><a href="https://vuejs.org" target="_blank">Core Docs</a></li>
      <li><a href="https://forum.vuejs.org" target="_blank">Forum</a></li>
      <li><a href="https://chat.vuejs.org" target="_blank">Community Chat</a></li>
      <li><a href="https://twitter.com/vuejs" target="_blank">Twitter</a></li>
      <br>
      <li><a href="http://vuejs-templates.github.io/webpack/" target="_blank">Docs for This Template</a></li>
    </ul>
    <h2>Ecosystem</h2>
    <ul>
      <li><a href="http://router.vuejs.org/" target="_blank">vue-router</a></li>
      <li><a href="http://vuex.vuejs.org/" target="_blank">vuex</a></li>
      <li><a href="http://vue-loader.vuejs.org/" target="_blank">vue-loader</a></li>
      <li><a href="https://github.com/vuejs/awesome-vue" target="_blank">awesome-vue</a></li>
    </ul>
  </div>
</template>

<script>
  export default {
    name: 'HelloWorld',
    data () {
      return {
        msg: '点这里 看控制台'
      }
    },
    methods: {
      onClick(){
        console.log(111);
        console.log(Qiniu);

        var uploader = Qiniu.uploader({
          runtimes: 'html5,flash,html4',      // 上传模式，依次退化
          browse_button: 'selectVideo',         // 上传选择的点选按钮，必需

          uptoken_url: 'http://localhost/yiiserver/web/index.php/video/uptoken',         // Ajax请求uptoken的Url，强烈建议设置（服务端提供）

          get_new_uptoken: false,             // 设置上传文件的时候是否每次都重新获取新的uptoken
          // downtoken_url: '/downtoken',
          // Ajax请求downToken的Url，私有空间时使用，JS-SDK将向该地址POST文件的key和domain，服务端返回的JSON必须包含url字段，url值为该文件的下载地址
          // unique_names: true,              // 默认false，key为文件名。若开启该选项，JS-SDK会为每个文件自动生成key（文件名）
          save_key: true,                  // 默认false。若在服务端生成uptoken的上传策略中指定了save_key，则开启，SDK在前端将不对key进行任何处理
          domain: 'videopro',     // bucket域名，下载资源时用到，必需
          container: 'videoContainer',             // 上传区域DOM ID，默认是browser_button的父元素
          max_file_size: '100mb',             // 最大文件体积限制
          flash_swf_url: '../plupload/Moxie.swf',  //引入flash，相对路径
          max_retries: 3,                     // 上传失败最大重试次数
          dragdrop: true,                     // 开启可拖曳上传
          drop_element: 'videoContainer',          // 拖曳上传区域元素的ID，拖曳文件或文件夹后可触发上传
          chunk_size: '4mb',                  // 分块上传时，每块的体积
          auto_start: true,                   // 选择文件后自动上传，若关闭需要自己绑定事件触发上传
          //x_vars : {
          //    查看自定义变量
          //    'time' : function(up,file) {
          //        var time = (new Date()).getTime();
          // do something with 'time'
          //        return time;
          //    },
          //    'size' : function(up,file) {
          //        var size = file.size;
          // do something with 'size'
          //        return size;
          //    }
          //},


          init: {
            'FilesAdded': function (up, files) {
              plupload.each(files, function (file) {
                // 文件添加进队列后，处理相关的事情
              });
            },
            'BeforeUpload': function (up, file) {
              // 每个文件上传前，处理相关的事情
            },
            'UploadProgress': function (up, file) {
              // 每个文件上传时，处理相关的事情
            },
            'FileUploaded': function (up, file, info) {
              // 每个文件上传成功后，处理相关的事情
              // 其中info是文件上传成功后，服务端返回的json，形式如：
              // {
              //    "hash": "Fh8xVqod2MQ1mocfI4S4KpRL6D98",
              //    "key": "gogopher.jpg"
              //  }
              // 查看简单反馈
              // var domain = up.getOption('domain');
              // var res = parseJSON(info);
              // var sourceLink = domain +"/"+ res.key; 获取上传成功后的文件的Url
            },
            'Error': function (up, err, errTip) {
              //上传出错时，处理相关的事情
            },
            'UploadComplete': function () {
              //队列文件处理完毕后，处理相关的事情
            },
            'Key': function (up, file) {
              // 若想在前端对每个文件的key进行个性化处理，可以配置该函数
              // 该配置必须要在unique_names: false，save_key: false时才生效
              var key = "";
              // do something with key here
              return key
            }
          }
        });
      }
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  h1, h2 {
    font-weight: normal;
  }

  ul {
    list-style-type: none;
    padding: 0;
  }

  li {
    display: inline-block;
    margin: 0 10px;
  }

  a {
    color: #42b983;
  }
</style>
