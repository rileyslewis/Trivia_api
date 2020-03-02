# Full Stack Trivia API Backend

## Getting Started

### Installing Dependencies

#### Python 3.7

Follow instructions to install the latest version of python for your platform in the [python docs](https://docs.python.org/3/using/unix.html#getting-and-installing-the-latest-version-of-python)

#### Virtual Enviornment

We recommend working within a virtual environment whenever using Python for projects. This keeps your dependencies for each project separate and organaized. Instructions for setting up a virual enviornment for your platform can be found in the [python docs](https://packaging.python.org/guides/installing-using-pip-and-virtual-environments/)

#### PIP Dependencies

Once you have your virtual environment setup and running, install dependencies by naviging to the `/backend` directory and running:

```bash
pip install -r requirements.txt
```

This will install all of the required packages we selected within the `requirements.txt` file.

##### Key Dependencies

- [Flask](http://flask.pocoo.org/)  is a lightweight backend microservices framework. Flask is required to handle requests and responses.

- [SQLAlchemy](https://www.sqlalchemy.org/) is the Python SQL toolkit and ORM we'll use handle the lightweight sqlite database. You'll primarily work in app.py and can reference models.py.

- [Flask-CORS](https://flask-cors.readthedocs.io/en/latest/#) is the extension we'll use to handle cross origin requests from our frontend server.

## Database Setup
With Postgres running, restore a database using the trivia.psql file provided. From the backend folder in terminal run:
```bash
psql trivia < trivia.psql
```

## Running the server

From within the `backend` directory first ensure you are working using your created virtual environment.

To run the server, execute:

```bash
export FLASK_APP=flaskr
export FLASK_ENV=development
flask run
```

Setting the `FLASK_ENV` variable to `development` will detect file changes and restart the server automatically.

Setting the `FLASK_APP` variable to `flaskr` directs flask to use the `flaskr` directory and the `__init__.py` file to find the application.

## Tasks

One note before you delve into your tasks: for each endpoint you are expected to define the endpoint and response data. The frontend will be a plentiful resource because it is set up to expect certain endpoints and response data formats already. You should feel free to specify endpoints in your own way; if you do so, make sure to update the frontend or you will get some unexpected behavior.

1. Use Flask-CORS to enable cross-domain requests and set response headers.
2. Create an endpoint to handle GET requests for questions, including pagination (every 10 questions). This endpoint should return a list of questions, number of total questions, current category, categories.
3. Create an endpoint to handle GET requests for all available categories.
4. Create an endpoint to DELETE question using a question ID.
5. Create an endpoint to POST a new question, which will require the question and answer text, category, and difficulty score.
6. Create a POST endpoint to get questions based on category.
7. Create a POST endpoint to get questions based on a search term. It should return any questions for whom the search term is a substring of the question.
8. Create a POST endpoint to get questions to play the quiz. This endpoint should take category and previous question parameters and return a random questions within the given category, if provided, and that is not one of the previous questions.
9. Create error handlers for all expected errors including 400, 404, 422 and 500.

REVIEW_COMMENT
```
This README is missing documentation of your endpoints. Below is an example for your endpoint to get all categories. Please use it as a reference for creating your documentation and resubmit your code.

Endpoints
GET '/categories'
GET ...
POST ...
DELETE ...

GET '/categories'
- Fetches a dictionary of categories in which the keys are the ids and the value is the corresponding string of the category
- Request Arguments: None
- Returns: An object with a single key, categories, that contains a object of id: category_string key:value pairs.
{
'1' : "Science",
'2' : "Art",
'3' : "Geography",
'4' : "History",
'5' : "Entertainment",
'6' : "Sports"
}

```


## Testing
To run the tests, run
```
dropdb trivia_test
createdb trivia_test
psql trivia_test < trivia.psql
python test_flaskr.py
```
## Error Handling
Errors return as Json objects as per the following format:
```
{
  "success": False,
  "error": 404,
  "message": "resource not found"
}
```
API Error types that may be returned when requests fail:
* 404: resource not found
* 405: method not allowed
* 422: unprocessable
* 400: bad request

## Endpoints
### GET /categories
* Retrieves all categories.
- Request: None
- Returns: success value and a dictionary of categories.
* Example: ```curl http://127.0.0.1:5000/categories```
```
{
  "categories": {
    "1": "Science",
    "2": "Art",
    "3": "Geography",
    "4": "History",
    "5": "Entertainment",
    "6": "Sports"
  },
  "success": true
}
```

## Get /questions
* Retrieves all questions. Results are paginated in groups of 10.
- Request: None.
- Returns: success value, a dictionary list of questions, total number of questions, a dictionary of categories, and a list of categories of current displayed questions.
* Example: ```curl http://127.0.0.1:5000/questions```
```
{
  "categories": {
    "1": "Science",
    "2": "Art",
    "3": "Geography",
    "4": "History",
    "5": "Entertainment",
    "6": "Sports"
  },
  "current_categories": [
    1,
    1,
    1,
  ],
  "questions": [
    {
      "answer": "Elon Musk",
      "category": 1,
      "difficulty": 1,
      "id": 1,
      "question": "What is the name of the founder of SpaceX?"
    },
    {
      "answer": "Falcon One"
      "category": 1,
      "difficulty": 3,
      "id": 2,
      "question": "What is the name of the first Rocket built by SpaceX?"
    },
    {
      "answer": "Andrew Ng",
      "category": 1,
      "difficulty": 2,
      "id": 3,
      "question": "Who was the founder of Coursera and was also a Professor in Computer Science?"
    }
  ],
  "success": true,
  "total_questions": 3
}
```
## DELETE /questions/{question_id}
* Deletes question using the specified question id.
- Request: an id of a question to delete.
- Returns: success value, an id of a question which has been deleted and the total number of questions remaining.
- Example: ```curl -X DELETE http://127.0.0.1:5000/questions/2?page=1```
```
{
  "deleted": 2,
  "success": true,
  "total_questions": 2
}
```
## POST /questions
* Creates a new question through using the required information such as a question, answer, difficulty and category.
- Returns: success value, id of the generated (created) question and a total number of questions.
- Example ```curl http://127.0.0.1:5000/questions?page=2 -X POST -H "content-Type: application/json" -d
             '{"question": "Who was the founder of SpaceX?", "answer": "Elon Musk", "difficulty":
               "1", "category": "1"}'
               ```
```
{
  "success": true,
  "created": 1,
  "total_questions": 9
}
```

## POST /search_questions
* Retrieves questions as per search term input. The search term is case-insensitive and will be a substring of the question.
- Request: None,
- Returns: success value, a list of dictionary - questions that correspond to the search term, a list of categories of the searched questions and total number of searched questions.
- Example: ```curl http://127.0.0.1:5000/search_questions -X POST -H "Content-Type: application/json" -d
              '{"searchTerm": "space"}'
           ```
```
{
  "current_category": [
  5
  ],
  "questions": [
  {
    "answer": "Matt Damon"
    "category": 1,
    "difficulty": 3,
    "id": 7,
    "question": "What was the name of the main actor in the movie 'The Martian'?"
  }
  ],
  "success": true,
  "total_questions": 1
}
```

## GET /categories/{category_id}/questions
* Retrieves questions of a specified category.
- Request: an id of a category.
- Returns: success value, list of dictionary of questions that correspond to an id of a category, a list of categories of currently displayed questions, total number of questions.
- Example: ```curl http://127.0.0.1:5000/categories/2/questions```

```
{
  "current_category": [
    2,
    2,
    2
  ],
  "questions": [
    {
      "answer": "Tokyo",
      "category": 2,
      "difficulty": 1,
      "id": 8,
      "question": "What is the name of the city which is the Capital of Japan?"
    },
    {
      "answer": "Japan",
      "category": 2,
      "difficulty": 4,
      "id": 9,
      "question": "To which country does the 'Mogami River' belong to?"
    },
    {
      "answer": "New Zealand",
      "category": 2,
      "difficulty": 3,
      "id": 10,
      "question": "In which country is Mount Cook located?"
    }
  ],
  "success": true,
  "total_questions": 3
}
```

## POST /generate_quizzes
* Retrieves a random question from a given category to play the quiz.
- Request: None.
- Returns: success value and a dictionary of a question.
- Example: ```curl http://127.0.0.1:5000/quizzes -X POST -H "Content-Type: application/json" -d
              '{"previousQuestions": [], "quizCategory": {"id":"1","type": "Science"}}'
              ```

```
{
  "question": {
    {
      "answer": "Elon Musk",
      "category": 1,
      "difficulty": 1,
      "id": 1,
      "question": "Who founded the Space company under the name of SpaceX?"
    },
    "success": true
}
```
