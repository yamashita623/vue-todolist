<template>
  <div id='app'>
    <h1>ToDoリスト</h1>
    <form>
      <label
        ><input
          type='radio'
          name='status'
          checked
          @click="doChangeLists('allLists')"
        />すべて</label
      >
      <label
        ><input
          type='radio'
          name='status'
          @click="doChangeLists('workingLists')"
        />作業中</label
      >
      <label
        ><input 
        type='radio' 
        name='status' 
        @click="doChangeLists('doneLists')"
        />完了</label
      >
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
          <tr v-for='list in computedTodos' :key='list.id'>
            <th>{{ list.id }}</th>
            <th>{{ list.body }}</th>
            <th>
              <button @click='doChangeState(list.id)'>
                {{ list.state }}
              </button>
            </th>
            <th><button @click='doDeleteList(list.id)'>削除</button></th>
          </tr>
        </tbody>
      </table>
      <div>
        <h2><label for='body'>新規タスクの追加</label></h2>
        <br />
        <textarea v-model='body'></textarea>
        <input type='submit' value='追加' @click='addList(lists.id)' />
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data: () => ({
    lists: [],
    show: 'allLists',
    body: '',
  }),

  computed: {
    computedTodos() {
      const list = this.lists;
      if (this.show === 'allLists') return list;
      else if (this.show === 'workingLists')
        return list.filter((e) => e.state === '作業中');
      else return list.filter((e) => e.state === '完了');
    }
  },

  methods: {
    addList: function () {
      if (this.body === '') return;
      this.lists.push({
        id: this.lists.length,
        body: this.body,
        state: (this.state = '作業中'),
      });
      this.body = '';
    },
    doChangeState: function (id) {
      for (let list of this.lists) {
        if (list.id === id) {
          if (list.state === '作業中') {
            return (list.state = '完了');
          } else {
            return (list.state = '作業中');
          }
        }
      }
    },
    doDeleteList: function (id) {
      if (id > -1) {
        this.lists.splice(id, 1);
        {
          this.lists.forEach((lists, index) => {
            lists.id = index;
          });
        }
      }
    },
    doChangeLists: function (val) {
      if (val === 'allLists')
          return this.show = 'allLists';
          else if (val === 'workingLists')
            return this.show = 'workingLists';
            else return this.show = 'doneLists';
      }
  }
};
</script>