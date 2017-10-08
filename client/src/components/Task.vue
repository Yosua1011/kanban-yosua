<template>
   <div :class="taskType">
      <div class="panel-heading">
         <h3 class="panel-title">{{title}}</h3>
      </div>
      <div class="panel-body" v-for="(task, index) in tasks" :key="index">
         <div class="panel panel-default">
            <div class="panel-body">
               <h1>{{task.title}} </h1>
               <p>{{task.desc}}</p>
               <p>
                 <a class="btn btn-warning btn-xs" @click="backAction(task['.key'], task.status)" v-if="showBack">{{backBtn}}</a>
                 <a class="btn btn-info btn-xs" @click="nextAction(task['.key'], task.status)" v-if="showNext">{{nextBtn}}</a>
                 <a class="btn btn-danger btn-xs" @click="deleteAction(task['.key'], task.status)">Delete</a>
               </p>
            </div>
         </div>
      </div>
   </div>
</template>

<script>
export default {
  props: ['status', 'tasks'],
  data () {
    return {
      wishlistBtn: false,
      onProgressBtn: false,
      checkingBtn: false,
      finishBtn: false
    }
  },
  computed: {
    title () {
      switch (this.status) {
        case 'stat_0': return 'Wishlist'
        case 'stat_1': return 'On Progress'
        case 'stat_2': return 'Checking'
        case 'stat_3': return 'Finish'
      }
    },
    taskType () {
      switch (this.status) {
        case 'stat_0': return 'panel panel-danger'
        case 'stat_1': return 'panel panel-warning'
        case 'stat_2': return 'panel panel-info'
        case 'stat_3': return 'panel panel-success'
      }
    },
    nextBtn () {
      switch (this.status) {
        case 'stat_0': return 'On Progress'
        case 'stat_1': return 'Checking'
        case 'stat_2': return 'Finish'
      }
    },
    backBtn () {
      switch (this.status) {
        case 'stat_1': return 'Wishlist'
        case 'stat_2': return 'On Progress'
        case 'stat_3': return 'Checking'
      }
    },
    showNext () {
      if (this.status !== 'stat_3') {
        return true
      }
    },
    showBack () {
      if (this.status !== 'stat_0') {
        return true
      }
    }
  },
  methods: {
    nextAction (id, status) {
      let obj = {
        key: id,
        stat: status
      }
      this.$emit('nextAction', obj)
    },
    backAction (id, status) {
      let obj = {
        key: id,
        stat: status
      }
      this.$emit('backAction', obj)
    },
    deleteAction (id, status) {
      let obj = {
        key: id,
        stat: status
      }
      this.$emit('deleteAction', obj)
    }
  }
}
</script>

<style lang="css">
</style>
