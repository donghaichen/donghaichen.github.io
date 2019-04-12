# 获取火币 K 线图数据

```html
<script src="https://cdn.bootcss.com/pako/1.0.6/pako.min.js"></script>
```

```javascript
	var market = 'hotbtc';
	var wsServer = 'wss://api.hadax.com/ws';
	var websocket = new WebSocket(wsServer);
    websocket.onopen = function (evt) {
        console.log("Connected to WebSocket server.");
		init()
    };

    websocket.onmessage = function (evt) {
		var reader = new window.FileReader();
		reader.readAsDataURL(evt.data); 
		reader.onloadend = function() {
			handle(reader.result)
		}
    };
	
	function init(){
		id = new Date()
		let kline = {
			"sub":"market."+market+".kline.1min",
			"id":id
		}
		websocket.send(JSON.stringify(kline));
	}  
	
	function unzip(b64Data){  
		var strData     = atob(b64Data);  
		var charData    = strData.split('').map(function(x){return x.charCodeAt(0);});  
		var binData     = new Uint8Array(charData);  
		var data        = pako.inflate(binData);  
		strData     = String.fromCharCode.apply(null, new Uint16Array(data));  
		return strData;  
	}
	
	function handle(data){
		data = data.slice(13)
		let text = unzip(data)
		let msg = JSON.parse(text)
		if (msg.ping) {
            websocket.send(JSON.stringify({
                pong: msg.ping
            }));
        } else {
			let doc = '<p>'+text+'</p>'
			document.write(doc)
            console.log(msg);
        }
	}
```