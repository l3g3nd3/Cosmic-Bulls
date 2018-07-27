# Cosmic-Bulls

<html>
<style>
#nav_pane {
	float: left;
	width: 200px;
	margin: 1em;
}
#work_pane {
	float: left;
	margin: 1em;
}
#imageToSwap {
	height: 400px;
	width: 400px;
	position:relative;
	top:0px;
	left:0px;
}
#dlist {
	min-width:70%;
}
.marker {
	background-color: red;
	width: 10px;
	height:10px;
	position:absolute;
	border-radius: 5px;
}
</style>
<script src="https://code.jquery.com/jquery-3.3.1.min.js"></script>
<script>
function get_images() {
	return[
		"img/May08_03.05.02.bin_1_0.png",	"img/May08_05.53.51.bin_11_0.png",
		"img/May08_03.13.02.bin_2_0.png",	"img/May08_05.55.31.bin_12_0.png",
		"img/May08_03.15.02.bin_3_0.png",	"img/May08_05.57.01.bin_13_0.png",
		"img/May08_03.43.44.bin_4_0.png",	"img/May08_05.59.52.bin_14_0.png",
		"img/May08_04.32.27.bin_5_0.png",	"img/May08_06.09.02.bin_15_0.png",
		"img/May08_04.33.57.bin_6_0.png",	"img/May08_06.30.43.bin_16_0.png",
		"img/May08_04.36.57.bin_7_0.png",	"img/May08_07.08.55.bin_17_0.png",
		"img/May08_05.24.39.bin_8_0.png",	"img/May08_07.10.35.bin_18_0.png",
		"img/May08_05.31.00.bin_9_0.png",	"img/May08_07.13.35.bin_19_0.png",
		"img/May08_05.35.20.bin_10_0.png",	"img/May08_07.30.46.bin_20_0.png"
	];
}

function get_local_images() {
	var list = [];
	$("#imageToSwap").children().forEach(function(option) {
		list.push(option.value);
	})
}

var intervalId;
var posX, posY; // to get x and y positions for the json file

$(document).ready(function() {

	  var select = document.getElementById("dlist");
	  get_images().forEach(function(image, index){
			var opt = document.createElement('option');
	    opt.value = image;
	    opt.innerHTML = index+1;
	    select.appendChild(opt);
		});

    $("#dlist").change(	function () {
			$("#imageToSwap").css('background-image', 'url("' + $("#dlist").val() + '")');
		});

		$("#clear_all_markers").click(function() {
			$("#imageToSwap").children().remove(); // only allows you to add one marker
		});

		$("#imageToSwap").click(function (e) {
			if (!$("#dlist").val()) return;
			posX = $(this).position().left;
      posY = $(this).position().top;
			var marker = document.createElement('div');
			$(marker).attr('class', 'marker')
					.css('top', e.pageY - $(this).position().top - 5)
					.css('left', e.pageX - $(this).position().left - 5);
			this.appendChild(marker);

			$(marker).contextmenu(function(){
				// delete marker (=this)
 				$(marker).remove();
				return false;
			});
		});

		$("#forward_button").click(function (){
			var images = get_images();
			var idx = images.indexOf($("#dlist").val());
			$("#dlist").val(images[(idx + 1) % images.length]).change();
		});

		$("submit_button").click(function () {

		});

		$("#backward_button").click(function () {
			var images = get_images();
			var idx = images.indexOf($("#dlist").val());
			$("#dlist").val(images[(idx + images.length - 1) % images.length]).change();
		});

		$("#delete_image_button").click(function() {
			var images = get_images();
			var idx = images.indexOf($("#dlist").val());
			$("#forward_button").click();
			$("#dlist :nth-child(" + (idx+1) + ")").remove();
			//$("#dlist").val(images[idx]).splice(idx, 1);
		});

		$("#start_show").click(function() {
			intervalId = setInterval(function() {$("#forward_button").click()}, 500);
		});

		$("#end_show").click(function() {
			clearInterval(intervalId);
		});
});

</script>
			<script type= "text/javascript">
				var speed =4;	
				
				function showImage (src)
					{
						var div = document.createElement("div");
						with (div.style)
							{
								width = "300px";
								height = "300px";
								border = "2px solid black";
								textAlign = "center";
								overflow = "hidden";
							}
							
						document.body.appendChild(div);
						ing = document.createElement("ing");
						ing.width = 300;
						ing.height = 300;
						div.appendChild(ing);
					}
				function keyDown(key)
					{
						var k=0;
						if (key == 187) k=speed;
						if (key == 189) k=-speed;
						if (key != 0) 
							{
								ing.wigth = ing.width + k;
								ing.height = ing.height + k;
								ing.style.margin = ((300 - ing.height) / 2).toString() + "px";
							}
					}	
			</script>
					
	<body>
		 
		
			<div id="nav_pane">
				<select id="dlist" size="20">

				</select>
			</div>


			<div id="work_pane">
				 <div id="imageToSwap"></div>

				 <!-- <button id="IncrementOneImage" onClick="startImageSlideShow()" text="Move By One"> -->
	 			<input type="button" value="Forward One Image" id="forward_button" />
	 			<input type="button" value="Backward One Image" id="backward_button" />
	 			<input type="button" value="Start Slide Show" id="start_show" />
	 			<input type="button" value="Stop Slide Show" id="end_show" />
				<input type="button" value="Remove All Markers" id="clear_all_markers" />
				<input type="button" value="Submit" id="submit_button" />
				<input type="button" value="Delete Image" id="delete_image_button" />

			</div>
					
					
			<div img src = "C:\Users\Dell-PC\Downloads\Cosmic-Bulls\img" onmouseover = "C:\Users\Dell-PC\Downloads\Cosmic-Bulls\img" onmouseout = "C:\Users\Dell-PC\Downloads\Cosmic-Bulls\img"> 
			</div>

	</body>

</html>
