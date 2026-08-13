<template>
  <div>
    <div style="margin-bottom: 8px;">
      <vxe-radio-group v-model="taskLinkConfig.lineWidth">
        <vxe-radio-button :checked-value="1" content="1px"></vxe-radio-button>
        <vxe-radio-button :checked-value="2" content="2px"></vxe-radio-button>
        <vxe-radio-button :checked-value="3" content="3px"></vxe-radio-button>
        <vxe-radio-button :checked-value="4" content="4px"></vxe-radio-button>
      </vxe-radio-group>
    </div>

    <vxe-gantt v-bind="ganttOptions"></vxe-gantt>
  </div>
</template>

<script lang="ts" setup>
import { reactive } from 'vue'
import { VxeGanttProps, VxeGanttPropTypes } from '../../../types'
import { VxeGanttDependencyType } from '../../../packages'

interface RowVO {
  id: number
  title: string
  start: string
  end: string
  progress: number
}

const taskLinkConfig = reactive<VxeGanttPropTypes.TaskLinkConfig>({
  lineWidth: 2 // 给所有线自定义宽度
})

const ganttOptions = reactive<VxeGanttProps<RowVO>>({
  border: true,
  height: 500,
  rowConfig: {
    keyField: 'id' // 行主键
  },
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
  // taskNowLineConfig: {
  //   mode: 'progress'
  // },
  taskViewConfig: {
    showNowLine: true,
    scales: [
      { type: 'month' },
      { type: 'date', step: 4 }
    ],
    tableStyle: {
      width: 480 // 表格宽度
    }
  },
  taskLinkConfig,
  links: [
    { from: 10001, to: 10002, type: VxeGanttDependencyType.FinishToFinish },
    { from: 10004, to: 10005, type: VxeGanttDependencyType.StartToStart },
    { from: 10005, to: 10006, type: VxeGanttDependencyType.FinishToStart }
  ],
  taskBarMoveConfig: {
    mode: 'progress',
    isSyncLinkTask: true
  },
  taskBarResizeConfig: {
    mode: 'progress'
  },
  columns: [
    { type: 'seq', width: 70 },
    { field: 'title', title: '任务名称' },
    { field: 'start', title: '开始时间', width: 100 },
    { field: 'end', title: '结束时间', width: 100 },
    { field: 'progress', title: '进度(%)', width: 80 }
  ],
  data: [
    { id: 10001, title: '任务1', start: '2026-07-27 08:30:00', end: '2026-08-04 12:30:00', progress: 50 },
    { id: 10002, title: '任务2', start: '2026-08-03 09:30:40', end: '2026-08-07 11:40:50', progress: 85 },
    { id: 10003, title: '任务3', start: '2026-08-06 10:30:00', end: '2026-08-10 14:10:30', progress: 90 },
    { id: 10004, title: '任务4', start: '2026-08-12 11:00:50', end: '2026-08-19 15:30:10', progress: 75 },
    { id: 10005, title: '任务5', start: '2026-08-18 12:30:00', end: '2026-08-28 18:30:00', progress: 100 },
    { id: 10006, title: '任务6', start: '2026-08-26 14:12:10', end: '2026-09-06 20:30:10', progress: 60 }
  ]
})
</script>
