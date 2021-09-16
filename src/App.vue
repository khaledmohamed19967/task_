<template>
  <div id="app">
    <div class="wrapper row m-0">
      <!-- list sidebar -->
      <div class="list col-md-3 col-lg-2 p-0">
        <div class="search">
          <div class="input_">
            <b-form-input placeholder="Search Component"></b-form-input>
          </div>
        </div>

        <!-- message -->
        <div  class="list_wrapper">
          <p class="list_title">Message</p>
          <draggable v-model="message"
                     :group="{ name: 'universalGroup', pull: 'clone', put: false }"
                     @start="drag=true" @end="drag=false">
            <div class="list_drag"v-for="element in message" :key="element.id" :class="element.color">
              <b-icon :icon="element.icon"></b-icon>  {{element.name}}
            </div>
          </draggable>
        </div>
        <!-- end message -->

        <!-- Voice -->
        <div  class="list_wrapper">
          <p class="list_title">Voice</p>
          <draggable v-model="voice"
                     :group="{ name: 'universalGroup', pull: 'clone', put: false }"
                     @start="drag=true" @end="drag=false">
            <div class="list_drag"v-for="element in voice" :key="element.id" :class="element.color">
              <b-icon :icon="element.icon"></b-icon>  {{element.name}}
            </div>
          </draggable>
        </div>
        <!-- end voice -->

        <!-- Function -->
        <div  class="list_wrapper">
          <p class="list_title">Function</p>
          <draggable v-model="function_list"
                     :group="{ name: 'universalGroup', pull: 'clone', put: false }"
                     @start="drag=true" @end="drag=false">
            <div class="list_drag"v-for="element in function_list" :key="element.id" :class="element.color">
              <b-icon :icon="element.icon"></b-icon>  {{element.name}}
            </div>
          </draggable>
        </div>
        <!-- end function -->

      </div>
      <!-- end list of sidebar -->

      <!-- start the board -->
      <div class="board col-md-9 col-lg-10 p-0">
        <draggable class="draggable"
               v-model="board"  @start="drag=false" @end="drag=false"
                   :group="{ name: 'universalGroup', pull: false, put: true }"
        >
          <b-card
              class="drag_box"v-for="(element,index) in board" :key="element.id"
              :class="element.color"
              footer-tag="footer"
          >
            <b-card-text>{{element.value}}.</b-card-text>
            <template #header>
              <div class="header_wrapper">
                <div>{{ index === 0 ? 'start' : element.name }}</div>
                <div v-if="index >= 1" @click="deleteBox(index)"><b-icon style="cursor: pointer" icon="x"></b-icon></div>
              </div>
            </template>
            <template #footer>
              <div class="action_wrapper">
                <div v-for="el in element.action"><button>{{ el }}</button></div>
              </div>
            </template>
          </b-card>
        </draggable>
      </div>
      <!-- end the board -->
    </div>
    </div>
</template>

<script>
import draggable from 'vuedraggable'
export default {
  components: {draggable},
  data:() => ({
    message:[
      {
        name: 'Sent SMS',
        icon: 'chat-dots',
        color: 'blue',
        action: ["Incoming SMS","Incoming Call","API Request"]
      }
    ],
    voice: [
      {
        name: 'Call Action',
        icon: 'telephone-outbound',
        color: 'purple',
        value: '0158xx-xxx-x',
        action: ["Answered","Not Answered","Busy/Rejected","Failed"],

      },
      {
        name: 'Get Input Action',
        icon: 'grid-3x3-gap',
        color: 'purple',
        value: 'Get user input',
        action:["No Input","Wrong Input","1", "2"]
      },
      {
        name: 'Play Sound Audio',
        icon: 'soundwave',
        color: 'purple',
        value: 'https://palceholder-testsound.com',
        action:["Prompt complate"]
      },
    ],
    function_list: [
      {
        name: 'HTTP Request',
        icon: 'chat-dots',
        color: 'orange',
      },
      {
        name: 'Counter  ',
        icon: 'chat-dots',
        color: 'orange',
      },
      {
        name: 'Bransh',
        icon: 'chat-dots',
        color: 'orange',
      }
    ],
    board: [
      {
        name: 'Start from this node',
        icon: 'chat-dots',
        color: 'green',
        value: 'Start from here',
        action: ["Incoming SMS","Incoming Call","API Request"],
      },
    ],
  }),
  methods: {
    /** methods invoke to delete box from board **/
    deleteBox(index) {
        this.board.splice(index, 1);
    }
  }
}
</script>

