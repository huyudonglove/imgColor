<!--
 * @Description: 
 * @Author: ydhu5
 * @Date: 2022-03-22 13:58:08
 * @LastEditTime: 2022-03-25 11:30:02
 * @LastEditors: ydhu5
-->
<template>
  <div>
    <button @click="changeD">66666666666</button>
    <img
      v-for="item in num"
      :src="item.url"
      alt=""
      :style="item.css"
      :class="item.class"
    />
    <div>
      <img src="../../public/i1/ca.jpg" alt="" />
      <div style="position: relative; height: 500px">
        <div style="width: 488px; height: 365px" class="d1"></div>
        <div class="d2"></div>
      </div>
      <div style="position: relative">
        <div class="d3"></div>
        <div class="d4"></div>
      </div>
    </div>
  </div>
</template>

<script>
import img1 from "../../public/i1/1.png";
export default {
  name: "HelloWorld",
  data() {
    return {
      msg: "Welcome to Your Vue.js App",
      num: [
        {
          url: require("../../public/i1/1.png"),
          css: "position:relative;overflow:hidden",
          class: "hover",
        },
        {
          url: require("../../public/i1/2.png"),
          css: "",
          class: "hover",
        },
        {
          url: require("../../public/i1/3.png"),
          css: "",
          class: "hover",
        },
        {
          url: require("../../public/i1/4.png"),
          css: "",
          class: "hover",
        },
        {
          url: require("../../public/i1/5.png"),
          css: "",
          class: "hover",
        },
        {
          url: require("../../public/i1/6.png"),
          css: "",
          class: "hover",
        },
        {
          url: require("../../public/i1/7.png"),
          css: "",
          class: "hover",
        },
      ],
    };
  },
  methods: {
    chang(imgUrl, color, callback) {
      let threshold = 114; //默认颜色阀值 为 114 －>和默认图相关
      let img = new Image();
      img.src = imgUrl;
      console.log(img);
      let newR = parseInt("0x" + color.substr(1, 2));
      let newG = parseInt("0x" + color.substr(3, 2));
      let newB = parseInt("0x" + color.substr(5, 2));
      console.log(7777777777777);
      //图片加载后进行处理
      img.onload = function () {
        console.log("wojinlaile");
        let width = img.width,
          height = img.height,
          canvas = document.createElement("canvas"),
          ctx = canvas.getContext("2d");
        canvas.width = width;
        canvas.height = height;
        // 将源图片复制到画布上
        ctx.drawImage(img, 0, 0, width, height);
        // 获取画布的像素信息
        let imageData = ctx.getImageData(0, 0, width, height),
          data = imageData.data;
        // 对像素集合中的单个像素进行循环，每个像素是由4个通道组成，所以要注意
        let i = 0;
        while (i < data.length) {
          let r = data[i++],
            g = data[i++],
            b = data[i++],
            a = data[i++];
          //计算透明度
          let alp = (255 - r) / (255 - threshold);
          //判断是否透明
          let isTransparent = a == 0;
          if (isTransparent) {
            data[i - 1] = 0;
          } else {
            data[i - 4] = newR;
            data[i - 3] = newG;
            data[i - 2] = newB;
            data[i - 1] = a !== 255 ? 255 - a : alp * 255; //处理透明的图片和不透明的图片
          }
        }
        // 将修改后的代码复制回画布中
        ctx.putImageData(imageData, 0, 0);
        // 图片导出为 png 格式
        let imgType = "png";
        let imgData = canvas.toDataURL(imgType);
        // console.log(imgData); // 生成base64
        callback && callback(imgData);
      };
      return img;
    },
    changeD() {
      console.log(1111111);
      this.chang(img1, "#f51ca6", (img) => {
        console.log(img);
      });
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style >
.hover:hover {
  position: absolute;
  top: -95px;
  filter: drop-shadow(0px 95px 0 green);
}
.d1 {
  position: absolute;
  z-index: 1;
  background-image: url("../../public/i1/ca.jpg"), linear-gradient(blue, blue);
  background-blend-mode: lighten;
  background-repeat: no-repeat;
}
.d2 {
  position: absolute;
  z-index: 2;
  background-image: url("../../public/i1/2-1.png"), linear-gradient(red);
  background-blend-mode: lighten;
  background-repeat: no-repeat;
  width: 187px;
  height: 140px;
  top: 47px;
  left: 100px;
}
.d3 {
  position: absolute;
  z-index: 1;
  background-image: url("../../public/i1/t3.svg"), linear-gradient(red);
  background-blend-mode: lighten;
  background-repeat: no-repeat;
  width: 187px;
  height: 140px;
  top: 47px;
  left: 100px;
}
.d4 {
  position: absolute;
  z-index: 2;
  background-image: url("../../public/i1/t4.svg"), linear-gradient(blue);
  background-blend-mode: lighten;
  background-repeat: no-repeat;
  width: 187px;
  height: 140px;
  top: 47px;
  left: 100px;
}
</style>
