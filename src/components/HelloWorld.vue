<template>
  <div class="hello">
    <div>
      <div class="time-item" v-for="(item,idx) in timeList" :key="idx">
        <el-time-picker is-range arrow-control v-model="item.time" format="HH:mm" value-format="HH:mm" range-separator="至" start-placeholder="开始时间" end-placeholder="结束时间">
        </el-time-picker>
      </div>
    </div>

    <el-button type="primary" @click="handleAdd">增加</el-button>
    <el-button type="primary" @click="mymethod(timeList)">判断</el-button>
    <p>{{timeList}}</p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      timeList: [{ time: '' }]
    }
  },
  methods: {
    handleAdd() {
      this.timeList.push({ time: '' })
    },
    mymethod(arr) {
      var tableEdit = this.formatTime(arr)
      console.log(tableEdit)
      var layerEditFlage = false
      var startTimeArr = []
      var endTimeArr = []
      var timeS = ''
      var timeE = ''
      for (var i = 0; i < tableEdit.length; i++) {
        timeS = tableEdit[i].startTime
        startTimeArr.push(timeS)
      }
      for (let i = 0; i < tableEdit.length; i++) {
        timeE = tableEdit[i].endTime
        endTimeArr.push(timeE)
      }
      var begin = startTimeArr.sort()
      var over = endTimeArr.sort()
      for (var k = 1; k < begin.length; k++) {
        if (begin[k] < over[k - 1]) {
          console.log(begin[k], over[k - 1])
          layerEditFlage = true
        }
      }
      if (layerEditFlage) {
        console.log('时间段有重叠,请检查!!')
      }
    },
    formatTime(arr) {
      const tableEdit = [...arr]
      return tableEdit.map(time => {
        return {
          startTime: time.time[0].split(':')[0] * 60 + time.time[0].split(':')[1] * 1,
          endTime: time.time[1].split(':')[0] * 60 + time.time[1].split(':')[1] * 1
        }
      })
    }
  }
}
</script>
