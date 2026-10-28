# House Price Prediction API

**Name:** Kanishka Solanki\
**Registration Number:** 202401100200164

## Overview

A machine learning project that predicts house sale prices using the
Kaggle **House Prices: Advanced Regression Techniques** dataset. The
trained model is served through a REST API built with FastAPI and
packaged with Docker.

## Model

A scikit-learn pipeline with a Random Forest regressor is trained on the
dataset. The project evaluates model performance using Mean Absolute
Error (MAE), Root Mean Squared Error (RMSE), and R².

Reported evaluation results:

-   **MAE:** 17,518.60
-   **RMSE:** 28,785.23
-   **R²:** 0.8920

These are the results from the training run and may vary if the model or
dataset is changed.

## API Endpoints

  Method   Endpoint     Description
  -------- ------------ ----------------------------
  `GET`    `/`          Basic API information
  `GET`    `/health`    Health check
  `POST`   `/predict`   Predict a house sale price

Interactive API documentation is available at `/docs` while the server
is running.

## Example Prediction Request

Send a `POST` request to `/predict` with JSON like this:

``` json
{
  "features": {
    "OverallQual": 7,
    "GrLivArea": 1710,
    "GarageCars": 2,
    "TotalBsmtSF": 856,
    "FullBath": 2,
    "YearBuilt": 2003,
    "Neighborhood": "CollgCr"
  }
}
```

The API returns the model's predicted sale price.

## Run Locally

Create and activate a virtual environment, then install dependencies:

``` bash
python3 -m venv .venv
source .venv/bin/activate
python -m pip install -r requirements.txt
```

Start the API:

``` bash
uvicorn app.main:app --host 0.0.0.0 --port 8000
```

Open `http://127.0.0.1:8000/docs` in your browser.

## Run with Docker

Build the image:

``` bash
sudo docker build -t house-prices-api .
```

Run the container:

``` bash
sudo docker run --rm -p 8000:8000 house-prices-api
```

Then visit `http://127.0.0.1:8000/docs`.

## Tests and Continuous Integration

Run the tests locally:

``` bash
pytest -v
```

The GitHub Actions workflow in `.github/workflows/ci.yml` installs
dependencies, runs the tests, checks that `model.joblib` exists, and
builds the Docker image on pushes and pull requests targeting `main`.

```

## Dataset

Kaggle: **House Prices: Advanced Regression Techniques**.

The model artifact (`model.joblib`) is included so the API can load the
trained model without retraining at startup.