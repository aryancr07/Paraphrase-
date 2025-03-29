<!DOCTYPE html><html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Paraphrasing Tool</title>
    <style>
        body { font-family: Arial, sans-serif; text-align: center; padding: 20px; }
        textarea { width: 80%; height: 100px; margin: 10px; padding: 10px; font-size: 16px; }
        button { padding: 10px 20px; font-size: 16px; cursor: pointer; }
        #output { margin-top: 20px; font-size: 18px; color: blue; padding: 10px; border: 1px solid #ccc; display: inline-block; max-width: 80%; }
    </style>
</head>
<body>
    <h2>Paraphrasing Tool</h2>
    <textarea id="inputText" placeholder="Enter text here..."></textarea><br>
    <button onclick="paraphraseText()">Paraphrase</button>
    <h3>Output:</h3>
    <p id="output"></p><script>
    async function paraphraseText() {
        let text = document.getElementById("inputText").value;
        let apiKey = "AIzaSyAPuqRXzi4MFBRfsbn-4p6riH9XOSCGtVM"; // Replace with your actual API key

        let response = await fetch("https://api.openai.com/v1/chat/completions", {
            method: "POST",
            headers: {
                "Content-Type": "application/json",
                "Authorization": `Bearer ${apiKey}`
            },
            body: JSON.stringify({
                model: "gpt-3.5-turbo",
                messages: [{ role: "user", content: `Paraphrase this: "${text}"` }],
                max_tokens: 100,
                temperature: 0.7
            })
        });

        let data = await response.json();
        let paraphrasedText = data.choices?.[0]?.message?.content || "Error: Unable to paraphrase.";
        document.getElementById("output").innerText = paraphrasedText;
    }
</script>

</body>
</html>
