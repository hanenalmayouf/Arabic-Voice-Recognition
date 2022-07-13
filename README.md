# Arabic-Voice-Recognition
<!DOCTYPE html>
<html lang="ar">
<head>
    <title>التعرف التلقائي على الكلمات </title>
    <meta charset="UTF-8">
    <script type="text/javascript" src="autoUpdate.js"></script>
		<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.6.0/jquery.min.js"></script>

</head>
<style>
.hidden{
	display:none;
	
}

</style>
<bodyid="full">
<div id="liveData" style="display: none;">
    <p>Loading Data...</p>
</div>



<audio id="audio">
	<source  id="sound" src="1.mp3" type="audio/mp3">
</audio>

<audio id="audio2">
	<source  id="sound" src="2.mp3" type="audio/mp3">
</audio>

<p id="demo" style="display:none;"></p>

<script>
  


window.addEventListener('load', function()
{


	var x = document.getElementById("audio"); 
	var x2 = document.getElementById("audio2"); 


	var xhr = null;
	
    getXmlHttpRequestObject = function()
    {
        if(!xhr)
        {               
            xhr = new XMLHttpRequest();
        }
        return xhr;
    };

    updateLiveData = function()
    {
        var now = new Date();
        var url = 'r1s1.php?' + now.getTime();
        xhr = getXmlHttpRequestObject();
        xhr.onreadystatechange = evenHandler;
        xhr.open("GET", url, true);
        xhr.send(null);
    };

    function evenHandler()
    {
        if(xhr.readyState == 4 && xhr.status == 200)
        {


            dataDiv = document.getElementById('liveData');
            dataDiv.innerHTML = xhr.responseText;
			var xx=xhr.responseText;
			if(xx==1){
    
				x.play();
				output.classList.add("hidden");	
				var y = document.getElementById("audio").duration;
				y=(y*1000);
				console.log(y);
				document.getElementById("demo").innerHTML = y;
				document.getElementById("p1").style.display = "block";
				document.getElementById("p2").style.display = "none";
				setTimeout(function(){ document.getElementById("p1").style.display = "none"; document.getElementById("p2").style.display = "block";}, y);
				
				const Http = new XMLHttpRequest();
				Http.open("GET","https://s-m.com.sa/r1/r1m2.php");
				Http.send();		
				setTimeout(function(){ stt(); }, y);
			}

			document.getElementById("sound").src=xhr.responseText;
            setTimeout(updateLiveData(), 10000);
        }
		
    }
	
	
	function stt(){
	
	
		var output = document.getElementById("output");
		var action = document.getElementById("action");
     
        var SpeechRecognition = SpeechRecognition || webkitSpeechRecognition;
        var recognition = new SpeechRecognition();
        recognition.onstart = function() {
            action.innerHTML = "<small>listening, please speak...</small>";
        };
                
        recognition.onspeechend = function() {
            action.innerHTML = "<small>stopped listening</small>";
            recognition.stop();
			

					  
        }
              
        // This runs when the speech recognition service returns result
        recognition.onresult = function(event) {
            var transcript = event.results[0][0].transcript;
			var confidence = event.results[0][0].confidence;
            output.innerHTML = "<b></b> " + transcript;
			
			
            output.classList.remove("hidden");
			
			const Http = new XMLHttpRequest();
			Http.open("GET","https://s-m.com.sa/r1/e.php?e=" + transcript);
			Http.send();		
				x2.play();
				var yy = document.getElementById("audio2").duration;
				yy=yy*1000;
				console.log(yy);
				document.getElementById("demo").innerHTML = yy;
				document.getElementById("p1").style.display = "block";
				document.getElementById("p2").style.display = "none";
				setTimeout(function(){ document.getElementById("p1").style.display = "none"; document.getElementById("p2").style.display = "block";}, yy);	

				//output.classList.add("hidden");				
			

			
        };
              
        // start recognition
        recognition.start();
	
	
	}



});


	function stt(){
	
	
		// get output div reference
		var output = document.getElementById("output");
		// get action element reference
		var action = document.getElementById("action");
        // new speech recognition object
        var SpeechRecognition = SpeechRecognition || webkitSpeechRecognition;
        var recognition = new SpeechRecognition();
            
        // This runs when the speech recognition service starts
        recognition.onstart = function() {
            action.innerHTML = "<small>انا استمع الان لك فضلك تحدث ..</small>";
        };
                
        recognition.onspeechend = function() {
            action.innerHTML = "<small>توقفت من الاستماع ..شكراً لك </small>";
            recognition.stop();
			

					  
        }
              
        // This runs when the speech recognition service returns result
        recognition.onresult = function(event) {
            var transcript = event.results[0][0].transcript;
			var confidence = event.results[0][0].confidence;
            output.innerHTML = "<b></b> " + transcript;
			
			
            output.classList.remove("hidden");
			
			const Http = new XMLHttpRequest();
			Http.open("GET","https://s-m.com.sa/r1/e.php?e=" + transcript);
			Http.send();		
				x2.play();
				var yy = document.getElementById("audio2").duration;
				yy=yy*1000;
				console.log(yy);
				document.getElementById("demo").innerHTML = yy;
				document.getElementById("p1").style.display = "block";
				document.getElementById("p2").style.display = "none";
				setTimeout(function(){ document.getElementById("p1").style.display = "none"; document.getElementById("p2").style.display = "block";}, yy);	

				//output.classList.add("hidden");				
			

			
        };
              
        // start recognition
        recognition.start();
	
	
	}

function playSound(){

  var x = document.getElementById("audio"); 
  x.play(); 
  var y = document.getElementById("audio").duration;
  y=y*1000;
  document.getElementById("demo").innerHTML = y;
  document.getElementById("p1").style.display = "block";
  document.getElementById("p2").style.display = "none";
  setTimeout(function(){ document.getElementById("p1").style.display = "none"; document.getElementById("p2").style.display = "block";}, y);
	
}

</script>
<div align="center">
<br>

	<button onclick="stt()">ابدأ التحدث </button>

    <p><span id="action"></span></p>
    <div id="output" class="hide" style="font-size:50px"></div>

</div>
</body>
</html>
