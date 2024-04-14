<script setup lang="ts">
import { products } from "@/data";
</script>

<template>
  <div class="timeline-container">
    <div class="timeline" :style="{minWidth: `${products.length * 130}px` }">
      <div
        v-for="(item, i) in products"
        v-bind:key="item.型号"
        :style="{ left: i * 120 + 'px' }"
        class="timeline-year-indicator"
      >
        <div
          v-if="
            products[i - 1] &&
            item.发布时间?.substring(0, 4) !==
              products[i - 1]?.发布时间?.substring(0, 4)
          "
        >
          {{ item.发布时间?.substring(0, 4) }}
        </div>
        <div v-if="!products[i - 1]">
          {{ item.发布时间?.substring(0, 4) }}
        </div>
      </div>
      <div
        class="timeline-item"
        v-for="(item, i) in products"
        v-bind:key="item.型号"
        :style="{ left: i * 120 + 'px' }"
      >
        <div class="timeline-item-content">
          <p class="timeline-item-content-title" :title="item.品牌 + item.型号">{{ item.品牌 }} {{ item.型号 }}</p>
          <div class="timeline-item-content-subtitle">
            <span>{{ item.内存 }}+{{ item.硬盘 }}</span> 
            <span v-if="item.重量">, {{ item.重量 }}g</span></div>

          <span class="timeline-item-date">{{ item.发布时间 }}</span>
          <div class="timeline-item-meta">
            <span>{{ item.尺寸 }}"</span>
            <span>{{ item.整体尺寸 }}</span>
            <span style="margin-left: auto;" title="屏幕像素密度">{{ item.PPI }}</span>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.timeline-container {
  min-width: 1200px;
  height: 100vh;
  margin: auto;
  position: relative;

  --primary-color: #111;
}

.timeline {
  background: var(--primary-color);
  height: 10px;

  margin: 0 20px;

  margin-top: 50vh;
  transform: translateY(-50%);
  width: 100%;
}

.timeline-item {
  --line-height: 70px;
  --line-gap: 140px;

  position: absolute;
  top: calc(-1 * var(--line-gap));
  padding: 10px 12px;
  padding-bottom: 25px;
  border: 2px solid var(--primary-color);
  min-width: 150px;
}

.timeline-item-content {
  font-size: 14px;
}

.timeline-item-content .timeline-item-meta {
  position: absolute;
  bottom: -2px;
  background: var(--primary-color);
  width: 100%;
  left: 0;
  color: #fff;
  font-size: 10px;
  height: 18px;
  line-height: 18px;
  padding: 0 4px;
  display: flex;
  gap: 10px;
}

.timeline-item::after {
  content: "";
  position: absolute;
  width: 2px;
  height: var(--line-height);
  left: calc(50% - 1px);
  bottom: calc(-1 * var(--line-height));
  background: var(--primary-color);
}

.timeline-item:nth-child(2n) {
  top: unset;
  bottom: calc(-1 * var(--line-gap));
}

.timeline-item:nth-child(2n)::after {
  bottom: unset;
  top: calc(-1 * var(--line-height));
}

.timeline-item-date {
  font-size: 10px;
  color: #fff;
  position: absolute;
  background: var(--primary-color);
  top: -1.4em;
  padding: 0 4px;
  left: -2px;
}

.timeline-year-indicator {
  position: absolute;
  top: 0;
  left: 0;
  font-size: 8px;
  line-height: 10px;
  color: #fff;
}

.timeline-item:nth-child(2n) .timeline-year-indicator {
  top: calc(-1 * var(--line-gap) + 45px);
}

.timeline-item-content-title {
    max-width: 160px;
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
}

.timeline-item-content-subtitle {
    font-size: 10px;
}
</style>