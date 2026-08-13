<template>
  <div>
    <vxe-gantt v-bind="ganttOptions"></vxe-gantt>
  </div>
</template>

<script lang="ts" setup>
import { reactive } from 'vue'
import type { VxeGanttProps } from '../../../types'

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
    resizable: true,
    barStyle: {
      round: true, // 圆角
      bgColor: '#fca60b', // 任务条的背景颜色
      completedBgColor: '#65c16f' // 已完成部分任务条的背景颜色
    }
  },
  taskViewConfig: {
    scales: [
      { type: 'month' },
      { type: 'date', step: 3 }
    ],
    tableStyle: {
      width: 480 // 表格宽度
    },
    viewStyle: {
      cellWidth: 120 // 单元格宽度
    }
  },
  taskBarMoveConfig: {
    mode: 'progress'
  },
  taskBarResizeConfig: {
    mode: 'progress'
  },
  columns: [
    { type: 'seq', field: 'seq', width: 70 },
    { field: 'title', title: '任务名称' },
    { field: 'start', title: '开始时间', width: 160 },
    { field: 'end', title: '结束时间', width: 160 }
  ],
  data: [
    { id: 10001, title: '任务1', start: '2024-02-27 08:30:00', end: '2024-03-04 12:30:00', progress: 50 },
    { id: 100012, title: '任务1', start: '2024-02-28 08:30:00', end: '2024-03-04 12:30:00', progress: 50 },
    { id: 100013, title: '任务1', start: '2024-02-29 08:30:00', end: '2024-03-04 12:30:00', progress: 50 }
    // { id: 10002, title: '任务2', start: '2024-03-03 09:30:40', end: '2024-03-07 11:40:50', progress: 85 },
    // { id: 10003, title: '任务3', start: '2024-03-06 10:30:00', end: '2024-03-10 14:10:30', progress: 90 },
    // { id: 10004, title: '任务4', start: '2024-03-12 11:00:50', end: '2024-03-19 15:30:10', progress: 75 },
    // { id: 10005, title: '任务5', start: '2024-03-18 12:30:00', end: '2024-03-28 18:30:00', progress: 100 },
    // { id: 10006, title: '任务6', start: '2024-03-26 14:12:10', end: '2024-04-06 20:30:10', progress: 60 }
  ]
})
</script>
