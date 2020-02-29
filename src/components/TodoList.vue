<style type="scss">
    .lineThrough {
        text-decoration: line-through;
    }

    h2 {
        text-align: center;
        margin: 10px 0;
        font-weight: bold;
    }
</style>
<template>
    <v-container class="todo-container">
        <h2 class="display-2  light-blue--text">todos</h2>
        <v-card class="mx-auto" max-width="600">
            <v-card-text>
                <v-list>
                    <v-list-item>
                        <v-list-item-content>
                            <v-form ref="form" v-on:submit="addItem">
                                <v-text-field v-model="taskForm" name="task" label="What need to be done?" prepend-inner-icon="mdi-plus" color="light-blue"></v-text-field>
                            </v-form>
                        </v-list-item-content>
                    </v-list-item>
                    <div v-for="item in items" :key="item.task">
                        <v-list-item>
                            <v-list-item-action>
                                <v-icon v-if="item.done" color="light-blue">mdi-check-circle-outline</v-icon>
                                <v-checkbox circle v-if="! item.done" v-model="item.done"
                                            color="light-blue"></v-checkbox>
                            </v-list-item-action>
                            <v-list-item-content @click="enableEditMode(item)">
                              <v-list-item-title v-bind:class="{ lineThrough: item.done }">{{item.task }}</v-list-item-title>
                            </v-list-item-content>
                            <v-list-item-action>
                                <v-icon @click="deleteTask(item.task)" color="red mx-2">mdi-trash-can</v-icon>
                            </v-list-item-action>
                        </v-list-item>
                        <v-divider></v-divider>
                    </div>
                </v-list>
            </v-card-text>
        </v-card>
    </v-container>
</template>

<script>
    export default {
        name: 'TodoList',
        methods: {
            addItem: function (event) {
                event.preventDefault();
                this.items.unshift({
                    task: this.taskForm,
                    done: false,
                })
            },
            deleteTask: function (task) {
                let self = this;
                this.items.forEach((val, idx) => {
                    if (task === val.task) {
                        self.items.splice(idx, 1);
                    }
                });
            },
        },
        data: () => ({
            taskForm: '',
            items: [
                {
                    task: 'take the dog out',
                    done: true,
                },
                {
                    task: 'finish writing your book',
                    done: true,
                },
                {
                    task: 'make a cake',
                    done: false,
                },
                {
                    task: 'kill someone',
                    done: false,
                },
                {
                    task: 'drink the coffee',
                    done: false,
                },
            ],
        }),
    }
</script>
