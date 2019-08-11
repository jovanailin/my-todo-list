<template>
    <v-card rounded color="light-blue darken-1" max-width="800" class="mx-auto card" light>
        <v-container dark class="wrapper white--text">
            <v-layout wrap="nowrap">
                <v-toolbar class="white--text" flat min-width="800" color="orange accent-3">
                    <v-flex class="text-center">
                        <h1>MY TODO LIST</h1>
                    </v-flex>
                </v-toolbar>
                <v-card-title>
                    Tasks ({{doneTasks}})
                </v-card-title>
                <v-card-text>
                    <v-list v-for="(task, index) in tasks">
                        <v-list-item class="listitem">
                            <span :id="index">{{task.title}}</span>
                            <v-spacer></v-spacer>
                            <v-btn @click="check(task, index)" icon small class="text-center trash-btn" color="blue"><i :class="task.checkbox" class="task-icon"></i></v-btn>
                            <v-btn @click="remove(index)" icon small class="white--text text-center trash-btn" color="red"><i class="fas fa-trash-alt fa task-icon"></i></v-btn>
                            <v-btn @click="dialog=true" icon small class="white--text text-center trash-btn" color="green"><i class="fas fa-pencil-alt task-icon"></i></v-btn>

                            <v-dialog max-width="600px" v-model="dialog">

                                <v-card>

                                    <v-card-text>
                                        <v-text-field @keyup.enter="edit(index)" v-model="edited" label="edit task:"></v-text-field>
                                    </v-card-text>
                                    
                                    <v-layout id="submit" justify-center align-content-center> <v-btn dark color="orange accent-3" large @click="edit(index)">Submit</v-btn></v-layout>

                                   
                                </v-card>

 

                            </v-dialog>

                        </v-list-item>
                        <v-divider></v-divider>
                    </v-list>
                </v-card-text>
                <v-card-text wrap>
                    <v-list-item>
                        <v-text-field @keyup.enter="add" class="white--text" label="Add new task" v-model="task"></v-text-field>
                        <v-btn @click="add" icon small class="white--text text-center trash-btn" color="white"><i class="fas fa-plus task-icon"></i></v-btn>
                    </v-list-item>
                </v-card-text>
                <v-layout justify-space-around>
                    <v-btn @click="clearChecked()" class="clear-btn">Clear Checked</v-btn>
                    <v-btn @click="clearAll()" class="clear-btn">Clear All</v-btn>
                </v-layout>
            </v-layout>
        </v-container>
    </v-card>
</template>
<script>
    export default {
        data() {
            return {
                tasks: [],
                task: "",
                edited: "",
                dialog: false,
                edited: ""
            }
        },
        computed: {
            doneTasks() {
                var br = 0;
                for (var i = 0; i < this.tasks.length; i++) {
                    if (this.tasks[i].done == false) br++;
                }
                return br;
            },
        },
        methods: {
            add() {
                var title = this.task;
                var done = false;
                var checkbox = "far fa-square";
                var readonly = true
                this.tasks.push({
                    title,
                    done,
                    checkbox,
                })
                console.log(this.tasks);
                this.task = ""
            },
            check(t, i) {
                if (t.done == false) {
                    this.tasks[i].done = true;
                    this.tasks[i].checkbox = "far fa-check-square";
                    document.getElementById(i).classList.add("checked")
                    return;
                }
                if (t.done == true) {
                    this.tasks[i].done = false;
                    this.tasks[i].checkbox = "far fa-square";
                    document.getElementById(i).classList.remove("checked")
                    return;
                }
            },
            remove(i) {
                this.tasks.splice(i, 1);
            },
            edit(i) {

                this.tasks[i].title = this.edited;
                this.dialog = false;

            },
            change(i) {},
            clearChecked() {
                for (var i = 0; i < this.tasks.length; i++) {
                    if (this.tasks[i].done == true) {
                        this.tasks.splice(i, 1);
                        i--;
                    }
                }
                
                for(var i=0; i<this.tasks.length;i++){
                    if(this.tasks[i].done==true) document.getElementById(i).classList.add("checked")
                    else document.getElementById(i).classList.remove("checked")
                }
              
            },
            clearAll() {
                for (var i = 0; i < this.tasks.length; i++) {
                    this.tasks.splice(i, 1);
                    i--;
                }

            }
        }
    }

</script>
<style>
    .container {
        padding: 50px;
    }

    .card {
        margin: 50px
    }

    .wrapper {
        padding: 0
    }

    .listitem {
        padding: 10px;
        padding-bottom: 0;
    }

    .task-icon {
        padding: 0;
        font-size: 20px;
    }

    .trash-btn {
        padding: 0;
    }

    .clear-btn {
        margin: 10px;
    }

    .checked {
        text-decoration: line-through;
    }
    
    #submit {
        
        padding: 10px;
        width: 600px;
    }

</style>
