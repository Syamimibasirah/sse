<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Asian Fashion Show</title>
    <style>
        body { 
            font-family: Arial, sans-serif; 
            background-color: #ffe6f2; 
            margin: 0; 
            padding: 0; 
            display: flex; 
            justify-content: flex-end; 
            align-items: center; 
            height: 100vh; 
            overflow: hidden;
        }
        .container {
            position: fixed;
            right: 10px;
            top: 10px;
            width: 300px;
            padding: 20px;
            background: #ff99cc;
            border-radius: 10px;
            box-shadow: 3px 3px 10px rgba(0, 0, 0, 0.2);
            text-align: center;
        }
        h1 {
            font-size: 18px;
            color: white;
            margin-bottom: 10px;
        }
        #updates {
            margin-top: 10px;
            height: 300px;
            overflow-y: auto;
            background: #ffe6f2;
            padding: 10px;
            border-radius: 8px;
            box-shadow: inset 0px 0px 5px rgba(0, 0, 0, 0.2);
        }
        .update {
            background: white;
            padding: 10px;
            margin-bottom: 8px;
            border-radius: 5px;
            font-size: 14px;
            font-weight: bold;
            transition: all 0.3s ease-in-out;
            color: #d63384;
        }
    </style>
</head>
<body>

    <div class="container">
        <h1>🌏 Asian Fashion Show 👗</h1>
        <div id="updates">
            <p>Waiting for fashion updates...</p>
        </div>
    </div>

    <script>
        // Connect to the SSE server
        const eventSource = new EventSource("https://lms.pb.edu.bn/wy2301/sse.php");

        // Get the updates container
        const updatesDiv = document.getElementById("updates");

        eventSource.onmessage = function(event) {
            const message = event.data;
            
            // Check if the message contains #GROUP01
            if (message.includes("#GROUP01")) {
                const cleanMessage = message.replace(/#GROUP\d+/, "").trim(); // Remove group ID
                
                const updateElement = document.createElement("div");
                updateElement.classList.add("update");
                updateElement.textContent = "👗 " + cleanMessage;
                updatesDiv.prepend(updateElement); // Show latest update at the top
            }
        };

        eventSource.onerror = function() {
            console.error("SSE connection error.");
        };
    </script>

</body>
</html>

<!-- REFERENCE: 
https://developer.mozilla.org/en-US/docs/Web/API/Server-sent_events/Using_server-sent_events -->
