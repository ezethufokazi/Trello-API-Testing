# Trello API Testing Project

**Author:** Ezethu Fokazi  
**Tool:** Postman, Newman  
**Project Type:** API Testing Portfolio Project

## Documentation

View the full API documentation here: [Trello API Documentation](https://documenter.getpostman.com/view/52307578/2sBXinJWGf)

## Project Overview

This project is an API testing portfolio piece built by an aspiring QA Engineer. It covers the Trello REST API using Postman, testing the full lifecycle of Trello objects — Boards, Lists, Cards, and Members. The project includes positive and negative test cases, environment variables, dynamic data, and a documented bug report tracked on a Jira board.

The Trello API allows users to manage boards, lists, and cards programmatically. All test scripts were written in JavaScript using Postman's built-in test framework.

\---

## Tools Used

* **Postman** — API testing and test script execution
* **Newman** — Command line collection runner and HTML report generation
* **JavaScript** — Test assertions and pre/post request scripts
* **Jira** — Bug tracking and defect documentation
* **GitHub** — Version control and portfolio hosting

\---

## Project Structure

```
Trello API Collection
├── Boards
│   ├── Create Board
│   ├── Get Board
│   ├── Update Board
│   ├── Create List on a Board
│   └── Get Lists on a Board
├── Lists
│   ├── Create new List
│   ├── Get List
│   ├── Update List
│   └── Archive List
├── Cards
│   ├── Create new Card
│   ├── Get Card
│   ├── Update Card
│   └── Delete Card
├── Members
│   ├── Get Member
│   └── Get Boards Member belongs to
├── Negative Tests
│   ├── Create Board - No Name
│   ├── Get Board - Invalid Board ID
│   ├── Get Member - Invalid Member ID
│   ├── Get List - Invalid API Key
│   └── Update Card - Invalid Token
└── Cleanup
    └── Delete Board
```

\---

## Endpoints Covered

|Method|Endpoint|Description|
|-|-|-|
|POST|/boards|Create a new board|
|GET|/boards/:id|Get a board by ID|
|PUT|/boards/:id|Update a board|
|POST|/boards/:id/lists|Create a list on a board|
|GET|/boards/:id/lists|Get all lists on a board|
|POST|/lists|Create a new list|
|GET|/lists/:id|Get a list by ID|
|PUT|/lists/:id|Update a list|
|PUT|/lists/:id/closed|Archive a list|
|POST|/cards|Create a new card|
|GET|/cards/:id|Get a card by ID|
|PUT|/cards/:id|Update a card|
|DELETE|/cards/:id|Delete a card|
|GET|/members/me|Get the authenticated member|
|GET|/members/me/boards|Get all boards the member belongs to|
|DELETE|/boards/:id|Delete a board|

\---

## Test Approach

**Positive Testing**

* Happy path scenarios for all endpoints
* Status code validation
* Response body assertions using dynamic environment variables
* Response time checks under 2000ms
* Cross-resource validation (e.g. confirming a card belongs to the correct board and list)

**Negative Testing**

* Creating a board without a name
* Getting a board with an invalid board ID
* Getting a member with an invalid member ID
* Getting a list with an invalid API key
* Updating a card with an invalid token

**Environment Variables**
All test data is stored and managed dynamically using environment variables. The Create Board request saves the `board\_id`, Create List saves the `list\_id`, Create Card saves the `card\_id`, and Get Member saves the `member\_id`. These are then reused across all subsequent requests. Environment variables are also unset after deletion requests to keep the environment clean. No hardcoded IDs anywhere in the collection.

\---

## Bug Report

One bug was identified and documented during testing and tracked on Jira:

|#|Bug|Endpoint|Expected|Actual|
|-|-|-|-|-|
|1|Wrong status code returned for invalid board ID|GET /boards/:id|404 Not Found|400 Bad Request|

\---

## How to Run the Collection

**Prerequisites**

* Postman installed on your machine
* Node.js installed on your machine
* Download the collection and environment files from this repository

**Running in Postman**

1. Open Postman
2. Click **Import** and import both the collection and environment files
3. Select the **Trello API** environment from the top right dropdown
4. Click the **Runner** button
5. Select the **Trello API** collection
6. Make sure the request order is correct (Create Board must run before List, Card, and Member requests)
7. Click **Run Trello API**

**Running with Newman**

1. Install Newman: `npm install -g newman`
2. Install HTML reporter: `npm install -g newman-reporter-htmlextra`
3. Run the collection:

```
newman run Trello\_API\_Collection.json -e Trello\_API\_Environment.json -r htmlextra --reporter-htmlextra-export trello-report.html
```

**Important Note**  
The collection must be run in order. Create Board runs first and saves the `board\_id` which all subsequent requests depend on. The Cleanup folder (Delete Board) should always run last.

\---

## Key Learnings

* API testing fundamentals using Postman and the Trello REST API
* Writing JavaScript test assertions for status codes, response bodies and response times
* Using environment variables for dynamic and reusable test data across multiple resource types
* Cross-resource validation — verifying that a card belongs to the correct list and board
* Difference between positive and negative testing
* Bug identification and documentation using Jira
* Understanding of HTTP methods, status codes, headers and API key/token authentication
* Importance of test execution order in API testing
* Generating HTML test reports using Newman and newman-reporter-htmlextra

