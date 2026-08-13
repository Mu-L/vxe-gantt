<template>
  <div>
    <vxe-gantt v-bind="ganttOptions"></vxe-gantt>
  </div>
</template>

<script lang="ts" setup>
import { reactive } from 'vue'
import { VxeGanttProps } from '../../../types'

interface RowVO {
  id: number
  title: string
  start: string
  end: string
  progress: number
}

const ganttOptions = reactive<VxeGanttProps<RowVO>>({
  border: true,
  showOverflow: true,
  taskConfig: {
    dateFormat: 'yyyy-MM-dd HH:mm:ss'
  },
  taskBarConfig: {
    showProgress: true, // 是否显示进度条
    showContent: true, // 是否在任务条显示内容
    moveable: true, // 是否允许拖拽任务移动日期
    resizable: true, // 是否允许拖拽任务调整日期
    barStyle: {
      round: true, // 圆角
      bgColor: '#fca60b', // 任务条的背景颜色
      completedBgColor: '#65c16f' // 已完成部分任务条的背景颜色
    }
  },
  taskViewConfig: {
    scales: [
      { type: 'date' },
      { type: 'hour', step: 3 }
    ],
    tableStyle: {
      width: 480 // 表格宽度
    }
  },
  taskBarMoveConfig: {
    mode: 'progress' // 按实际拖拽进度比例进行渲染
  },
  taskBarResizeConfig: {
    mode: 'progress' // 按实际拖拽进度比例进行渲染
  },
  columns: [
    { type: 'seq', field: 'seq', width: 70 },
    { field: 'title', title: '任务名称', minWidth: 140 },
    { field: 'start', title: '开始时间', width: 160 },
    { field: 'end', title: '结束时间', width: 160 }
  ],
  data: [
    { id: 10001, title: '任务1', start: '2024-03-01 08:30:20', end: '2024-03-01 09:30:30', progress: 100 },
    { id: 10002, title: '任务2', start: '2024-03-01 00:00:00', end: '2024-03-01 00:00:00', progress: 100 },
    { id: 10003, title: '任务3', start: '2024-03-01 01:00:00', end: '2024-03-01 01:05:0', progress: 90 },
    { id: 10004, title: '任务4', start: '2024-03-01 01:20:00', end: '2024-03-01 08:50:00', progress: 80 }
  ]
})
</script>
