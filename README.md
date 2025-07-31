# Address Service API (AWS SAM + TypeScript)

## Overview

Build a real-world, serverless API using **AWS SAM**, **TypeScript**, and implement **integration tests with mocked external services**.
The service should return all **Local Government Areas (LGAs)** for a given **state code** in Nigeria. Additionally, enrich each LGA with dummy **geo-coordinates**, simulating a call to an external service (like Mapbox or OpenCage).

---

## Requirements

### Functionality

Implement one endpoint:

```
GET /lgas/{stateCode}
```

Where `stateCode` is a two-letter Nigerian state abbreviation (e.g., `LA` for Lagos, `FC` for Abuja FCT).

**Response Example:**

```json
{
  "state": "Lagos",
  "lgas": [
    {
      "name": "Ikeja",
      "coordinates": { "lat": 6.6018, "lng": 3.3515 }
    },
    {
      "name": "Surulere",
      "coordinates": { "lat": 6.5000, "lng": 3.3500 }
    }
  ]
}
```

**Data Source**
* Use a **hardcoded or local JSON file** with states and LGAs (you may use \~5 states for demo).
* For each LGA, simulate enrichment with coordinates using a **call to an external geolocation API**.

---

## Technical Requirements

* Use **AWS SAM** for infrastructure setup (API Gateway + Lambda).
* Use **TypeScript** for all code.
* Structure your project cleanly (`src/`, `tests/`, etc.).
* Implement **integration tests** that run locally using `sam local start-api`.

**Write tests that:**
* Start the API locally and call the real `/lgas/{stateCode}` endpoint.
* Mock external API calls (for coordinates) - Use **mocks** for all external API calls in your tests (e.g., with `nock`).
* Validate:

  * Correct response structure.
  * Proper handling of invalid state codes.
  * Error handling if enrichment fails.

**Bonus Points**
* Use environment variables for external API keys or base URLs.
* Add logging middleware or simple input validation.
* Handle timeouts and errors from external APIs gracefully.
* Support caching (in-memory or simulated) for repeated state lookups.
