# What is SerpAPI?
**SerpAPI** is a web-scraping and data delivery service that provides structured access to search engine results through an API. It allows developers to retrieve real-time data from platforms like **Google Search**, **Google Scholar**, **Google Images**, **Bing**, **YouTube**, and others—without needing to manually scrape pages or handle captchas.

# Endpoints

### Google Scholar Organic Results
Allows to retrieve organic search results from Google Scholar based on a query.
-> `/search?engine=google_scholar`

### Google Scholar Author Results
Used to scrape author results from Google’s Scholar author search page.
-> `/search?engine=google_scholar_author`

### Google Scholar Cite Results
Allows you to scrape citation information associated with articles found on Google Scholar.
-> `/search?engine=google_scholar_cite`

### Google Scholar Author Cited By
Used to access citation details and metrics for a specific Google Scholar author.
-> `/search?engine=google_scholar_author_cited_by`

### Google Scholar Profiles (Discontinued)
Google Scholar implemented login requirements for accessing profile information, making this type of endpoint generally discontinued or less reliable.
-> `/search?engine=google_scholar_profiles`


# Authentication methods

Google scholar does not provide a public API with direct authentication. However, there are third-party services that expose Google Scholar data, for example: SerpAPI. Using third-party services usually require authentication.

### **The way it works**

1. **Account registration** - Sign up on the provider’s plataform
2. **API Key generation** – Receive a unique key that identifies your account
3. **Request Header or a Parameter** – Include this key in your requests, usually like this:
	- As a **query** **parameter**
		``https://api.scholar.com/search?query=deep+learning&api_key=YOUR_KEY``
	- As an **HTTP Header**
		``GET /search?query=deep+learning HTTP/1.1``
		``Host: api.scholar.com``
		``Authorization: Bearer YOUR_KEY``
4. **Key management**


# Query parameters
1. **query**
	Keywords to search
	Example: ``?query=artificial+intelligence`` 

2. **author**
	Filter results by a specific author’s name
	Example:  ``?author=John+Smith`` 

3. **year / year_low / year_high**
	Filter results to a particular year or range
	Example: ``?year=2023`` or ``?year_low=2018&year_high=2024``

4. **num**
	Number of results to return per request (commonly 10–20)
	Example: ``?num=10``

5. **start**
	Offset for pagination, telling the API where to begin listing results
	Example: ``?start=20``

6. **citation_id**
	Retrieve details of a specific publication by its unique ID

7. **sort**
	Sort results by relevance or by year
	Example: ``?sort=year``
	
	This is an **example** of a request with parameters:
```
https://api.scholar.com/search?query=deep+learning&author=Jane+Doe&year_low=2020&year_high=2023&num=5
```
This query would return 5 results about “deep learning” authored by Jane Doe published between 2020 and 2023.


# Response formats
The API typically returns results in JSON format for easy parsing

**Snippet example**
```
{
  "title": "Deep Learning for Natural Language Processing",
  "authors": ["John Doe", "Jane Smith"],
  "year": 2023,
  "citations": 152,
  "link": "https://scholar.google.com/scholar?cluster=123456"
}
```

This structure makes it easier to extract metadata, author names, year of publication, citations in the article, and the citation.

# Usage limits
To prevent abuse, the API enforces limits on request volume:
- Free plans typically allow ~100 requests per day.
- Paid plans can allow thousands of requests.
- If limits are exceeded, the API returns an HTTP 429 Too Many Requests error.

Best practices:
- Cache results to minimize repeated queries.
- Space out requests to respect rate limits.


# Code examples
Example from SerpAPI Documentation

**Python language**
```
from serpapi import GoogleSearch

params = {
  "engine": "google_scholar",
  "q": "artificial intelligence",
  "api_key": "YOUR_SERPAPI_KEY"
}

search = GoogleSearch(params)
results = search.get_dict()

for paper in results["organic_results"]:
    print(paper["title"], "-", paper["link"])

```
**Javascript (Node.js)**
```
const SerpApi = require('google-search-results-nodejs');
const search = new SerpApi.GoogleSearch("YOUR_SERPAPI_KEY");

const params = {
  engine: "google_scholar",
  q: "machine learning"
};

search.json(params, data => {
  data.organic_results.forEach(paper => {
    console.log(`${paper.title} - ${paper.link}`);
  });
});
```



# References

- Google Scholar. (2025). _Google Scholar Help Center_. Retrieved from: https://scholar.google.com/intl/en/scholar/help.html

- SerpAPI. (2025). _Google Scholar API Documentation_. Retrieved from: https://serpapi.com/google-scholar-api