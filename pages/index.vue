<template>
<div>
  <canvas id="canvas" height="400" width="400" style="background-color:gray;"></canvas><br/>
	
  <v-file-input multiple label="画像を選択" @change="drawCanvas($event)"></v-file-input>

  <div id="result"></div>
</div>  
</template>

<script>

export default {
    methods: {
        drawCanvas(e) {
	    console.log(e[0])
            let fileData = e[0]
            if (!fileData.type.match('image.*')) {
                alert('画像を選択してください')
                return
            }
            let canvas = document.getElementById('canvas');
            let canvasWidth = 400;
            let canvasHeight = 400;
            canvas.width = canvasWidth;
            canvas.height = canvasHeight;
            let ctx = canvas.getContext('2d');

            let reader = new FileReader();
            let that = this;
            reader.onload = function() {
                let uploadImgSrc = reader.result;
                let img = new Image();
                img.src = uploadImgSrc;
                img.onload = function() {
		    //ctx.drawImage(img, 0, 0, canvasWidth, this.height * (canvasWidth / this.width));                    
		    ctx.drawImage(img, 100, 100, 200,200, 0,0,100,100)
		    ctx.drawImage(img, 0,0,100,100, 100, 100, 100,100 )
		    ctx.drawImage(img, 100,0,200,100, 100, 0, 100,100 )
                }
            }
            reader.readAsDataURL(fileData);
        }
    }
}

</script>
