<template>
  <div class="flex h-screen">
    <div class="w-1/2 h-96 m-auto">
      <qrcode-stream @decode="decode" :track="drawOutline"></qrcode-stream>
    </div>
  </div>
</template>

<script>
import { QrcodeStream } from "vue3-qrcode-reader";

export default {
  components: {
    QrcodeStream,
  },

  methods: {
    decode(decodeString) {
      console.log(decodeString);
    },

    drawOutline(decodeData, ctx) {
      var points = [];

      for (var k in decodeData) {
        switch (k) {
          case "topLeftCorner":
            points[0] = decodeData[k];

            break;
          case "topRightCorner":
            points[1] = decodeData[k];

            break;
          case "bottomRightCorner":
            points[2] = decodeData[k];

            break;
          case "bottomLeftCorner":
            points[3] = decodeData[k];

            break;

          default:
            break;
        }
      }
      ctx.lineWidth = 10;
      ctx.strokeStyle = "green";
      ctx.beginPath();

      ctx.moveTo(points[0].x, points[0].y);

      for (const { x, y } of points) {
        ctx.lineTo(x, y);
      }

      ctx.lineTo(points[0].x, points[0].y);
      ctx.closePath();
      ctx.stroke();
    },
  },
};
</script>

<style></style>
