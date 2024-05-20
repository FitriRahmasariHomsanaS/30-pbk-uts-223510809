<template>
  <div>
    <h1>Header</h1>
    <nav>
      <ul>
        <li>
          <button @click="selectedComponent = 'todos'" class="btn btn-primary" style="color: violet; font-weight: bold;">Todos</button>
        </li>
        <li>
          <button @click="selectedComponent = 'posts'" class="btn btn-primary" style="color: violet; font-weight: bold;">Posts</button>
        </li>
      </ul>
    </nav>
    
    <component :is="selectedComponent" />
  </div>
</template>

<script>
import Todos from './components/Todos.vue';
import Posts from './components/Posts.vue';

export default {
  components: {
    Todos,
    Posts
  },
  data() {
    return {
      selectedComponent: 'todos'
    };
  }
};
</script>

