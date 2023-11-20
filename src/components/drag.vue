<template lang="">
    <div>
        <div
            class="draggable"
            @mousedown="startDrag"
            @touchstart="startDrag"
            @mousemove="onDrag"
            @touchmove="onDrag"
            @mouseup="stopDrag"
            @touchend="stopDrag"
            @mouseleave="stopDrag"
        >
            <svg class="bg" width="320" height="560">
                <path :d="headerPath" :fill="'#3F51B5'"></path>
            </svg>
            <div class="header">Drag Me</div>
            <div class="content" :style="contentPosition">Hello</div>
        </div>
    </div>
</template>
<script>
import { reactive, computed } from 'vue'
import dynamics from 'dynamics.js'

export default {
    setup() {
    const headerHeight = 120

    let isDragging = false
    const start = { x: 0, y: 0 }
    const c = reactive({ x: headerHeight, y: headerHeight })

    const headerPath = computed(() => {
    return `M0,0 L320,0 320,${headerHeight}Q${c.x},${c.y} 0,${headerHeight}`
    })
    const contentPosition = computed(() => {
    const dy = c.y - headerHeight
    const dampen = dy > 0 ? 2 : 4
        return {
            transform: `translate(0,${dy / dampen}px)`
        }
    })
        function startDrag(e) {
        e = e.changedTouches ? e.changedTouches[0] : e
        isDragging = true
        start.x = e.pageX
        start.y = e.pageY
        }
        function onDrag(e) {
        e = e.changedTouches ? e.changedTouches[0] : e
        if (isDragging) {
                c.x = headerHeight + (e.pageX - start.x)
                const dy = e.pageY - start.y
                const dampen = dy > 0 ? 1.5 : 4
                c.y = headerHeight + dy / dampen
            }
        }
        function stopDrag() {
            if (isDragging) {
                isDragging = false
                dynamics.animate(
                c,
                { x: headerHeight, y: headerHeight },
                { type: dynamics.spring, duration: 700, friction: 280 }
                )
            }
        }  
        return {
            headerPath,
            contentPosition,
            startDrag,
            onDrag,
            stopDrag,
      };
    }
}
</script>
<style scoped>
.draggable {
  background-color: #fff;
  box-shadow: 0 4px 16px rgba(0, 0, 0, 0.15);
  width: 320px;
  height: 240px;
  overflow: hidden;
  margin: 30px auto;
  position: relative;
  text-align: center;
  font-size: 14px;
  font-weight: 300;
  user-select: none;
  border-radius: 8px;
}
.bg {
  position: absolute;
  top: 0;
  left: 0;
  z-index: 0;
}
.header,
.content {
  position: relative;
  z-index: 1;
  padding: 30px;
  box-sizing: border-box;
}
.header {
  color: #fff;
  height: 120px;
  font-size: 2em;
  font-weight: bold;
}
</style>
