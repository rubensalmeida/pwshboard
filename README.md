# pwshboard

[powershell](https://github.com/powershell/powershell) + [websocketd](https://github.com/joewalnes/websocketd) + [javascript](https://github.com/joewalnes/websocketd/blob/master/examples/html/count.html) = pwshboard

Couldn't be easier!

1) create a powershells script. Here's a suggestion:

```
#start of c:\scripts\counter.ps1
1..10 | ForEach-Object {
    $_;
    Start-Sleep -Seconds 1;
}
#end of c:\scripts\counter.ps1
```

2) start a websocketd instance of your powershell script:
```
c:\tools\websocketd.exe --port=8080 pwsh.exe -File c:\scripts\counter.ps1
```

3) create a basic HTML5 file. Host it on any webserver or open it directly from a file:// URL. Here's an example:

```
<!-- start of file counter.html -->
<!DOCTYPE html>
<html lang='en'>
<head>
	<meta charset='UTF-8'>
	<title>pwshboard</title>
	<script>
		function log(msg) {
			document.getElementById('log').textContent += msg + '\n';
		}
		var ws = new WebSocket('ws://localhost:8080/');
		ws.onopen = function() {
			log('CONNECT');
		};
		ws.onclose = function() {
			log('DISCONNECT');
		};
		ws.onmessage = function(event) {
			log('MESSAGE: ' + event.data);
		};
	</script>
</head>
<body>
	<div>
		<pre id="log"></pre>
	</div>
</body>
</html>
<!-- end of file counter.html -->
```

If you can see the counter numbers showing up on your webpage, everything is working!

At this point the sky is the limit! 

If you're interested in streaming realtime data into your dashboard have a look at:
- [Bootstrap](https://getbootstrap.com/docs/4.4/examples/dashboard/)
- [Rickshaw](https://tech.shutterstock.com/rickshaw/examples/)
- [Epoch](https://epochjs.github.io/epoch/real-time/)
- [SmoothieCharts](http://smoothiecharts.org/)

Hope this can help you the same way it helped me!
