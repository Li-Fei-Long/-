<template>
  <div class="wrapper">
    <!-- 头部 月/日试图切换 和下拉整体-->
    <header class="HeaderUtils">
      <nav class="RoomStatueNav">
        <div class="select">
          <span class="RoomTitle">日期</span>

          <el-date-picker
            v-model="SelectTime"
            type="month"
            placeholder="选择日期"
            popper-class="Timeed"
            format="yyyy 年 MM 月 "
            value-format="yyyy-MM"
            @change="SelectMonth"
          >
          </el-date-picker>
        </div>
      </nav>
    </header>
    <!-- 月视图 -->
    <main class="MothBox">
      <!-- 月视图左右两侧主要内容 -->
      <div class="theMainContent">
        <!-- 左侧 三部分内容 -->
        <div class="left">
          <!-- one -->
          <header>
            <span class="roomNumber">房号</span>
            <!-- 也可以循环 暂时先这样 -->
            <!-- <span>{{ GetTime.substr(0, GetTime.length - 3) }}</span> -->
            <span class="theCurrentTime">{{ inDynamic[0] }}</span>
            <span class="theCurrentTime">{{ inDynamic[1] }}</span>
            <span class="theCurrentTime">{{ inDynamic[2] }}</span>
          </header>
          <!-- two -->
          <div class="operationContent">
            <!-- 房间信息 -->
            <div
              class="RoomInfo"
              v-for="(item, index) in theGuestInfoList"
              :key="item.roomGuestId"
            >
              <!-- 房号 -->
              <p class="yourRoomNumber">{{ item.roomNo }}</p>
              <!-- 客户信息 -->
              <div class="theCustomerInformation">
                <!-- 时间节点盒子 -->
                <div class="timeNodeAll">
                  <!-- 时间节点  -->
                  <span
                    class="timeNode"
                    v-for="(item, index) in ThreeMonthNumber"
                    :key="index"
                  ></span>
                  <!-- 客户节点盒子 -->
                  <div
                    class="theCustomerNode"
                    v-for="(n, i) in item.viewMonthClienteleList"
                    :key="item.clienteleId"
                  >
                    <!-- {{ n.clienteleName }} -->
                    <!-- 拖拽节点 -->
                    <i
                      v-for="(node, nodeIndex) in n.endGrid"
                      :key="nodeIndex + n.clienteleId"
                      @click.stop="accordingToInfo(n.clienteleName)"
                      :style="{
                        background:
                          n.roomStatus == 2
                            ? pink
                            : n.roomStatus == 1
                            ? Skyblue
                            : n.roomStatus == 0
                            ? gray
                            : n.roomStatus == 3
                            ? darkBlue
                            : n.roomStatus == 5
                            ? green
                            : n.roomStatus == 4
                            ? brown
                            : '',
                      }"
                    >
                    </i>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <!-- three -->
          <footer></footer>
        </div>
        <!-- 右边添加客户 -->
        <div class="right"></div>
      </div>
    </main>
  </div>
  <!-- 内容结束部分 -->
</template>

