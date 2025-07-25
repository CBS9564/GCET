### Example usage of the Google Gemini API (model and API key are both environment variables)

const response = await fetch('https://generativelanguage.googleapis.com/v1beta/models/gemini-1.5-flash:generateContent', {
method: 'POST',
headers: {
    'Content-Type': 'application/json',
    'x-goog-api-key': this.apiKey
},
body: JSON.stringify({
    contents: [{
        role: 'user',
        parts: [{
            text: this.buildPRPParsingPrompt(prpContent, projectContext, config)
        }]
    }],
    generationConfig: {
        maxOutputTokens: 3000
    }
})
});

if (!response.ok) {
throw new Error(`Google Gemini API error: ${response.status} ${response.statusText}`);
}

const result = await response.json();
const content = (result as any).candidates[0].content.parts[0].text;

// Parse the JSON response
const aiTasks = JSON.parse(content);