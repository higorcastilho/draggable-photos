<template>
  <div>
<!--     <div class='drop-zone' @drop="onDrop($event, 1)" @dragover.prevent @dragenter.prevent>
      <div v-for='item in listOne' :key='item.title' class='drag-el' draggable @dragstart='startDrag($event, item)'>
        {{ item.title }}
      </div>
    </div>
    <div class='drop-zone' @drop="onDrop($event, 2)" @dragover.prevent @dragenter.prevent>
      <div v-for='item in listTwo' :key='item.title' class='drag-el' draggable @dragstart='startDrag($event, item)'>
        {{ item.title }}
      </div>
    </div> -->
    <div class="mt-10" style=" width: 80%; height: 200px; margin: 0 auto">
      <v-row>
        <div 
          @dragover.prevent 
          @dragenter.prevent
          style="background: pink; border: 1px solid #000000;" 
          v-for="(foto, index) in fotos" 
          :key="foto.id" 
          cols="4"
          @dragenter = "onDragEnter(index)"
          @drop="onDrop"
        >
          <div 
            @dragstart="onDragStart($event, foto.position, index)" 
            :draggable="true" 
            style="width: 100px; height: 100px; background: steelblue; "
          >
            <p class="text-align-center">{{ foto.nome }}</p>
          </div>
        </div> 
      </v-row>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'HelloWorld',

    data() {
      return {
        itemArrastado: 0,
        taEmCima: 0,
        substituir: true,
        fotos: [
          { id: 0, nome: 'foto 0', src:'', position: 0 },
          { id: 1, nome: 'foto 1', src:'', position: 4 },
          { id: 2, nome: 'foto 2', src:'', position: 2 },
          { id: 3, nome: 'foto 3', src:'', position: 3 },
          { id: 4, nome: 'foto 4', src:'', position: 1 },
          { id: 5, nome: 'foto 5', src:'', position: 5 },
          { id: 6, nome: 'foto 6', src:'', position: 6 },
          { id: 7, nome: 'foto 7', src:'', position: 7 },
          { id: 8, nome: 'foto 8', src:'', position: 8 }
        ],

        // items: [
        // {
        //   id: 0,
        //   title: 'Item A',
        //   list: 1
        // },
        // {
        //   id: 1,
        //   title: 'Item B',
        //   list: 1
        // },
        // {
        //   id: 2,
        //   title: 'Item C',
        //   list: 2
        // }]
      }
    },


    methods: {

      sortFotos () {
        this.fotos.sort((a, b) => {
          if (a.position > b.position) return 1;
          if (a.position < b.position) return -1;
          return 0;
        })  
      },

      onDragStart (event, fotoPosition) {
        event.dataTransfer.dropEffect = 'move';
        event.dataTransfer.effectAllowed = 'move';
        this.itemArrastado = fotoPosition;

      },
      onDragEnter(taEmCima) {
        this.taEmCima = taEmCima;
        console.log(this.itemArrastado, this.taEmCima)

        this.fotos[this.itemArrastado].position = taEmCima + 0.2
        this.fotos[this.itemArrastado].position = Math.floor(this.fotos[this.itemArrastado].position)
        this.sortFotos();
        console.log(this.fotos) 
      },
      onDrop() {
        this.sortFotos();
      }
      // onDrop () {
      //   const itemArrastadoObjeto = this.fotos[this.itemArrastado]
      //   this.fotos.forEach((item, index) => {
      //     if (index === 0) {
      //       return ''
      //     } else if (index <= this.taEmCima && this.substituir) {
      //       this.fotos.splice(this.taEmCima + 1, 0, itemArrastadoObjeto)
      //       //this.fotos.splice(this.taEmCima + 1, 1)
      //       this.substituir = false;
      //     }
      //   })

      //   this.fotos.splice(this.itemArrastado, 1, this.fotos[this.taEmCima])
      // }
      // startDrag (event, item) {
      //   event.dataTransfer.dropEffect = 'move';
      //   event.dataTransfer.effectAllowed = 'move';
      //   event.dataTransfer.setData('itemID', item.id);
      // },

      // onDrop (event, list) {
      //   const itemID = event.dataTransfer.getData('itemID');
      //   const item = this.items.find(item => item.id == itemID);
      //   item.list = list
      // }
    },

    computed: {
      listOne () {
        return this.items.filter(item => item.list === 1);
      },
      listTwo () {
        return this.items.filter(item => item.list === 2);
      }
    },
    created() {
      this.sortFotos();
    }
  }
</script>
<style scoped>
  .drop-zone {
    background-color: #eee;
    margin-bottom: 10px;
    padding: 10px;
  }

  .drag-el {
    background-color: #fff;
    margin-bottom: 10px;
    padding: 5px;
  }
  
</style>
