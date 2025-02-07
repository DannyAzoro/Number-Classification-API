Here's a detailed `README.md` 

---

# Number Classification API

This API is Flask-based. It takes numbers inserted to it, and sorts them according to different properties. These properties include **prime**, **perfect**, **Armstrong**, and **even/odd**. It also gives a fun-fact about the number. The API accepts a number via a GET request and returns a JSON response containing all those properties.

## Content

- [Setup](#Setup)
- [Usage](#usage)
- [API Endpoints](#api-endpoints)
  - [GET /api/classify-number](#get-apiclassify-number)
- [Response Format](#response-format)
  - [Successful Response (200 OK)](#successful-response-200-ok)
  - [Error Response (400 Bad Request)](#error-response-400-bad-request)
- [Code Structure](#code-structure)
- [Test phase](#test-phase)
- [Deployment](#deployment)
- [Performance](#performance)

---

## Setup

Follow these steps below to run the API on your local machine:

### Requirement(s)

- Python 3.6 or higher: 
confirm python is installed with

```bash
python --version
```
- `pip` (Python package installer)

install on windows (VScode) using
```bash
sudo apt install python3-pip
```

### Steps 

1. Clone the repository:

   ```bash
   git clone https://github.com/DannyAzoro/Number-Classification-API.git
   cd Number-Classification-API.git
   ```

2. Create a virtual environment and activate it (just so you can isolate your dependencies)

On Windows (VScode)

```bash
sudo apt install python3.12 venv
python3 -m venv venv
source venv/bin/activate
```

3. Install the required dependencies:

   ```bash
   pip install -r requirements.txt
   ```

3. Run the Flask app:

   ```bash
   python app.py
   ```

   The app will start and be accessible at `http://127.0.0.1:5000` by default.

---

## Usage

The API will be ready to run now, make GET requests to the `/api/classify-number` endpoint by passing a query parameter `number`.

Example:

```bash
http://127.0.0.1:5000/api/classify-number?number=9
```

### Expected Output:

For a valid input `9`, the API will return the following response:

```json
{
    "number": 9,
    "is_prime": false,
    "is_perfect": false,
    "properties": ["armstrong","odd"],
    "digit_sum": 9,
    "fun_fact": "9 is the number of circles of Hell in Dante's Divine Comedy"
}
```

---

## API Endpoints

### `GET /api/classify-number`

This takes the `number` and returns a response in JSON format alongside all the properties of the numbers.

#### Parameters:

- `number` (required): The integer value that needs to be classified.

#### Response:

The API returns a JSON object with the following fields:


- `fun_fact`: A fun fact about the number (e.g., explaining if it’s an Armstrong number).
- `digit_sum`: The sum of the digits of the number.
- `is_prime`: Boolean indicating if the number is prime.
- `is_perfect`: Boolean indicating if the number is perfect.
- `properties`: An array of classifications (e.g., prime, perfect, armstrong, even, odd).
- `number`: The input number.

---

## Response Format

### A Successful Response (200 OK) will read

```json
{
    "number": 9,
    "is_prime": false,
    "is_perfect": false,
    "properties": ["armstrong", "odd"],
    "digit_sum": 9,
    "fun_fact": "9 is the number of circles of Hell in Dante's Divine Comedy"
}
```

### An Error Response (400 Bad Request) - an unsuccessful one will read

```json
{
    "number": "alphabet",
    "error": true
}
```
The above will occur when anything other than an integer is used instead of an integer
---

## Code Structure

### Main Files

- **`app.py`**: The main Python file containing the Flask app and logic for classifying numbers.
- **`requirements.txt`**: A file listing all the dependencies required to run the app.

### Helper Functions

- **`is_prime(n)`**: Checks if a number is prime.
- **`is_perfect(n)`**: Checks if a number is perfect.
- **`is_armstrong(n)`**: Checks if a number is an Armstrong number.
- **`sum_of_digits(n)`**: Calculates the sum of digits of the number.
- **`get_fun_fact(n)`**: Returns a fun fact about the number.

---

## Test phase

To test the API:

1. Run the Flask server locally with `python app.py`.
2. Open **Postman** or **Curl** to send a `GET` request to the endpoint `/api/classify-number?number=<your_number>` or copy the link and send a `GET` request to that endpoint on your browser
3. Verify that the response matches the required format for both valid and invalid inputs.

### Example Requests:

- **Valid Request**:

  ```bash
  curl "http://127.0.0.1:5000/api/classify-number?number=9"
  ```

  Expected Response:
  
  ```json
  {
      "number": 9,
      "is_prime": false,
      "is_perfect": false,
      "properties": ["armstrong", "odd"],
      "digit_sum": 9,
      "fun_fact": "9 is the number of circles of Hell in Dante's Divine Comedy"
  }
  ```

- **Invalid Request**:

  ```bash
  curl "http://127.0.0.1:5000/api/classify-number?number=kane"
  ```

  Expected Response:
  
  ```json
  {
      "number": "alphabet",
      "error": true
  }
  ```

---

## Deployment

This API is also hosted on **Render**, a cloud platform for deploying web applications. Follow the steps below to deploy it:

### Steps for Deployment on Render:

1. **Create a Render Account:**
   - Go to [Render](https://render.com) and sign up for a free account.

2. **Create a New Web Service:**
   - From your Render dashboard, click on the **New** button and select **Web Service**.
   
3. **Connect to Your GitHub Repository:**
   - Select **GitHub** as the source and choose the repository containing your Flask API project.
   
4. **Configure Deployment Settings:**
   - Set the **Environment** to **Python**.
   - Under **Build Command**, use:
   
     ```bash
     pip install -r requirements.txt
     ```

   - Under **Start Command**, use:
   
     ```bash
     python app.py
     ```

5. **Deploy:**
   - Click **Deploy** to deploy your Flask API to Render.

Once deployed, your API will be publicly accessible at the Render-provided URL, such as:

```bash
https://number-classification-api-pwew.onrender.com/api/classify-number?number=17
```

---

## Performance

The API is set in such a way that its response time is fast. It performs basic validation and calculates classifications within an acceptable time frame. The average response time is expected to be under 500ms. You can monitor response times and optimize as needed.

---