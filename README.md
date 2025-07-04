# LoanLens - Loan Prediction API

A machine learning-powered API for predicting loan approval status using FastAPI.

## Features

- **Machine Learning Model**: Uses Logistic Regression trained on loan application data
- **REST API**: FastAPI-based API with automatic documentation
- **Web Interface**: Simple HTML frontend for testing
- **Input Validation**: Pydantic models for request validation
- **Health Checks**: API health monitoring endpoint

## Setup and Installation

1. **Navigate to the server directory**:
   ```bash
   cd server
   ```

2. **Install dependencies**:
   ```bash
   pip install -r requirements.txt
   ```

3. **Ensure the model is trained** (run the Jupyter notebook if needed):
   ```bash
   jupyter notebook main.ipynb
   ```
   Make sure to run all cells to generate the `loan_model.pkl` file.

## Running the API

1. **Start the FastAPI server**:
   ```bash
   python api.py
   ```
   
   Or using uvicorn directly:
   ```bash
   uvicorn api:app --reload --host 0.0.0.0 --port 8000
   ```

2. **Access the API**:
   - API Documentation: http://localhost:8000/docs
   - Alternative docs: http://localhost:8000/redoc
   - Web Interface: Open `index.html` in your browser

## API Endpoints

### POST /predict
Predict loan approval status.

**Request Body**:
```json
{
  "Gender": "Male",
  "Married": "Yes",
  "Dependents": 1,
  "Education": "Graduate",
  "Self_Employed": "No",
  "ApplicantIncome": 5849.0,
  "CoapplicantIncome": 0.0,
  "LoanAmount": 146.0,
  "Loan_Amount_Term": 360.0,
  "Credit_History": "Yes",
  "Property_Area": "Semiurban"
}
```

**Field Descriptions**:
- `Gender`: "Female" or "Male"
- `Married`: "No" or "Yes"
- `Dependents`: 0, 1, 2, or 4 (for 3+)
- `Education`: "Not Graduate" or "Graduate"
- `Self_Employed`: "No" or "Yes"
- `ApplicantIncome`: Applicant's income
- `CoapplicantIncome`: Coapplicant's income
- `LoanAmount`: Requested loan amount
- `Loan_Amount_Term`: Loan term in days
- `Credit_History`: "No" or "Yes"
- `Property_Area`: "Rural", "Semiurban", or "Urban"

**Response**:
```json
{
  "loan_status": 1,
  "loan_status_text": "Approved",
  "probability": 0.8542
}
```

### GET /health
Health check endpoint.

### GET /
Root endpoint with API information.

## Testing the API

1. **Using the test script**:
   ```bash
   python test_api.py
   ```

2. **Using curl**:
   ```bash
   curl -X POST "http://localhost:8000/predict" \
        -H "Content-Type: application/json" \
        -d '{
          "Gender": "Male",
          "Married": "Yes",
          "Dependents": 1,
          "Education": "Graduate",
          "Self_Employed": "No",
          "ApplicantIncome": 5849.0,
          "CoapplicantIncome": 0.0,
          "LoanAmount": 146.0,
          "Loan_Amount_Term": 360.0,
          "Credit_History": "Yes",
          "Property_Area": "Semiurban"
        }'
   ```

3. **Using the web interface**:
   Open `index.html` in your browser and fill out the form.

## Project Structure

```
loanlens/
├── README.md
└── server/
    ├── api.py              # FastAPI application
    ├── main.ipynb          # Jupyter notebook for model training
    ├── loan_model.pkl      # Trained model (generated)
    ├── requirements.txt    # Python dependencies
    ├── test_api.py        # API test script
    ├── index.html         # Web interface
    └── train_u6lujuX_CVtuZ9i (1).csv  # Training data
```

## Model Information

The API uses a Logistic Regression model trained on loan application data with the following features:
- Demographic information (Gender, Marital Status, Dependents, Education)
- Employment status and income details
- Loan amount and terms
- Credit history
- Property area

The model achieves good accuracy on the training and test datasets as shown in the Jupyter notebook.