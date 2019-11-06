<template>
  <div class="drag-container" v-drag-and-drop:options="options">
    <v-row class="ma-0">
      <v-col cols="4" v-for="group in groups" :key="group.id">
        <vue-draggable-group
          v-model="group.items"
          :groups="groups"
          :data-id="group.id"
        >
          <div class="drag-inner-list" :data-id="group.id">
            <v-card
              tile
              class="drag-item" v-for="item in group.items" :key="item.id" :data-id="item.id"
            >
              <v-list dense
              >
                <v-subheader>{{ item.name }}</v-subheader>
                <v-list-item-group color="primary" class="hidden__drap">
                  <v-list-item
                    v-for="(ite, i) in items"
                    :key="i"
                  >
                    <v-list-item-icon>
                      <v-icon v-text="ite.icon"></v-icon>
                    </v-list-item-icon>
                    <v-list-item-content>
                      <v-list-item-title v-text="ite.text"></v-list-item-title>
                    </v-list-item-content>
                  </v-list-item>
                </v-list-item-group>
              </v-list>
            </v-card>
          </div>
        </vue-draggable-group>
      </v-col>
    </v-row>
  </div>
</template>
<script>
export default {
  data() {
    return {
      groups: [
        {
          id: 1,
          name: "To Do",
          items: [
            { id: 1, name: "Item 1" },
            { id: 2, name: "Item 2" },
            { id: 3, name: "Item 3" }
          ]
        },
        {
          id: 2,
          name: "In Progress",
          items: [
            { id: 4, name: "Item 4" },
            { id: 5, name: "Item 5" },
            { id: 6, name: "Item 6" }
          ]
        },
        {
          id: 3,
          name: "Done",
          items: [
            { id: 7, name: "Item 7" },
            { id: 8, name: "Item 8" },
            { id: 9, name: "Item 9" },
            { id: 10, name: "Item 10" }
          ]
        }
      ],
      options: {
        dropzoneSelector: ".drag-inner-list",
        draggableSelector: ".drag-item",
        onDragstart(event) {
          this.collapsibleList();
        },
        onDrop(event) {
          this.expandList();
        },
        onDragend: function(event) {
          this.expandList();
        },
      },
      items: [
        { text: 'Real-Time', icon: 'mdi-clock' },
        { text: 'Audience', icon: 'mdi-account' },
        { text: 'Conversions', icon: 'mdi-flag' },
      ],
    };
  },
  methods: {
    collapsibleList() {
      setTimeout(() => {
        const item = document.getElementsByClassName("hidden__drap");
        for(let i=0;i<item.length;i++) {
          document.getElementsByClassName("hidden__drap")[i].style.display = "none";
        }
      }, 50);
     
    },
    expandList() {
      const item = document.getElementsByClassName("hidden__drap");
      for(let i=0;i<item.length;i++) {
        document.getElementsByClassName("hidden__drap")[i].style.display = "block";
      }
    }
  }
}
</script>
<style lang="scss">
.ma-0 {
  margin: 0;
}
.drag-inner-list {
  min-height: 70vh;
  .drag-item {
    margin-bottom: 12px;
    .v-list--dense {
      padding: 0;
    }
    .v-subheader {
      cursor: pointer;
      font-weight: bold;
    }
  }
}
@keyframes nodeInserted {
  from { opacity: 0.2; }
  to { opacity: 0.8; }
}

.item-dropzone-area {
  height: 2rem;
  background: #888;
  opacity: 0.8;
  animation-duration: 0.5s;
  animation-name: nodeInserted;
}

</style>

