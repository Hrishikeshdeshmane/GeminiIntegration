# Gemini Chat - Spring Boot Backend

Backend-only REST API for chatting with Google Gemini. Java 17+, Spring Boot 3.5.6, Maven.

## 1. Prerequisites
- JDK 17 or later
- IntelliJ IDEA
- Maven (IntelliJ can use the Maven wrapper/imported Maven)
- Gemini API key from https://aistudio.google.com/app/apikey

## 2. Run in IntelliJ
1. Extract this ZIP.
2. IntelliJ: File -> Open -> select the `gemini-springboot-backend` folder (the folder containing `pom.xml`).
3. Allow Maven to import/download dependencies.
4. Set environment variable `GEMINI_API_KEY` in Run -> Edit Configurations -> Environment variables.
5. Run `GeminiChatApplication.java`.
6. Server starts at `http://localhost:8080`.

Do not commit your API key or put it in source control. Optional: set `GEMINI_MODEL` to another model available to your API key.

## 3. Postman request
- Method: POST
- URL: `http://localhost:8080/api/chat`
- Header: `Content-Type: application/json`
- Body: raw -> JSON

Single message:
```json
{
  "message": "Explain Spring Boot in simple words"
}
```

Multi-turn conversation (send prior turns each time; `user` and `model` are Gemini roles):
```json
{
  "history": [
    { "role": "user", "text": "My name is Rahul." },
    { "role": "model", "text": "Nice to meet you, Rahul!" }
  ],
  "message": "What is my name?"
}
```

Example response:
```json
{
  "reply": "Spring Boot is a Java framework...",
  "model": "gemini-3.5-flash"
}
```

## Endpoint
`POST /api/chat` - sends the latest message and optional conversation history to Gemini.

## Notes
- The backend does not store conversation history. Postman/client sends the history with each request.
- A 400 response means the request body failed validation.
- Gemini API errors are returned with the upstream HTTP status and message.
- Keep the API key on the backend. Never send it from a browser/client or include it in Postman requests.
