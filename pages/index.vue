<template>
  <v-row justify="center" align="center">
    <v-col cols="12" sm="8" md="6">
      <v-card>
        <v-card-title class="headline"> Nuxt js Todo app </v-card-title>
        <v-card-text>
          <v-form @submit.prevent="addNewTodo">
            <v-text-field
              label="Add New Todo"
              ref="newTodo"
              v-model="newTodo"
            ></v-text-field>
            <v-btn block large @click="addNewTodo">Add New Todo List</v-btn>
            <div class="text-center">
              <v-btn class="ma-2" @click="markAllDone">Mark All Todo</v-btn>
              <v-btn class="ma-2" @click="removeAllTodo"
                >Remove All Todo List</v-btn
              >
              <v-btn class="ma-2" @click="removeSelectTodo"
                >Remove Select Todo List</v-btn
              >
            </div>
          </v-form>
          <v-list>
            <v-subheader>Todo List</v-subheader>
            <v-list-item v-for="(item, index) in TodoList" :key="item.id">
              <template v-slot:default="{ active }">
                <v-list-item-action>
                  <v-checkbox
                    v-model="item.active"
                    :input-value="item.active"
                    color="primary"
                    @click="toggleTodoDone(item)"
                  ></v-checkbox>
                </v-list-item-action>

                <v-list-item-content>
                  <v-list-item-title>{{ item.content }}</v-list-item-title>
                </v-list-item-content>
              </template>
            </v-list-item>
          </v-list>
        </v-card-text>
      </v-card>
    </v-col>
  </v-row>
</template>

<script>
export default {
  data() {
    return {
      TodoList: [],
      newTodo: '',
    }
  },
  mounted() {},
  methods: {
    addNewTodo() {
      this.$refs.newTodo.focus()
      this.TodoList.push({
        id: Date.now(),
        active: false,
        content: this.newTodo,
      })

      this.newTodo = ''
    },
    removeNewTodo_index(index) {
      this.$refs.newTodo.focus()
      this.TodoList.splice(index, 1)
    },

    removeAllTodo() {
      this.$refs.newTodo.focus()
      this.TodoList = []
    },

    removeSelectTodo() {
      //this.$refs.newTodo.focus()
      this.TodoList.forEach((item, index) => {
        if (item.active == true) {
          console.log(item)
          this.TodoList.splice(index, 1)
        }
      })
    },

    toggleTodoDone(item) {
      item.active = !item.active
      console.log(item.active)
    },

    markAllDone() {
      this.TodoList.forEach((item) => {
        item.active = true
      })
    },
  },
}
</script>
