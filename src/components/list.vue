<template>
    <div>
      <input v-model="query" />
      <div class="box">
  
        <TransitionGroup
          tag="ul"
          :css="false"
          @before-enter="onBeforeEnter"
          @enter="onEnter"
          @leave="onLeave"
        >
          <li v-for="(item, index) in computedList" :key="item.msg" :data-index="index">
            {{ item.msg }}
          </li>
        </TransitionGroup>
      </div>
    </div>
  </template>
  
  <script>
  import { ref, computed } from 'vue';
  import gsap from 'gsap';
  
  export default {
    setup() {
      const list = [
        { msg: 'Ahmet Yılmaz' },
        { msg: 'Ayşe Demir' },
        { msg: 'Mustafa Kaya' },
        { msg: 'Zeynep Yıldırım' },
        { msg: 'Canberk Cartel' },
        { msg: 'Seda Doğan' },
        { msg: 'Mustafa Çelik' },
        { msg: 'Şeref Orkun Öztunç' },
        { msg: 'Mehmet Aksoy' },
        { msg: 'Elif Çetin' },
        { msg: 'Umut Bulut' },
        { msg: 'Gamze Taş' },
        { msg: 'Kaan Şahin' },
        { msg: 'Şeyma Güneş' },
        { msg: 'Onur Kurt' },
        { msg: 'Ebru Kılıç' },
        { msg: 'Can Günebakan' },
        { msg: 'Zehra Yılmaz' },
        { msg: 'Ali Karahan' },
        { msg: 'Begüm Kocaman' },
        { msg: 'Volkan Turan' },
        { msg: 'Nazlı Erdoğan' },
        { msg: 'Berkecan Özbek' },
        { msg: 'Nur Çelik' },
        { msg: 'Murat Sarıgül' },
        { msg: 'Esra Arslan' },
        { msg: 'Fahrettin Baştürk' },
      ];
  
      const query = ref('');
  
      const computedList = computed(() => {
        return list.filter((item) => item.msg.toLowerCase().includes(query.value));
      });
  
      function onBeforeEnter(el) {
        el.style.opacity = 0;
        el.style.height = 0;
      }
  
      function onEnter(el, done) {
        gsap.to(el, {
          opacity: 1,
          height: '2em', // Increased height for a bit more space
          padding: '0.5em',
          borderBottom: '1px solid #ddd', // Adding a border between items
          delay: el.dataset.index * 0.15,
          onComplete: done,
        });
      }
  
      function onLeave(el, done) {
        gsap.to(el, {
          opacity: 0,
          height: 0,
          padding: 0,
          borderBottom: 'none',
          delay: el.dataset.index * 0.15,
          onComplete: done,
        });
      }
  
      // Return variables and functions for template
      return {
        query,
        computedList,
        onBeforeEnter,
        onEnter,
        onLeave,
      };
    },
  };
  </script>
  
  <style scoped>
  .box {
    display: flex;
    flex-direction: column;
  }
  
  .box li {
    flex: 1;
    list-style: none; /* Remove default list style */
    margin: 0; /* Remove default margin */
    background-color: #f9f9f9; /* Light background color */
  }
  </style>
  