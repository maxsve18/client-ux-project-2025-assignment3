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

import carpenterIcon from '../assets/craftman/carpenter.svg'
import plumberIcon from '../assets/craftman/plumber.svg'
import electricianIcon from '../assets/craftman/electrician.svg'
import painterIcon from '../assets/craftman/painter.svg'
import masonIcon from '../assets/craftman/mason.svg'

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
  display: flex;
  flex-direction: column;
  width: 158px;
}

.worker-card {
  display: flex;
  flex-direction: row;
  align-items: center;
  border: 1px solid #9C9C9C;
  width: 100%;
  border-radius: 5px;
  background-color: #E2E2E2;
  font-size: 12px;
  margin-bottom: 10px;

  p {
    padding-left: 5px;
  }
}

.role-icon {
  position: absolute;
  left: 125px;
  transform: translateY(-11px);
}

.worker-card:nth-child(4n) {
  margin-bottom: 2rem;
}
</style>