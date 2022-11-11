<template>
  <div class="container" >
    <canvas  
    class="card"
    :draggable="draggable"
    @dragstart="dragStart"
    @dragover.stop 
    id="canvas" width="500" height="500"></canvas>
  </div>
</template>

<script>
export default {
  props: ['id', 'draggable'],
  data: () => ({
    CX: 250,
    CY: 250,
    SLICES_COUNT: 8,
    RADIUS: 150,
    MAX_DISTANCE: 0.15,
    MAXRAD: Math.PI * 2, // 360 º
    PEPPERONI_SIZE: 56,
    PEPPERONI_RADIUS: 15,

    BORDER_COLOR: "#f2d28c",
    CHEESE_COLOR: "#ffffbc",
    PEPPERONI_COLOR: "#ee4400",

    canvas: document.getElementById("canvas"),
    canvas: null,
    context: null,

    vueCanvas:null
  }),

  mounted() {
 
    this.context= canvas.getContext("2d")
    // this.pepperoni();
    //this.drawPie();
    this.drawSlices();
  },


  methods: {
    pepperoni() {
      this. canvas = document.createElement("canvas");
      this.canvas.width = this.PEPPERONI_SIZE;
      this.canvas.height = this.PEPPERONI_SIZE;

      let context = this.canvas.getContext("2d");
      context.fillStyle = this.CHEESE_COLOR;
      context.fillRect(0, 0, this.PEPPERONI_SIZE, this.PEPPERONI_SIZE);

      let cords = [
        [0, 0],
        [canvas.width, 0],
        [canvas.width / 2, canvas.height / 2],
        [0,canvas.height],
        [canvas.width, this.canvas.height],
      ];

      context.fillStyle = this.PEPPERONI_COLOR;

      cords.forEach(function (cord) {
        var x = cord[0];
        var y = cord[1];
        context.moveTo(x, y);
        //context.arc(x, y, this.PEPPERONI_RADIUS, 0, this.MAXRAD, 0);
        context.fill();
      });

      return context.createPattern(this.canvas, "repeat");
    },

    drawPie(x, y, r, starts, ends, color) {
      this.context.beginPath();
      this.context.fillStyle = color;
      this.context.moveTo(x, y);
      this.context.arc(x, y, r, starts, ends, 0);
      this.context.fill();
    },

    drawSlices() {
      for (var index = 0; index < this.SLICES_COUNT; index++) {
        let sliceSize = this.MAXRAD / this.SLICES_COUNT;
        let fromRadians = this.MAXRAD * (index / this.SLICES_COUNT);
        let toRadians = fromRadians + sliceSize;
        let halfRadians = fromRadians + sliceSize / 2;
        let distance = this.RADIUS * Math.random() * this.MAX_DISTANCE;
        let cx = distance * Math.cos(halfRadians) + this.CX;
        let cy = distance * Math.sin(halfRadians) + this.CY;

        this.drawPie(cx, cy, this.RADIUS, fromRadians, toRadians, this.BORDER_COLOR);
        this.drawPie(cx, cy, this.RADIUS * 0.85, fromRadians, toRadians, this.pepperoni);
      }
    },
    dragStart: e => {
      const target = e.target;
      e.dataTransfer.setData('card_id',target.id);

      setTimeout(()=>{
        target.style.display = "none";
      },0);
    }

  },
};
</script>
