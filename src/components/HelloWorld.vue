<template>
  <div class="board-layout">
    <div id="boardlists" class="board-lists">
      <div id="list1" class="board-list" @drop="dropIt($event)" @dragover="allowDrop($event)">
        <div v-for="item in items" :key="item.id" :id="`card${item.id}`" class="card" draggable="true" @dragstart="dragStart($event)">
          <img style="width: 100px; height: 100px; object-fit: cover" :src="item.src" />
        </div>
      </div>
    </div>  
  </div>
</template>

<script>
  export default {
    name: 'HelloWorld',

    data() {
      return {
        items: [
          {
            id: 0,
            src: "https://www.galeriadaarquitetura.com.br/Img/projeto/702x415/5651/casa-113917.jpg" 
          },
          {
            id: 1,
            src: "https://www.imperialseguros.com/wp-content/uploads/2020/06/leve-e-iluminada-esta-casa-na-bahia-mistura-estrutura-metalica-madeira-e-vidro_9.jpg" 
          },
          {
            id: 2,
            src: "https://fotos.vivadecora.com.br/decoracao-casas-modernas-teto-revestido-com-madeira-e-ilha-com-grama-verde-revistavd-185763-proportional-height_cover_medium.jpg" 
          },
          {
            id: 3,
            src: "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRPDwJoSodBQBTnORcxszcppBaOnY38E9ItG4xSlRMNd9PJnaNLrTZVo3wkC7WsJKptMXw&usqp=CAU" 
          }
        ]
      }
    },
    methods: {
      allowDrop(ev) {
        ev.preventDefault();  // default is not to allow drop
      },
      dragStart(ev) {
        // The 'text/plain' is referring the Data Type (DOMString) 
        // of the Object being dragged.
        // ev.target.id is the id of the Object being dragged
        ev.dataTransfer.setData("text/plain", ev.target.id);
      },
      dropIt(ev) {
        ev.preventDefault();  // default is not to allow drop
        let sourceId = ev.dataTransfer.getData("text/plain");
        let sourceIdEl=document.getElementById(sourceId);
        
        // ev.target.id here is the id of target Object of the drop
        let targetEl=document.getElementById(ev.target.id)
      

            // Same list. Swap the text of the two cards
            // Just like swapping the values in two variables
          
            // Temporary holder of the destination Object
            let holder=targetEl;
            // The text of the destination Object. 
            // We are really just moving the text, not the Card
            let holderSrc=holder.childNodes[0].src;
            let holderId = holder.id;

            // Replace the destination Objects text with the sources text
            targetEl.childNodes[0].src=sourceIdEl.childNodes[0].src;
            targetEl.id=sourceIdEl.id;
            // // Replace the sources text with the original destinations
            sourceIdEl.childNodes[0].src=holderSrc;
            sourceIdEl.id=holderId;
            
            holderSrc=''
            holderId=''


            const DOMPhotosList = document.getElementById('list1').childNodes
            const elements = Object.values(DOMPhotosList)
            const sortedPhotos = elements.map(item => item.id.replace(/\D/g, '') )

            console.log(sortedPhotos);
      }
    },
  }
</script>
<style scoped>
  .board-layout {
    background-color: rgb(100, 92, 165);
    font-family: Arial, Helvetica, sans-serif;
    font-size: 15px;
    display: grid;
    grid-template-rows: max-content auto;
    grid-gap: 10px;
    padding: 10px;
    height:800px;
  }
.list-layout {
    display: grid;
    grid-gap: 10px;
   
  }
.board-text {
    font-weight: bold;
    font-size: 28px;
    padding: 5px;
  }
.board-lists {
    display: flex;
    grid-auto-columns: 275px;
    grid-auto-flow: column;
    grid-gap: 10px;
    height: 200px;
 
  }
  
  .board-list {
    background-color: rgb(235, 236, 240);
    border-radius: 3px;
    display: flex;
    flex-wrap: wrap;
    grid-auto-rows: max-content;
    grid-gap: 10px;
/* Chrome use a fixed height */
    height: 400px;
    padding: 10px;
    width: 400px;
  }
  
  .list-title {
    font-size: 18px;
    font-weight: bold;
  }
.card {
    background-color: white;
    border-radius: 3px;
    box-shadow: 0 1px 0 rgba(9,30,66,.25);
    padding: 10px;
    cursor:pointer;
  }
</style>