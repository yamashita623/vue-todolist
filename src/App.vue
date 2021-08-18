<template>
  <div id="app">
    <h1>ToDoリスト</h1>
    <form>
      <label
        ><input type="radio" name="status" id="allLists" checked v-on:change='allLists'/>すべて</label
      >
      <label
        ><input type="radio" name="status" id="WorkingLists" v-on:change='workingLists'/>作業中</label
      >
      <label><input type="radio" name="status" id="doneLists" v-on:change='doneLists'/>完了</label>
    </form>

    <div>
      <table>
        <thead>
          <tr>
            <th>ID</th>
            <th>コメント</th>
            <th>状態</th>
          </tr>
        </thead>
        <tbody>
    <tr v-for="list in lists" :key="list.id">
     
        <th>{{ list.id }}</th>
        <th>{{ list.body }}</th>
            <th><button @click="doChangeState(list.id)">
              {{ list.state }}
            </button></th>         
        <th><button @click="doDeleteList(list.id)">削除</button></th>
     
    </tr>

    <tr>"{{ allLists }}"</tr>
    <tr>"{{ workingLists }}"</tr>
    <tr>"{{ doneLists }}"</tr>
    </tbody>
    </table>
    <div>
      <h2><label for="body">新規タスクの追加</label></h2><br>
      <textarea v-model="body"></textarea>
      <input type="submit" value="追加" @click="addList(lists.id)" />
    </div>
  </div>
   </div>
</template>

<script>
export default {
  data: () => ({
    id: 0,
    lists: [],
    body: '',
    state: '',
    show: 0,
  }),
   computed: { 
          workingLists:function() {
      return this.lists.filter(    
                function (value) {
                  return value.state === '作業中'
                })},
                allLists:function() {
      return this.lists.filter(    
                function (value) {
                  return value.state === '作業中'||'完了'
                })},
                doneLists:function() {
      return this.lists.filter(    
                function (value) {
                  return value.state === '完了'
                })}},
  
  methods: {
    addList: function () {
      if (this.body === '') return;
      this.lists.push({id: this.lists.length, body: this.body, state: this.state = '作業中', });
      this.body = '';
    },
    doChangeState: function (id) {
      for (let list of this.lists) {
            if (list.id === id) {
              if (list.state === '作業中') {
                return list.state = '完了'
              } else {
                return list.state = '作業中'
              }
            }
          }},
        doDeleteList: function (id) {
      if (id > -1) {
        this.lists.splice(id,1);
        this.lists.forEach((lists, index) => {
          lists.id = index;
        });
      }},
     
}};
</script>
