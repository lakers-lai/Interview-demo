<template>
  <div class="home">
    <h1 class="title">东门Locker</h1>
    <draggable v-model="boxes" class="locker-grid" :animation="200">
      <div 
        v-for="box in boxes" 
        :key="box.id" 
        class="locker-box"
        :class="{ 'size-l': box.size === 'L', 'size-m': box.size === 'M' }"
      >
        <div class="box-content">
          <div class="box-number">
            <i class="box-icon">📦</i>
            {{ box.number.padStart(3, '0') }}
          </div>
          <div :class="['box-status', box.status]">
            {{ getStatusText(box.status) }}
            <span v-if="box.progress" class="progress">{{ box.progress }}</span>
          </div>
        </div>
      </div>
    </draggable>
  </div>
</template>

<script>
import draggable from 'vuedraggable';

export default {
  name: 'Home',
  components: {
    draggable
  },
  data() {
    return {
      boxes: [
        { id: 1, number: '1', status: 'waiting', size: 'M' },
        { id: 2, number: '2', status: 'verifying', size: 'M', progress: '1/7' },
        { id: 3, number: '3', status: 'waiting', size: 'M' },
        { id: 4, number: '4', status: 'waiting', size: 'M' },
        { id: 5, number: '5', status: 'completed', size: 'L' },
        { id: 6, number: '6', status: 'waiting', size: 'L' },
        { id: 7, number: '7', status: 'completed', size: 'L' },
        { id: 8, number: '8', status: 'waiting', size: 'L' }
      ]
    }
  },
  methods: {
    getStatusText(status) {
      const statusMap = {
        waiting: '配備待ち',
        verifying: '検証進歩',
        completed: '完了'
      }
      return statusMap[status] || status
    }
  }
}
</script>

<style scoped>
.home {
  padding: 20px;
  background-color: #f5f5f5;
  min-height: 100vh;
}

.title {
  text-align: center;
  margin-bottom: 20px;
  font-size: 24px;
}

.locker-grid {
  display: flex;
  flex-wrap: wrap;
  flex-direction: row;
  align-items: flex-end;
  gap: 20px;
  padding: 0 10px;
  max-width: 600px;
  margin: 0 auto;
}

.locker-box {
  width: calc(50% - 10px);
  box-sizing: border-box;
  background: linear-gradient(145deg, #1a1a1a, #2a2a2a);
  border-radius: 12px;
  padding: 20px;
  position: relative;
  overflow: hidden;
  border: 2px solid #333;
  cursor: move;
  transition: transform 0.3s ease, opacity 0.3s ease;
  user-select: none;
  touch-action: none;
}

.locker-box.size-m {
  height: 100px;
}

.locker-box.size-l {
  height: 200px;
}

.box-content {
  height: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-between;
  color: white;
}

.box-number {
  font-size: 28px;
  display: flex;
  align-items: center;
  gap: 8px;
}

.box-icon {
  font-style: normal;
}

.box-status {
  background-color: rgba(255, 255, 255, 0.2);
  padding: 6px 12px;
  border-radius: 20px;
  font-size: 14px;
  width: fit-content;
  display: flex;
  align-items: center;
  gap: 8px;
}

.box-status.completed {
  background-color: #4CAF50;
}

.box-status.verifying {
  background-color: #FFA000;
  font-size:12px;
}

.box-status.waiting {
  background-color: rgba(255, 255, 255, 0.3);
}

.progress {
  background-color: rgba(0, 0, 0, 0.2);
  padding: 2px 8px;
  border-radius: 10px;
}

.locker-box:not(.dragging):hover {
  transform: scale(1.02);
  box-shadow: 0 2px 8px rgba(0,0,0,0.2);
}
</style> 