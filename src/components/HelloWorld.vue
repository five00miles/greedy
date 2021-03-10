<template>
  <div class="hello">
    <div>
      <div class="time-item" v-for="(time,idx) in timeList" :key="idx">
        <el-time-select placeholder="起始时间" v-model="time.startTime"
                        :picker-options="{start: '00:00',step: '00:01', end: '24:00' }">
        </el-time-select>
        <el-time-select placeholder="结束时间" v-model="time.endTime"
                        :picker-options="{start: '00:00',step: '00:01',end: '24:00',minTime: time.startTime}">
        </el-time-select>
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
      timeList: [{ startTime: '', endTime: '' }]
    }
  },
  methods: {
    handleAdd() {
      this.timeList.push({ startTime: '', endTime: '' })
    },
    mymethod(tableEdit) {
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
    }
  }
}
</script>
