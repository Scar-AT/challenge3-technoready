# ⚙️ Challenge 3 – Server and Database Commands  

## 🧠 Project Purpose
This project provides a technical and practical overview of the **Google Scholar API**.  
It explains how the API can be used to access academic information programmatically and demonstrates a backend implementation using **Java Spring Boot**.  

The system retrieves author information and publications through the **Google Scholar Author API** (via [SerpAPI](https://serpapi.com/google-scholar-author-api)), applying the **Model–View–Controller (MVC)** architecture to handle requests, process JSON responses, and deliver structured results.

---

## 🧩 Key Functionalities
- Describes and implements core endpoints for accessing **author** and **publication** data.  
- Explains authentication using **API keys**.  
- Lists common query parameters for filtering and customizing searches.  
- Shows expected response formats with sample JSON and text outputs.  
- Includes a working **Java (Spring Boot)** implementation with `RestTemplate`.  
- Demonstrates **error handling** and **stub mode** for offline or demo use.  

---

## 🔍 Project Relevance
This documentation and implementation provide a clear understanding of how developers can access and process scholarly data through the Google Scholar API.  
It supports:
- **Automation of literature searches** 
- **Citation tracking**
- **Integration of scholarly information** into research or academic software workflows  

The backend also establishes a solid foundation for later expansion with database persistence and data analysis features.

----
  


## ⚙️ Technologies Used
- **Java 17 or higher**  
- **Spring Boot 3.5.6**  
- **Maven**  
- **RestTemplate (HTTP Client)**  
- **SerpAPI – Google Scholar Author API**  
- **PostgreSQL (planned for database integration)**  
- **Lombok (optional)**  

---

## 🧠 MVC Structure

| Layer | Package | Description |
|--------|----------|-------------|
| **Model** | `com.technoready.ch3.model` | Defines the `Author` record with id, name, affiliation, citations, interests, and articles. |
| **View** | `com.technoready.ch3.view` | Renders author data in plain-text format (`&format=txt`). |
| **Controller** | `com.technoready.ch3.controller` | Exposes `/api/author/info` to handle GET requests. |
| **Service** | `com.technoready.ch3.service` | Fetches data from the SerpAPI Author API, processes JSON, and includes a stub fallback. |
| **Exception Handler** | `com.technoready.ch3.controller` | Returns structured JSON errors for failed API calls. |
| **Configuration** | `com.technoready.ch3.config` | Provides the `RestTemplate` bean and connection timeouts. |

---

## 🚀 How to Run

### 1. Clone the Repository
```bash
git clone https://github.com/<your-username>/<your-repo>.git
cd CH3
```

### 2. Configure Environment
Edit ``src/main/resources/application.properties``

```properties
spring.application.name=CH3
server.port=8080
serpapi.key=YOUR_SERPAPI_KEY
```
💡 If serpapi.key is left blank, the application runs in stub/demo mode using sample author data.

### 3. Build and Run
```bash
mvn clean install
java -jar target/CH3-0.0.1-SNAPSHOT.jar
```
### 4. Test the Endpoint
**JSON output**
```bash
GET http://localhost:8080/api/author/info?id=qc6CJjYAAAAJ
```
**TXT output**
```bash
GET http://localhost:8080/api/author/info?id=qc6CJjYAAAAJ&format=txt
```

---

## 🧪 Example Responses
### ✅ JSON Response (Stub Mode)
```json
{
  "authorId": "qc6CJjYAAAAJ",
  "name": "Albert Einstein",
  "affiliation": "Institute for Advanced Study",
  "citations": 210000,
  "interests": ["Physics", "Relativity"],
  "articles": [
    "On the Electrodynamics of Moving Bodies",
    "Does the Inertia of a Body Depend on Its Energy Content?"
  ]
}
```

### ✅ Text Response
```vbnet
Author: Albert Einstein  
Affiliation: Institute for Advanced Study  
Citations: 210000  
Interests: Physics, Relativity  
Articles: On the Electrodynamics of Moving Bodies; Does the Inertia of a Body Depend on Its Energy Content?
```

### ❌ Error Handling Example
```json
{
  "error": "Upstream API failure",
  "detail": "External API error: 400 Bad Request"
}
```

## 🧠 Highlights & Key Learnings
- Applied the MVC pattern for clear backend structure.
- Implemented a RESTful endpoint integrating an external API.
- Added exception handling and stub mode for reliability.
- Established a strong, maintainable base for future database features.
