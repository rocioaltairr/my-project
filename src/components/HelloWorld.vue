<template>
  <div class="hello">
    <div class="left">
      <h1>{{ title }}</h1>
      <form @submit.prevent="addLink">
        <input class="link-input" type="text" placeholder="Add a Link" v-model="newLink" />
      </form>
      <ul>
        <li v-for="(link, index) in links" v-bind:key="index">
          {{ link }}
          <button v-on:click="removeLinks(index)" class="rm">Remove</button>
        </li>
      </ul>
    </div>
    <div class="right">
      <stats />
    </div>
  </div>
</template>
<script>
  import stats from '@/components/stats.vue'
  import {
    mapState,
    mapMutations,
    mapActions
  } from 'vuex'

  export default {
    name: 'HelloWorld',
    data() { // Add this:
      return {
        newLink: ''
      }
    },
    components: {
      stats
    },
    computed: mapState([
      'title',
      'links'
    ]),
    methods: { // Add this:
      ...mapMutations([
        'ADD_LINK'
      ]),
    ...mapActions([                  // Add this
      'removeLink'
    ]),
      addLink: function () {
        this.ADD_LINK(this.newLink)
        this.newLink = ''
      },
      removeLinks: function (link) { // Add this
        this.removeLink(link)
      }
    }
  }
</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  h3 {
    margin: 40px 0 0;
  }

  ul {
    list-style-type: none;
    padding: 0;
  }

  li {
    display: inline-block;
    margin: 0 10px;
  }

  a {
    color: #42b983;
  }

  .hello {
    display: flex;
  }

  .right {
    width: 50%;
    background: #bcdac8;
  }

  .left {
    background: #d9f7e5;
    width: 50%;
  }

  ul {
    display: flex;
    flex-direction: column;
    align-items: center;
  }

  li {
    background: aliceblue;
    width: 50%;
    padding: 10px;
    margin: 5px;
  }
  
</style>