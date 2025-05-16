<template>
  <div class="worker-list">
    <div v-for="worker in workers" :key="worker.name" class="worker-card">
      <p>{{ worker.name }}</p>
      <div class="icons">
        <img
            v-for="role in worker.role"
            :key="role"
            :src="roleIcons[role]"
            :alt="role + ' icon'"
            class="role-icon"
        />
      </div>
    </div>
  </div>
</template>

<script setup>
import {workers} from '../data/workers.js';

import carpenterIcon from '../assets/craftman/carpenter.svg?url'
import plumberIcon from '../assets/craftman/plumber.svg?url'
import electricianIcon from '../assets/craftman/electrician.svg?url'
import painterIcon from '../assets/craftman/painter.svg?url'
import masonIcon from '../assets/craftman/mason.svg?url'

const roleIcons = {
  carpenter: carpenterIcon,
  plumber: plumberIcon,
  electrician: electricianIcon,
  painter: painterIcon,
  mason: masonIcon
};

</script>

<style>

.worker-list {
  margin-top: 15px;
  display: flex;
  flex-direction: column;
  width: 173px;
}

.worker-card {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  border: 1px solid #9C9C9C;
  height: 26px;
  width: 100%;
  border-radius: 5px;
  background-color: #F6F6F6;
  font-size: 12px;
  margin-bottom: 10px;
  cursor: pointer;
  p {
    align-self: center;
    padding-left: 5px;
  }
}

.role-icon {
  position: relative;
  transform: translateY(3px);
}

.icons:last-child {
  margin-right: 6px;
}

.worker-card:nth-child(4n) {
  margin-bottom: 2rem;
}
</style>