<script>
export default {
  name: "MothView",
  data() {
    return {
      // 月/日试图切换
      SwitchValue: true,
      //desc 顶部日期双向绑定
      SelectTime: new Date(),
      //desc 头部动态月份 （根据当前月份自增加后面两个月）
      inDynamic: [],
      //#endregion
      // #region 左侧数据
      //desc 三个月总天数用作循环
      ThreeMonthNumber: null,
      //desc 左侧客人列表数据
      theGuestInfoList: [
        {
          roomGuestId: 1,
          roomNo: "8201",
          viewMonthClienteleList: [
            {
              clienteleId: 65,
              clienteleName: "邵芸",
              day: 19,
              startTime: "03-01",
              endTime: "03-19",
              startGrid: 1,
              endGrid: 19,
              roomStatus: 2,
              startLong: 1677600000000,
              endLong: 1679155200000,
              overallDay: 20,
              overallStartTime: "02-28",
              overallEndTime: "03-19",
              contactStart: null,
              contactEnd: null,
              roomClienteles: [],
            },
            {
              clienteleId: 75,
              clienteleName: "陈西西",
              day: 31,
              startTime: "04-01",
              endTime: "05-01",
              startGrid: 32,
              endGrid: 62,
              roomStatus: 1,
              startLong: 1680278400000,
              endLong: 1682870400000,
              overallDay: 31,
              overallStartTime: "04-01",
              overallEndTime: "05-01",
              contactStart: null,
              contactEnd: null,
              roomClienteles: [],
            },
          ],
        },
        {
          roomGuestId: 2,
          roomNo: "8202",
          viewMonthClienteleList: [
            {
              clienteleId: 56,
              clienteleName: "周蕾",
              day: 1,
              startTime: "03-01",
              endTime: "03-01",
              startGrid: 1,
              endGrid: 1,
              roomStatus: 2,
              startLong: 1677600000000,
              endLong: 1677600000000,
              overallDay: 29,
              overallStartTime: "02-01",
              overallEndTime: "03-01",
              contactStart: null,
              contactEnd: null,
              roomClienteles: [],
            },
            {
              clienteleId: 66,
              clienteleName: "邱扬",
              day: 32,
              startTime: "03-10",
              endTime: "04-10",
              startGrid: 10,
              endGrid: 41,
              roomStatus: 2,
              startLong: 1678377600000,
              endLong: 1681056000000,
              overallDay: 32,
              overallStartTime: "03-10",
              overallEndTime: "04-10",
              contactStart: null,
              contactEnd: null,
              roomClienteles: [],
            },
          ],
        },
        {
          roomGuestId: 3,
          roomNo: "8203",
          viewMonthClienteleList: [
            {
              clienteleId: 58,
              clienteleName: "陆琰红",
              day: 5,
              startTime: "03-01",
              endTime: "03-05",
              startGrid: 1,
              endGrid: 5,
              roomStatus: 2,
              startLong: 1677600000000,
              endLong: 1677945600000,
              overallDay: 24,
              overallStartTime: "02-10",
              overallEndTime: "03-05",
              contactStart: null,
              contactEnd: null,
              roomClienteles: [],
            },
            {
              clienteleId: 67,
              clienteleName: "强馨月",
              day: 33,
              startTime: "03-11",
              endTime: "04-12",
              startGrid: 11,
              endGrid: 43,
              roomStatus: 2,
              startLong: 1678464000000,
              endLong: 1681228800000,
              overallDay: 33,
              overallStartTime: "03-11",
              overallEndTime: "04-12",
              contactStart: null,
              contactEnd: null,
              roomClienteles: [],
            },
            {
              clienteleId: 77,
              clienteleName: "霍珂迪",
              day: 23,
              startTime: "04-10",
              endTime: "05-02",
              startGrid: 41,
              endGrid: 63,
              roomStatus: 1,
              startLong: 1681056000000,
              endLong: 1682956800000,
              overallDay: 23,
              overallStartTime: "04-10",
              overallEndTime: "05-02",
              contactStart: null,
              contactEnd: null,
              roomClienteles: [],
            },
          ],
        },
    
   
     
     
    
      
      ],
      // 预定
      Skyblue: "#5FC0FA",
      // 入住
      pink: "#FF81AD",
      // 重叠
      purple: "BF6BF7",
      // 空房
      gray: "#E1E1E1",
      // 维修
      darkBlue: "#5F6EB6",
      // 样板间
      green: "#80CA4E",
      // 脏房
      brown: "#9E6665",
      // 连续
      yellow: "#FFCC00",
      // 锁定
      darkGrey: "#A29CB9",
      //#endregion
    };
  },
  computed: {
    // 获取当前年月
    GetTime() {
      let date = new Date(),
        year = date.getFullYear(), //获取完整的年份(4位)
        month = date.getMonth() + 1, //获取当前月份(0-11,0代表1月)
        strDate = date.getDate(); // 获取当前日(1-31)
      if (month < 10) month = `0${month}`; // 如果月份是个位数，在前面补0
      if (strDate < 10) strDate = `0${strDate}`; // 如果日是个位数，在前面补0
      return `${year}-${month}-${strDate}`;
    },
  },
  methods: {
    // #region  头部 月/日试图切换和下拉整体方法

    // desc 选择月份
    SelectMonth(val) {
      this.getNextTwoMonths(val);
      this.getNextThreeMonthsTotalDays(val);
    },
    // 获取当前未来两个月
    getNextTwoMonths(Time) {
      let currentDate = Time;
      let date = new Date(currentDate);
      let currentMonthDate = new Date(date);
      let nextMonthDate = new Date(date.setMonth(date.getMonth() + 1));
      let nextTwoMonthsDate = new Date(date.setMonth(date.getMonth() + 1));
      let year0 = currentMonthDate.getFullYear();
      let month0 = currentMonthDate.getMonth() + 1;
      if (month0 < 10) month0 = `0${month0}`;
      // let strDate0 = currentMonthDate.getDate();
      let year1 = nextMonthDate.getFullYear();
      let month1 = nextMonthDate.getMonth() + 1;
      if (month1 < 10) month1 = `0${month1}`;
      // let strDate1 = nextMonthDate.getDate();
      let year2 = nextTwoMonthsDate.getFullYear();
      let month2 = nextTwoMonthsDate.getMonth() + 1;
      if (month2 < 10) month2 = `0${month2}`;
      // let strDate2 = nextTwoMonthsDate.getDate();
      return (this.inDynamic = [
        `${year0}-${month0}`,
        `${year1}-${month1}`,
        `${year2}-${month2}`,
      ]);
    },
    // 获取当前和未来个月的总天数
    getNextThreeMonthsTotalDays(Time) {
      let currentDate = Time;
      let date = new Date(currentDate);
      let currentMonthDate = new Date(date);
      let nextMonthDate = new Date(date.setMonth(date.getMonth() + 1));
      let nextTwoMonthsDate = new Date(date.setMonth(date.getMonth() + 1));
      // 获取每个月的最后一天
      let lastDayOfCurrentMonth = new Date(
        currentMonthDate.getFullYear(),
        currentMonthDate.getMonth() + 1,
        0
      ).getDate();
      let lastDayOfNextMonth = new Date(
        nextMonthDate.getFullYear(),
        nextMonthDate.getMonth() + 1,
        0
      ).getDate();
      let lastDayOfNextTwoMonths = new Date(
        nextTwoMonthsDate.getFullYear(),
        nextTwoMonthsDate.getMonth() + 1,
        0
      ).getDate();

      // 计算总天数
      return (this.ThreeMonthNumber =
        lastDayOfCurrentMonth + lastDayOfNextMonth + lastDayOfNextTwoMonths);
    },
    // #endregion
  },

  created() {},
  mounted() {
    //#region  * 获取当前月和未来两个月月份
    this.getNextTwoMonths(this.GetTime.substr(0, this.GetTime.length - 3));
    // 获取当前和未来两个月总天数
    this.getNextThreeMonthsTotalDays(
      this.GetTime.substr(0, this.GetTime.length - 3)
    );
    // 处理日期数据
    const [year, month] = this.inDynamic[0].split("-");
    const monthNumber = parseInt(month);
    const monthString = monthNumber.toString();
  },
};
</script>
<style lang="scss">
// 这些都是element 需要穿透的且不能加scopoed的样式
.RoomSelect {
  font-family: "Medium";
}
.Timeed {
  .el-picker-panel__body-wrapper {
    .el-picker-panel__body {
      font-family: "Medium";
      .el-picker-panel__content {
        .el-date-table {
          td.today span {
            color: #8e7bff;
          }
          td.current:not(.disabled) span {
            background: #8e7bff;
            color: #fff;
          }
          tbody {
            .el-date-table__row {
              td {
                &:hover {
                  color: #8e7bff;
                }
                span {
                  display: inline-flex;
                  align-items: center;
                  justify-content: center;
                  width: 30px;
                  height: 30px;
                  &:hover {
                    background: #8e7bff;
                    color: #fff;
                  }
                  &:focus {
                    background: #8e7bff;
                    color: #fff;
                  }
                }
              }
            }
          }
        }
      }
    }
  }
}
</style>
<style lang="scss" scoped>
@import "../../assets/css/mixin.scss";
.wrapper {
  height: 100%;
  width: 100%;
  padding: 20px 30px;
  box-sizing: border-box;
  // 最顶部标题
  .titleName {
    justify-content: space-between;
    display: flex;
    align-items: center;
    margin-bottom: 10px;
    aside {
      display: flex;
      align-items: center;
      img {
        margin-right: 5px;
      }
      @include Bold();
    }
  }
  // 头部 月/日试图切换 和下拉整体
  .HeaderUtils {
    display: flex;
    align-items: center;
    justify-content: space-between;
    width: 85%;
    // background: skyblue;
    height: 50px;
    .personNum {
      width: 10%;
      display: flex;
      justify-content: space-between;
      align-items: center;
      // margin: 30px 0 ;
      height: 50px;

      ::v-deep .el-switch__label * {
        line-height: 1;
        font-size: 14px;
        display: inline-block;
      }
      ::v-deep .el-switch__label {
        position: absolute;
        display: none;
        color: #fff;
        font-size: 12px;
      }
      /*打开时文字位置设置*/
      ::v-deep .el-switch__label--right {
        z-index: 1;
        right: 50px;
        font-family: "Bold";
        font-size: 14px;
      }
      /*关闭时文字位置设置*/
      ::v-deep .el-switch__label--left {
        z-index: 1;
        left: 50px;
        font-family: "Bold";
        font-size: 14px;
      }
      /*显示文字*/
      ::v-deep .el-switch__label.is-active {
        display: block;
      }
      /*开关宽度*/
      ::v-deep .el-switch .el-switch__core,
      .el-switch .el-switch__label {
        width: 117.5px !important;
        height: 40px;
        border-radius: 20px;
      }
      /*关闭时圆球的位置(只需要调整为垂直居中即可)*/
      ::v-deep .el-switch__core:after {
        width: 32px;
        height: 32px;
        top: 50%;
        transform: translateY(-50%);
        // margin-top: -16px;
      }
      /*打开时圆球的位置*/
      ::v-deep .el-switch.is-checked .el-switch__core::after {
        left: 85%;
      }
    }
    .RoomStatueNav {
      flex: 1;
      display: flex;
      justify-content: space-around;
      margin: 20px 0;
      .select {
        box-sizing: border-box;
        ::v-deep .el-date-editor {
          width: 180px;
          .el-input__inner {
            border-color: #8787aa;
            border-radius: 10px;
            width: 180px;
            font-family: "Medium";
            &:hover {
              border-color: #aba4ff;
            }
            &:focus {
              border-color: #aba4ff;
            }
          }
        }
        .RoomTitle {
          margin-right: 20px;
          font-family: "Medium";
          text-align: center;
        }
        .el-select {
          width: 180px;
        }
      }
    }
    .OccupancyRate {
      width: 13%;
      // background: #aba4ff;
      display: flex;
      align-items: center;
      justify-content: space-around;
      img {
        width: 22px;
        height: 22px;
        margin-left: 20px;
      }

      > span:nth-child(2) {
        font-family: "Medium";
        font-size: 14px;
      }
      > span:nth-child(3) {
        font-family: "Bold";
        font-size: 34px;
      }
    }
  }
  // 月视图
  .MothBox {
    height: 91%;
    margin-top: 10px;
    // border-radius: 20px;
    // 月视图左右两侧主要内容
    .theMainContent {
      display: flex;
      height: 100%;
      // 左侧 三部分内容
      .left {
        height: 100%;
        // background: pink;
        width: 85%;
        display: flex;
        flex-direction: column;
        // one
        header {
          height: 6%;
          background: #eeecff;
          border-radius: 20px 0px 0px 0px;
          font-family: "Bold";
          display: flex;
          // 房号
          .roomNumber {
            width: 5%;
            border-right: 1px solid #fff;
            box-sizing: border-box;
          }
          .theCurrentTime {
            flex: 1;
          }
          span {
            display: inline-flex;
            align-items: center;
            justify-content: center;
            color: #9283d6;
            font-size: calc(100vw * 16 / 1920);
          }
        }
        // two
        .operationContent {
          height: 80%;
          // background: #cccccca3;
          overflow: auto;
          // 房间信息
          .RoomInfo {
            height: 16%;
            // background: skyblue;
            font-family: "Medium";
            display: flex;
            border-bottom: 1px solid #eeeeee;
            box-sizing: border-box;
            // 房间号
            .yourRoomNumber {
              width: 5%;
              height: 100%;
              color: #81819f;
              font-size: calc(100vw * 16 / 1920);
              border-right: 1px solid #eeeeee;
              border-left: 1px solid #eeeeee;
              box-sizing: border-box;
              display: inline-flex;
              justify-content: center;
              align-items: center;
            }
            // 客户信息
            .theCustomerInformation {
              flex: 1;
              position: relative;
              // 时间节点
              .timeNodeAll {
                width: 100%;
                display: inline-flex;
                justify-content: space-between;
                align-items: center;
                padding: 0 15px;
                box-sizing: border-box;
                height: 100%;
                position: relative;
                // background: #8e7bff;
                // 时间节点
                .timeNode {
                  width: 8px;
                  height: 8px;
                  background: #e1e1e1;
                  border-radius: 2px 2px 2px 2px;
                  margin: 0 6px 0 0;
                  z-index: 11;
                }
                // 客户节点
                .theCustomerNode {
                  position: absolute;
                  color: red;
                  height: 100%;
                  display: inline-flex;
                  align-items: center;
                  // height: 100px;
                  i {
                    width: 8px;
                    height: 8px;
                    display: inline-block;
                    // margin-top: 2px;
                    box-sizing: border-box;
                    opacity: 0.7;
                    // &:active {
                    //    box-shadow: 0px 4px 10px 0px rgba(79,126,255,0.74);
                    // }
                  }
                }
              }
            }
          }
        }
        // three
        footer {
          flex: 1;
          background: #f7f6f2;
        }
      }
      .right {
        flex: 1;
        height: 100%;
        background: #8e7bff;
      }
    }
  }
}

// 下拉框的 一边去
::v-deep .el-select {
  .el-input__inner {
    border-color: #8787aa;
    font-family: "Medium";
  }
  .el-input.is-focus .el-input__inner {
    border-color: #aba4ff;
  }

  .el-input {
    .el-input__inner {
      border-radius: 10px;
      &:hover {
        border-color: #aba4ff;
      }
    }
  }
}
</style>