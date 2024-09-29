# TradeBot_AI

This project is designed to be a flexible AI-powered stock predictor. Although it is still in development, it incorporates unique indicators and features to enhance its predictive capabilities


# Features

- **Custom Indicators**: Uses unique, non-daily data such as earnings to enhance predictions.
- **Non-Daily Indicators**: Unlike most bots, AI-InvestiBot uses indicators that are not limited to daily data, such as earnings.
- **Flexible Model Design:**:
    + Create custom models with the information_keys feature.
    +Integrate any model into the AI by using a callback function during training
- **ResourceManager**:  The ResourceManager class helps manage financial resources.
- **Holding Stocks**: The bot can hold stocks when conditions are met
- **Lambda Version**: Runs on AWS Lambda for low-cost, continuous operation.
- **Advanced AI Techniques**:
  + Price and percentage prediction models
  + Data Augmentation
  + Transfer learning
  + Early Stopping



# Getting Started

1) Collect data using get_info.py.
2) Train and save your models using the example at the end of models.py.
3) Review and modify implementations in implementation.py.
4) Update the API key in secret_key.

Remember to change the api key in secret key. 

# How It Works

## Data Retrieval and Caching

- Data is gathered from yfinance and stored as JSON.
- Unique indicators are mapped to models using the information_keys attribute.

## Unique Indicators in Models

The models in this project incorporate unique indicators as follows:

- They rely on the information_keys attribute to extract custom indicators.
- These information_keys are derived from the data processed by get_info.py.
- The model retrieves a dictionary from a JSON file containing the required indicator lists.
- These indicators are then transformed into NumPy arrays and used in the Sequential model for predictions.
- You can customize the model by feeding in different information_keys into either the PriceModel or PercentageModel.

## Stock Bot Functionality

The stock bot operates based on a structured framework that incorporates AI-driven decision-making:

BaseModel: The parent class for all models, without data of its own unless specified. It handles the core bot functionality (not AI-specific).
PriceModel: A child class of BaseModel, which uses company stock data scaled between high and low values to predict prices.
PercentageModel: Another child class, which scales past data over a window of days to predict percentage price changes.
Training, testing, saving, and loading are separate processes, ensuring a clean and maintainable codebase.
The bot uses two primary methods to retrieve information:
Offline (past data): Pulls cached info from get_info.py.
Online (live data): Uses yfinance to update the model with recent stock data. It dynamically removes the oldest day and adds the newest one as it goes.

## Earnings

Earnings data is processed in the following way:

- Earnings dates and the difference between actual and estimated earnings are stored in lists.
- During execution, outliers are removed from the data, and the remaining earnings are transformed into a continuous time series:
- Days without earnings are assigned a value of 0.
- The difference between actual and expected earnings is used for days when earnings are reported.
- The project currently faces challenges in detecting earnings on certain days, which is being addressed.

## Results
- Directional Test (75.43%): Indicates that the model correctly predicts the direction of price movement 75% of the time.
- Spatial Test (68.35%): Measures whether the predicted values align with real data in relation to changes. It demonstrates 68% accuracy in positioning.
- RMSE and RMSSE: These metrics quantify the error in predictions. Lower values indicate better performance, with RMSSE being more sensitive to larger discrepancies.

## Lisence
This project is licensed under the MIT License.