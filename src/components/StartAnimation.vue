<template>


    <div id="incloud">
      <div id="canvas01">
      </div>
      <div id="tiptext">
        <img @mouseenter="pikapika" @mouseleave="stilllight" id="clicktocontinue" src="../staticFile/imgs/clicktocontinue.png" alt="点击以继续">
      </div>
    </div>


</template>




<script>

import * as spritejs from "spritejs";
//
// let winWidth = 0;
// let winHeight = 0;
//
// if (window.innerWidth) {
//   winWidth = window.innerWidth
// }else if ((document.body) && (document.body.clientWidth)){
//   winWidth = document.body.clientWidth;
// }
//
// if (window.innerHeight){
//   winHeight = window.innerHeight
// }else if ((document.body) && (document.body.clientHeight)){
//   winHeight = document.body.clientHeight
// }
//
// console.log("（OP）窗口宽度：" + winWidth);
// console.log("（OP）窗口高度：" + winHeight);



export default {
  name: "StartAnimation",
  data:() => {
    return {
      italyLine: null,
      leftDoor: null,
      rightDoor: null,
      leftdoor: null,
      rightdoor: null,
      ani01Fin: false,
    }
  },
  computed: {



    winWidth: () => {
      if (window.innerWidth) {     // 获取页面高度
        return window.innerWidth
      }else if ((document.body) && (document.body.clientWidth)){
        return document.body.clientWidth;
      }
    },
    winHeight: () => {
      if (window.innerHeight){     // 获取页面宽度
        return window.innerHeight
      }else if ((document.body) && (document.body.clientHeight)){
        return document.body.clientHeight
      }
    }


  },
  methods: {

    drowLogo: function (flag) {


      //dubug
      console.log("窗口宽度：" + this.winWidth);
      console.log("窗口高度：" + this.winHeight);
      console.log("flag is：" + flag);




      // igalyLine's points start 构筑中间斜线的端点
      let zero = 0,

          //斜线宽度
          italyLine_Width = this.winWidth * 0.003,
          // 中间的白色斜线 -左上
          italyLine_LeftTopX = this.winWidth * 0.368489,
          italyLine_LeftTopY = zero,
          // 已知 斜线角度 与 浏览器页面高度，做垂直于浏览器上边且过斜线下端点的辅助线，
          // 中间的白色斜线 -左下                             辅助线长度等于浏览器页面高度，可得减可得斜线下端点X值与上端点X值之差
          italyLine_LeftBottomX = italyLine_LeftTopX - (1/(Math.tan((65*(Math.PI/180))))) * this.winHeight,
          italyLine_LeftBottomY = this.winHeight,
          // 中间的白色斜线 -右下
          italyLine_RightBottomX = italyLine_LeftBottomX + italyLine_Width,
          italyLine_RightBottomY = this.winHeight,
          // 中间的白色斜线 -右上
          italyLine_RightTopX = italyLine_LeftTopX + italyLine_Width,
          italyLine_RightTopY = zero

      // finish 端点构筑完毕

      // leftDoor's points start 构筑左侧大门的端点
      let
          // 左侧大门 -左上
          leftDoor_LeftTopX = zero,
          leftDoor_LeftTopY = zero,
          // 左侧大门 -左下
          leftDoor_LeftBottomX = zero,
          leftDoor_LeftBottomY = this.winHeight,
          // 左侧大门 -右下         与中间斜线的左下点重合，故沿用
          leftDoor_RightBottomX = italyLine_LeftBottomX,
          leftDoor_RightBottomY = italyLine_LeftBottomY,
          // 左侧大门 -右上         与中间斜线的左上点重合，故沿用
          leftDoor_RightTopX = italyLine_LeftTopX,
          leftDoor_RightTopY = italyLine_LeftTopY,

          // 左侧大门拉开所需要的偏移量  与斜线左上角点X值相等
          leftDoor_XDecrease = italyLine_LeftTopX

      // finish 端点构筑完毕

      // leftDoor's points start 构筑中间斜线的端点
      let
          // 右侧大门 -左上         与中间斜线的右上点重合，故沿用
          rightDoor_LeftTopX = italyLine_RightTopX,
          rightDoor_LeftTopY = zero,
          // 右侧大门 -左下         与中间斜线的右下点重合，故沿用
          rightDoor_LeftBottomX = italyLine_RightBottomX,
          rightDoor_LeftBottomY = italyLine_RightBottomY,
          // 右侧大门 -右下
          rightDoor_RightBottomX = this.winWidth,
          rightDoor_RightBottomY = this.winHeight,
          // 右侧大门 -右上
          rightDoor_RightTopX = this.winWidth,
          rightDoor_RightTopY = zero,

          // 右侧大门拉开所需要的偏移量  等于窗口总宽度减去左下点的X值
          rightDoor_XDecrease = this.winWidth - italyLine_RightBottomX

      // finish 端点构筑完毕


      // colors here 定义几个图形的颜色
      let italyLine_color = '#ffffff',

          leftDoor_color = '#403f3f',
          leftDoor_color_hover = '#363636',

          rightDoor_color = '#1f1f1f',

          leftdoor_color = '#00a7e0',
          rightdoor_color = '#ff3f1a'

      // fin



      //绘制OP动画的斜线和大门
      const {Scene, Polyline} = spritejs
      const canvas01 = document.getElementById('canvas01')
      const scene = new Scene({
        container: canvas01,
        width: this.winWidth,
        height: this.winHeight,
      })
      const layer = scene.layer()



      if (flag == 0){


        document.getElementById('incloud').style.height = 100 + "vh"   //展开画布

        //绘制左边小门, 底层图层的代码在上
        this.leftdoor = new Polyline({

          pos: [0,0],  //原点坐标
          //               左上                                               左下
          points: [ leftDoor_LeftTopX,leftDoor_LeftTopY,              leftDoor_LeftBottomX,leftDoor_LeftBottomY,
                    leftDoor_RightBottomX,leftDoor_RightBottomY,      leftDoor_RightTopX,leftDoor_RightTopY
            //                右下                                               右上
          ],
          fillColor: leftdoor_color,
          close: true,
          smooth: false

        })
        layer.append(this.leftdoor)


        //绘制右边小门, 底层图层的代码在上
        this.rightdoor = new Polyline({

          pos: [0,0],  //原点坐标
          //                左上                                               左下
          points: [ rightDoor_LeftTopX,rightDoor_LeftTopY,              rightDoor_LeftBottomX,rightDoor_LeftBottomY,
                    rightDoor_RightBottomX,rightDoor_RightBottomY,      rightDoor_RightTopX,rightDoor_RightTopY
            //                右下                                               右上
          ],
          fillColor: rightdoor_color,
          close: true,
          smooth: false

        })

        layer.append(this.rightdoor)


        //绘制中间的斜线
        this.italyLine = new Polyline({
          pos: [0,0],  //原点坐标
          //                左上                                               左下
          points: [ italyLine_LeftTopX,italyLine_LeftTopY,              italyLine_LeftBottomX,italyLine_LeftBottomY,
                    italyLine_RightBottomX,italyLine_RightBottomY,      italyLine_RightTopX,italyLine_RightTopY
            //                 右下                                              右上
          ],
          fillColor: italyLine_color,
          close: true,
          smooth: false

        })
        layer.append(this.italyLine);


        //绘制左边大门
        this.leftDoor = new Polyline({

          pos: [0,0],  //原点坐标
          //               左上                                               左下
          points: [ leftDoor_LeftTopX,leftDoor_LeftTopY,              leftDoor_LeftBottomX,leftDoor_LeftBottomY,
                    leftDoor_RightBottomX,leftDoor_RightBottomY,      leftDoor_RightTopX,leftDoor_RightTopY
            //                右下                                               右上
          ],
          fillColor: leftDoor_color,
          close: true,
          smooth: false

        })
        layer.append(this.leftDoor)

        //为左侧大门添加hover效果
        this.leftDoor.addEventListener('mouseenter',() => {

          this.leftDoor.attr({
            fillColor: leftDoor_color_hover
          })
        })
        this.leftDoor.addEventListener('mouseleave',() => {

          this.leftDoor.attr({
            fillColor: leftDoor_color
          })
        })


        //绘制右边大门
        this.rightDoor = new Polyline({

          pos: [0,0],  //原点坐标
          //                左上                                               左下
          points: [ rightDoor_LeftTopX,rightDoor_LeftTopY,              rightDoor_LeftBottomX,rightDoor_LeftBottomY,
                    rightDoor_RightBottomX,rightDoor_RightBottomY,      rightDoor_RightTopX,rightDoor_RightTopY
            //                右下                                               右上
          ],
          fillColor: rightDoor_color,
          close: true,
          smooth: false

        })

        layer.append(this.rightDoor)

      }
      console.log("绘制完毕");


//————————————————————————————————careful gook luck————————————————————————————————————————



      if (flag == 1){

        let animeTime = 900  //动画总时长，单位：毫秒

        setTimeout(() => {
          document.getElementById('canvas01').style.display = "none"     //隐藏画板，用于退出鼠标样式以及异常情况的跳出
          document.getElementById('tiptext').style.display = "none"      //隐藏提示文字，用于退出鼠标样式以及异常情况的跳出

        },animeTime)



        if(this.ani01Fin != true){
          //隐藏提示文字的动画
           document.getElementById('tiptext').animate(
               [
                 {
                   opacity: 1
                 },
                 {
                   opacity: 0
                 }
               ],
               {
                 duration: 300,
                 fill: "forwards",
                 easing: "ease-in"
               }
           )





          // 隐藏中间的线的动画
          setTimeout(() => {
            this.italyLine.transition(0).attr({
              //        左下               左上
              points: [ 0,0,              0,0,
                0,0,              0,0
                //        右下               右上
              ]
            })
          },200)



          //绘制左边小门打开的动画,低层图层的代码要在上面
          this.leftdoor.animate([
                {
                  //               左上                                               左下
                  points: [ leftDoor_LeftTopX,leftDoor_LeftTopY,              leftDoor_LeftBottomX,leftDoor_LeftBottomY,
                    leftDoor_RightBottomX,leftDoor_RightBottomY,      leftDoor_RightTopX,leftDoor_RightTopY
                    //                右下                                               右上
                  ]
                },
                {
                  //                 左上偏移量                                                            左下偏移量
                  points: [ leftDoor_LeftTopX - leftDoor_XDecrease,leftDoor_LeftTopY,              leftDoor_LeftBottomX - leftDoor_XDecrease,leftDoor_LeftBottomY,
                    leftDoor_RightBottomX - leftDoor_XDecrease,leftDoor_RightBottomY,      leftDoor_RightTopX - leftDoor_XDecrease,leftDoor_RightTopY
                    //                 右下偏移量                                                            右上偏移量
                  ]
                }
              ],
              {
                delay: 200,
                duration: 700,
                fill: "forwards",
                easing: "ease-in-out"
              }

          )
          layer.append(this.leftdoor)



          //绘制右边小门打开的动画，低层图层的代码要在上面
          this.rightdoor.animate([
                {
                  //                左上                                               左下
                  points: [ rightDoor_LeftTopX,rightDoor_LeftTopY,              rightDoor_LeftBottomX,rightDoor_LeftBottomY,
                    rightDoor_RightBottomX,rightDoor_RightBottomY,      rightDoor_RightTopX,rightDoor_RightTopY
                    //                右下                                               右上
                  ]
                },
                {
                  //                 左上偏移量                                                            左下偏移量
                  points: [ rightDoor_LeftTopX + rightDoor_XDecrease,rightDoor_LeftTopY,              rightDoor_LeftBottomX + rightDoor_XDecrease,rightDoor_LeftBottomY,
                    rightDoor_RightBottomX + rightDoor_XDecrease,rightDoor_RightBottomY,      rightDoor_RightTopX + rightDoor_XDecrease,rightDoor_RightTopY
                    //                 右下偏移量                                                            右上偏移量
                  ]
                }
              ],
              {
                delay: 200,
                duration: 700,
                fill: "forwards",
                easing: "ease-in-out"
              }

          )
          layer.append(this.rightdoor)


          //绘制左边大门打开的动画
          this.leftDoor.animate([
                {
                  //               左上                                               左下
                  points: [ leftDoor_LeftTopX,leftDoor_LeftTopY,              leftDoor_LeftBottomX,leftDoor_LeftBottomY,
                    leftDoor_RightBottomX,leftDoor_RightBottomY,      leftDoor_RightTopX,leftDoor_RightTopY
                    //                右下                                               右上
                  ]
                },
                {
                  //                 左上偏移量                                                            左下偏移量
                  points: [ leftDoor_LeftTopX - leftDoor_XDecrease,leftDoor_LeftTopY,              leftDoor_LeftBottomX - leftDoor_XDecrease,leftDoor_LeftBottomY,
                    leftDoor_RightBottomX - leftDoor_XDecrease,leftDoor_RightBottomY,      leftDoor_RightTopX - leftDoor_XDecrease,leftDoor_RightTopY
                    //                 右下偏移量                                                            右上偏移量
                  ]
                }
              ],
              {
                duration: 900,
                fill: "forwards",
                easing: "ease-in-out"
              }

          )
          layer.append(this.leftDoor)



          //绘制右边大门打开的动画
          this.rightDoor.animate([
                {
                  //                左上                                               左下
                  points: [ rightDoor_LeftTopX,rightDoor_LeftTopY,              rightDoor_LeftBottomX,rightDoor_LeftBottomY,
                    rightDoor_RightBottomX,rightDoor_RightBottomY,      rightDoor_RightTopX,rightDoor_RightTopY
                    //                右下                                               右上
                  ]
                },
                {
                  //                 左上偏移量                                                            左下偏移量
                  points: [ rightDoor_LeftTopX + rightDoor_XDecrease,rightDoor_LeftTopY,              rightDoor_LeftBottomX + rightDoor_XDecrease,rightDoor_LeftBottomY,
                    rightDoor_RightBottomX + rightDoor_XDecrease,rightDoor_RightBottomY,      rightDoor_RightTopX + rightDoor_XDecrease,rightDoor_RightTopY
                    //                 右下偏移量                                                            右上偏移量
                  ]
                }
              ],
              {
                duration: 900,
                fill: "forwards",
                easing: "ease-in-out"
              }

          )
          layer.append(this.rightDoor)



          this.ani01Fin = true  //将动画播放完成标识设为true

          setTimeout(() => {
            document.getElementById('incloud').style.height = 0 + "px"   //动画完成后收起画板
          },animeTime)




        }

      }




    },

    openTheDoor: function (flag) {
      // console.log("test openDoor");
      this.drowLogo(flag)
    },
    pikapika: () => {
      const tipTextimg = document.getElementById("clicktocontinue")
      tipTextimg.animate(
          [
            {
              opacity: 1
            },
            {
              opacity: 0.5
            }
          ],
          {
            duration: 1500,
            fill: "forwards",
            iterations: Infinity,
            direction: "alternate",
            easing: "ease-in-out"
          }
      )
    },
    stilllight: () => {
      const tipTextimg = document.getElementById("clicktocontinue")
      tipTextimg.animate(
          [
            {
              opacity: 0.8
            },
            {
              opacity: 1
            }
          ],
          {
            duration: 1000,
            fill: "forwards",
            easing: "ease-out"
          }
      )
    }

  },
  mounted() {
    this.drowLogo(0)
  }
}
</script>

<style scoped>


  #incloud{
    width: 100vw;
    height: 100vh;

    position: absolute;


  }
  #canvas01{
    /*background-color: white;*/
    width: 100%;
    height: 100%;

    position: absolute;
    /*left: 0px;*/
    /*width: 0px;*/

    cursor:crosshair;
    /*鼠标指针变成十字架*/

  }
  #tiptext{
    width: 15vw;
    height: 21.5vh;

    /*border: 3px solid purple;*/

    position: absolute;
    top: 44vh;
    left: 60vw;

    cursor:crosshair;
    /*鼠标指针变成十字架*/

    /*font:40px verdana, arial, sans-serif; !* 设置文字大小和字体样式 *!*/
    /*color: #ffffff;*/
  }
  #clicktocontinue{
    width: 100%;
  }




</style>