基于vue.js图像预览组件

# Github
[github][1]


# 安装

    npm install enlargeimg --save-dev
    

    import enlargeimg from 'enlargeimg'; 

 

# 基础用法

    <enlargeImg :data="files"></enlargeImg> 

 
  
    export default {
      name: 'hello',
      data () {
        return {
          msg: 'Welcome to Your Vue.js App',
          files:[
        {
          path:'http://img4q.duitang.com/uploads/item/201311/01/20131101141757_tunaj.png'
        },
        {
          path:'http://img5.duitang.com/uploads/item/201503/22/20150322122457_EQ3NP.thumb.700_0.jpeg'
        },
        {
          path:'http://tupian.enterdesk.com/uploadfile/2013/1219/20131219053302481.jpg'
        },
      ]
        }
      },
    }
    
# 注意事项

    图片地址为path
    
    此组件主要针对PC端，手机端未测试。


  [1]: https://github.com/Repeg/enlargeImg
