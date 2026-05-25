<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="utf-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1" />
        <title>Temperature Prediction - Learning Document</title>
        <style>
            :root {
                --ink: #0b0b0f;
                --soft-ink: #1b1a22;
                --muted: #5b5a6a;
                --light: #f5f2ea;
                --accent: #ff6b35;
                --accent-2: #1f7a8c;
                --accent-3: #f6aa1c;
                --card: #ffffff;
                --grid: rgba(0, 0, 0, 0.06);
            }

            * {
                box-sizing: border-box;
            }

            body {
                margin: 0;
                font-family: "Trebuchet MS", "Lucida Sans Unicode", "Lucida Grande", "Lucida Sans", Arial, sans-serif;
                color: var(--ink);
                background: radial-gradient(circle at 20% 20%, #fff5e9 0%, #f1f5f9 35%, #eef0f8 100%);
            }

            header {
                padding: 64px 24px 48px;
                background: linear-gradient(120deg, #101018 0%, #141d2a 55%, #0e2830 100%);
                color: #fff;
                position: relative;
                overflow: hidden;
            }

            header::after {
                content: "";
                position: absolute;
                inset: 0;
                background: repeating-linear-gradient(135deg, rgba(255, 255, 255, 0.07), rgba(255, 255, 255, 0.07) 1px, transparent 1px, transparent 16px);
                pointer-events: none;
            }

            .wrap {
                max-width: 1100px;
                margin: 0 auto;
                position: relative;
                z-index: 1;
            }

            .title {
                font-size: clamp(2.2rem, 3vw, 3.4rem);
                margin: 0 0 12px;
                letter-spacing: 0.5px;
            }

            .subtitle {
                font-size: 1.05rem;
                max-width: 760px;
                color: #d7d8e4;
            }

            .hero-grid {
                display: grid;
                grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
                gap: 16px;
                margin-top: 28px;
            }

            .hero-card {
                background: rgba(255, 255, 255, 0.08);
                border: 1px solid rgba(255, 255, 255, 0.12);
                padding: 16px;
                border-radius: 14px;
                backdrop-filter: blur(4px);
            }

            .hero-card h3 {
                margin: 0 0 6px;
                font-size: 1rem;
            }

            .section {
                padding: 48px 24px;
            }

            .section-title {
                font-size: 1.8rem;
                margin-bottom: 12px;
            }

            .lead {
                color: var(--muted);
                max-width: 900px;
            }

            .grid {
                display: grid;
                gap: 20px;
                grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
                margin-top: 24px;
            }

            .card {
                background: var(--card);
                border-radius: 18px;
                padding: 20px;
                box-shadow: 0 12px 30px rgba(16, 24, 40, 0.08);
                border: 1px solid var(--grid);
            }

            .card h4 {
                margin: 0 0 10px;
            }

            .tag {
                display: inline-block;
                font-size: 0.8rem;
                padding: 4px 10px;
                border-radius: 999px;
                background: #fff1e5;
                color: #9b4c27;
                margin-bottom: 10px;
            }

            pre {
                background: #0f172a;
                color: #e2e8f0;
                padding: 16px;
                border-radius: 12px;
                overflow-x: auto;
                font-size: 0.9rem;
            }

            code {
                font-family: "Courier New", Courier, monospace;
            }

            .note {
                background: #fef5e7;
                border-left: 4px solid var(--accent-3);
                padding: 14px 16px;
                border-radius: 12px;
                color: #5b3f00;
                margin-top: 16px;
            }

            .outputs {
                display: grid;
                gap: 18px;
                grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
                margin-top: 24px;
            }

            .outputs img {
                width: 100%;
                border-radius: 14px;
                border: 1px solid var(--grid);
                box-shadow: 0 8px 20px rgba(15, 23, 42, 0.1);
            }

            .qa {
                display: grid;
                gap: 16px;
                margin-top: 20px;
            }

            .qa-item {
                background: var(--card);
                padding: 18px;
                border-radius: 14px;
                border: 1px solid var(--grid);
            }

            .qa-item h5 {
                margin: 0 0 8px;
                color: var(--accent-2);
            }

            footer {
                padding: 24px;
                text-align: center;
                color: var(--muted);
            }

            @media (max-width: 700px) {
                header {
                    padding: 48px 20px 36px;
                }
                .section {
                    padding: 36px 20px;
                }
            }
        </style>
    </head>
    <body>
        <header>
            <div class="wrap">
                <div class="title">Temperature Prediction - Learning Document</div>
                <div class="subtitle">
                    A simple, complete walkthrough of predicting temperature from humidity. Every library and function is explained in clear language, with outputs included.
                </div>
                <div class="hero-grid">
                    <div class="hero-card">
                        <h3>Goal</h3>
                        <p>Predict temperature using humidity from the dataset.</p>
                    </div>
                    <div class="hero-card">
                        <h3>Model</h3>
                        <p>Linear Regression, used as a simple, interpretable baseline.</p>
                    </div>
                    <div class="hero-card">
                        <h3>Outputs</h3>
                        <p>Plots and evaluation metrics saved with the notebook.</p>
                    </div>
                </div>
            </div>
        </header>

        <section class="section">
            <div class="wrap">
                <div class="section-title">1) Import Required Libraries</div>
                <div class="lead">This step loads all tools needed for data handling, modeling, and visualization.</div>
                <div class="grid">
                    <div class="card">
                        <div class="tag">Code</div>
                        <pre><code>import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

from sklearn.model_selection import train_test_split
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_squared_error, r2_score</code></pre>
                    </div>
                    <div class="card">
                        <div class="tag">Explanation</div>
                        <p><strong>pandas (pd)</strong> handles tabular data like spreadsheets.</p>
                        <p><strong>numpy (np)</strong> provides fast math functions like square root.</p>
                        <p><strong>matplotlib.pyplot (plt)</strong> draws charts with detailed control.</p>
                        <p><strong>seaborn (sns)</strong> makes statistical plots easier and cleaner.</p>
                        <p><strong>train_test_split</strong> divides data into train and test sets.</p>
                        <p><strong>LinearRegression</strong> fits a straight line $y = mx + b$.</p>
                        <p><strong>mean_squared_error</strong> and <strong>r2_score</strong> measure model quality.</p>
                    </div>
                </div>

                <div class="card" style="margin-top: 20px;">
                    <div class="tag">Library &amp; Function Details</div>
                    <ul>
                        <li><strong>pd.read_csv(path)</strong> loads CSV into a dataframe.</li>
                        <li><strong>df.info()</strong> shows column types and missing counts.</li>
                        <li><strong>df.head()</strong> previews the first rows.</li>
                        <li><strong>df.isna().sum()</strong> counts missing values per column.</li>
                        <li><strong>df.describe()</strong> gives statistics like mean and min.</li>
                        <li><strong>df.select_dtypes(include="number")</strong> keeps numeric columns.</li>
                        <li><strong>next(...)</strong> finds the first matching column name.</li>
                        <li><strong>sns.scatterplot</strong> draws a dot chart for two variables.</li>
                        <li><strong>plt.title/plt.xlabel/plt.ylabel</strong> label plots for clarity.</li>
                        <li><strong>df.dropna()</strong> removes rows with missing values.</li>
                        <li><strong>train_test_split</strong> shuffles and splits data.</li>
                        <li><strong>LinearRegression().fit</strong> learns the best line.</li>
                        <li><strong>model.predict</strong> creates predictions.</li>
                        <li><strong>mean_squared_error</strong> measures average squared error.</li>
                        <li><strong>np.sqrt</strong> computes RMSE in the same units as temperature.</li>
                        <li><strong>r2_score</strong> shows how much variance is explained.</li>
                    </ul>
                </div>
            </div>
        </section>

        <section class="section" style="background: #f8fafc;">
            <div class="wrap">
                <div class="section-title">2) Load the Dataset</div>
                <div class="grid">
                    <div class="card">
                        <div class="tag">Code</div>
                        <pre><code>df = pd.read_csv("humidity.csv")
df.info()
df.head()</code></pre>
                    </div>
                    <div class="card">
                        <div class="tag">Explanation</div>
                        <p>This loads the CSV into memory, checks structure, and previews the first rows.</p>
                    </div>
                </div>
            </div>
        </section>

        <section class="section">
            <div class="wrap">
                <div class="section-title">3) Exploratory Data Analysis (EDA)</div>
                <div class="grid">
                    <div class="card">
                        <div class="tag">Missing Values &amp; Summary</div>
                        <pre><code>missing = df.isna().sum()
print("Missing values per column:")
print(missing)

df.describe()</code></pre>
                        <p>We count missing values and view summary statistics.</p>
                    </div>
                    <div class="card">
                        <div class="tag">Scatter Plot</div>
                        <pre><code>numeric_cols = df.select_dtypes(include="number").columns
humidity_col = next((c for c in numeric_cols if "humid" in c.lower()), None)
temp_col = next((c for c in numeric_cols if "temp" in c.lower()), None)

if humidity_col and temp_col:
        sns.scatterplot(data=df, x=humidity_col, y=temp_col)
        plt.title(f"{temp_col} vs {humidity_col}")
        plt.show()
else:
        print("Could not find humidity/temperature columns.")</code></pre>
                        <p>The scatter plot shows the relationship between humidity and temperature.</p>
                    </div>
                </div>
            </div>
        </section>

        <section class="section" style="background: #f8fafc;">
            <div class="wrap">
                <div class="section-title">4) Data Preprocessing</div>
                <div class="grid">
                    <div class="card">
                        <div class="tag">Code</div>
                        <pre><code>df_clean = df.dropna().copy()

numeric_cols = df_clean.select_dtypes(include="number").columns
humidity_col = next((c for c in numeric_cols if "humid" in c.lower()), None)
temp_col = next((c for c in numeric_cols if "temp" in c.lower()), None)

if not humidity_col or not temp_col:
        raise ValueError("Expected humidity and temperature columns.")

X = df_clean[[humidity_col]]
y = df_clean[temp_col]

X_train, X_test, y_train, y_test = train_test_split(
        X, y, test_size=0.2, random_state=42
)</code></pre>
                    </div>
                    <div class="card">
                        <div class="tag">Explanation</div>
                        <p>Rows with missing values are removed, then humidity becomes input (X) and temperature becomes target (y). We split into training and testing sets.</p>
                    </div>
                </div>
            </div>
        </section>

        <section class="section">
            <div class="wrap">
                <div class="section-title">5) Model Training</div>
                <div class="grid">
                    <div class="card">
                        <div class="tag">Code</div>
                        <pre><code>model = LinearRegression()
model.fit(X_train, y_train)

y_pred = model.predict(X_test)</code></pre>
                    </div>
                    <div class="card">
                        <div class="tag">Explanation</div>
                        <p>The model learns a best-fit straight line and predicts temperature for the test set.</p>
                    </div>
                </div>
            </div>
        </section>

        <section class="section" style="background: #f8fafc;">
            <div class="wrap">
                <div class="section-title">6) Evaluation</div>
                <div class="grid">
                    <div class="card">
                        <div class="tag">Code</div>
                        <pre><code>mse = mean_squared_error(y_test, y_pred)
rmse = np.sqrt(mse)
r2 = r2_score(y_test, y_pred)
print(f"MSE: {mse:.4f}")
print(f"RMSE: {rmse:.4f}")
print(f"R2: {r2:.4f}")

plt.figure(figsize=(6, 4))
sns.scatterplot(x=y_test, y=y_pred)
plt.xlabel("Actual Temperature")
plt.ylabel("Predicted Temperature")
plt.title("Actual vs Predicted Temperature")
min_val = min(y_test.min(), y_pred.min())
max_val = max(y_test.max(), y_pred.max())
plt.plot([min_val, max_val], [min_val, max_val], "r--")
plt.show()</code></pre>
                    </div>
                    <div class="card">
                        <div class="tag">Explanation</div>
                        <p>MSE and RMSE show average error. R2 shows how much variance the model explains. The plot checks prediction quality visually.</p>
                    </div>
                </div>
            </div>
        </section>

        <section class="section">
            <div class="wrap">
                <div class="section-title">7) Model Equation and Sample Predictions</div>
                <div class="grid">
                    <div class="card">
                        <div class="tag">Code</div>
                        <pre><code>coef = model.coef_[0] if hasattr(model, "coef_") else None
intercept = model.intercept_ if hasattr(model, "intercept_") else None
print(f"Model equation: {temp_col} = {coef:.4f} * {humidity_col} + {intercept:.4f}")

sample = pd.DataFrame({
        humidity_col: X_test.iloc[:5, 0],
        "Actual": y_test.iloc[:5],
        "Predicted": y_pred[:5]
})
sample</code></pre>
                    </div>
                    <div class="card">
                        <div class="tag">Explanation</div>
                        <p>The equation shows the learned relationship. The sample table compares real vs predicted values for a quick check.</p>
                    </div>
                </div>
            </div>
        </section>

        <section class="section" style="background: #f8fafc;">
            <div class="wrap">
                <div class="section-title">8) Conclusion</div>
                <div class="card">
                    <p>We used linear regression as a simple baseline. Humidity alone does not explain all temperature changes, so future improvements could add more features or try non-linear models.</p>
                    <div class="note">
                        If you see errors about missing columns, check the dataset column names with <strong>print(df.columns)</strong> and adjust names if needed.
                    </div>
                </div>
            </div>
        </section>

        <section class="section">
            <div class="wrap">
                <div class="section-title">Outputs From The Run</div>
                <div class="lead">The plots are saved from the notebook run and shown here.</div>
                <div class="outputs">
                    <div class="card">
                        <h4>Temperature vs Humidity</h4>
                        <img src="plot_scatter.png" alt="Temperature vs Humidity plot" />
                    </div>
                    <div class="card">
                        <h4>Actual vs Predicted Temperature</h4>
                        <img src="plot_actual_vs_pred.png" alt="Actual vs Predicted plot" />
                    </div>
                </div>

                <div class="card" style="margin-top: 20px;">
                    <div class="tag">Compact JSON Output</div>
                    <pre><code>{
    "shape": [
        701548,
        6
    ],
    "shape_after_dropna": [
        701548,
        6
    ],
    "columns": [
        "sensor_id",
        "lat",
        "lon",
        "pressure",
        "temperature",
        "humidity"
    ],
    "missing": {
        "sensor_id": 0,
        "lat": 0,
        "lon": 0,
        "pressure": 0,
        "temperature": 0,
        "humidity": 0
    },
    "metrics": {
        "mse": 144.08481646510748,
        "rmse": 12.003533499145469,
        "r2": 0.2570441670365028
    },
    "model": {
        "equation": "temperature = -0.3412 * humidity + 41.2517"
    },
    "sample_predictions": [
        {
            "humidity": 77.12,
            "Actual": 16.58,
            "Predicted": 14.936811048425259
        },
        {
            "humidity": 26.92,
            "Actual": 31.45,
            "Predicted": 32.06608595592121
        },
        {
            "humidity": 67.5,
            "Actual": 20.69,
            "Predicted": 18.21935337133584
        },
        {
            "humidity": 52.04,
            "Actual": 23.22,
            "Predicted": 23.494624089859492
        },
        {
            "humidity": 37.92,
            "Actual": 32.99,
            "Predicted": 28.31265918336234
        }
    ]
}</code></pre>
                </div>
            </div>
        </section>

        <section class="section" style="background: #f8fafc;">
            <div class="wrap">
                <div class="section-title">Interview Questions And Answers (Intermediate ML)</div>
                <div class="qa">
                    <div class="qa-item"><h5>1) What problem does this project solve?</h5><p>It predicts temperature using humidity as the input. The goal is to learn a simple relationship so we can estimate temperature from humidity values.</p></div>
                    <div class="qa-item"><h5>2) Why is this a regression problem?</h5><p>The target value (temperature) is continuous, not a category. Regression models predict continuous numbers.</p></div>
                    <div class="qa-item"><h5>3) Why start with linear regression?</h5><p>It is a simple baseline that is easy to interpret. It tells us if there is any basic linear relationship between humidity and temperature.</p></div>
                    <div class="qa-item"><h5>4) What does the model equation mean?</h5><p>The equation temperature = -0.3412 * humidity + 41.2517 means temperature tends to decrease as humidity increases. The slope shows the change per 1 unit of humidity.</p></div>
                    <div class="qa-item"><h5>5) What is the role of train-test split?</h5><p>We train on one part of the data and test on another part to see how well the model works on unseen data.</p></div>
                    <div class="qa-item"><h5>6) What does random_state=42 do?</h5><p>It fixes the random split so the results are reproducible across runs.</p></div>
                    <div class="qa-item"><h5>7) Why do we check missing values?</h5><p>Missing values can break the model or bias results. We check them to decide how to clean the data.</p></div>
                    <div class="qa-item"><h5>8) Why do we drop missing rows instead of filling them?</h5><p>Dropping is the simplest clean step when the dataset is large and missing counts are low. Filling may be better if many values are missing.</p></div>
                    <div class="qa-item"><h5>9) What is MSE and why is it used?</h5><p>Mean Squared Error measures average squared prediction error. It penalizes big mistakes more strongly.</p></div>
                    <div class="qa-item"><h5>10) What is RMSE?</h5><p>It is the square root of MSE, so the error is in the same units as temperature. This is easier to interpret.</p></div>
                    <div class="qa-item"><h5>11) What is R2?</h5><p>It measures how much of the variance in temperature is explained by the model. Closer to 1 means better fit.</p></div>
                    <div class="qa-item"><h5>12) What does an R2 around 0.26 mean here?</h5><p>It means humidity alone explains about 26% of temperature variation. There are likely other factors needed for better predictions.</p></div>
                    <div class="qa-item"><h5>13) How do you interpret the scatter plot?</h5><p>It shows the general relationship between humidity and temperature. Here the trend looks negative overall.</p></div>
                    <div class="qa-item"><h5>14) Why do we plot actual vs predicted?</h5><p>This plot quickly shows how close predictions are to real values. Points closer to the diagonal line indicate good predictions.</p></div>
                    <div class="qa-item"><h5>15) What does it mean if points are far from the diagonal line?</h5><p>It means the model is making large errors for those samples.</p></div>
                    <div class="qa-item"><h5>16) Why use only humidity as input?</h5><p>The project goal is to predict temperature from humidity specifically. This is a focused, single-feature model.</p></div>
                    <div class="qa-item"><h5>17) What other features might improve the model?</h5><p>Pressure, latitude, longitude, time, or other weather variables could explain more variance and improve accuracy.</p></div>
                    <div class="qa-item"><h5>18) What are the assumptions of linear regression?</h5><p>Linear relationship, independent errors, constant variance, and roughly normal errors.</p></div>
                    <div class="qa-item"><h5>19) How would you check linear regression assumptions?</h5><p>Use residual plots, check for patterns, and examine distribution of residuals.</p></div>
                    <div class="qa-item"><h5>20) What are residuals?</h5><p>Residuals are the differences between actual values and predictions.</p></div>
                    <div class="qa-item"><h5>21) Why might the model underperform?</h5><p>Humidity alone may not be enough to predict temperature, or the relationship may be non-linear.</p></div>
                    <div class="qa-item"><h5>22) What is overfitting in this context?</h5><p>Overfitting means the model performs well on training data but poorly on test data. With one feature and a linear model, overfitting risk is low.</p></div>
                    <div class="qa-item"><h5>23) Why is scaling not required here?</h5><p>With a single feature and linear regression, scaling does not change model performance, though it may help with interpretability in some cases.</p></div>
                    <div class="qa-item"><h5>24) What is the difference between MSE and MAE?</h5><p>MSE squares errors so large errors matter more, while MAE uses absolute errors and is less sensitive to outliers.</p></div>
                    <div class="qa-item"><h5>25) How would you handle outliers?</h5><p>You can detect them using plots or statistical methods, then decide to remove them, cap them, or use robust models.</p></div>
                    <div class="qa-item"><h5>26) Why is df.describe() useful?</h5><p>It gives quick stats like mean and max, which help identify unusual values or scale issues.</p></div>
                    <div class="qa-item"><h5>27) What does a negative slope in the equation tell you?</h5><p>As humidity increases, the model expects temperature to decrease.</p></div>
                    <div class="qa-item"><h5>28) How would you improve this model without changing the algorithm?</h5><p>Add more relevant features, clean outliers, or engineer new features like interaction terms.</p></div>
                    <div class="qa-item"><h5>29) Why is a baseline model important?</h5><p>It sets a reference point. If advanced models do not beat the baseline, they are not adding value.</p></div>
                    <div class="qa-item"><h5>30) If you used polynomial regression, what changes?</h5><p>The model can capture curves, not just a straight line, which might better represent the humidity-temperature relationship.</p></div>
                    <div class="qa-item"><h5>31) What evaluation would you add for business context?</h5><p>Define acceptable error thresholds and evaluate how often predictions fall within that tolerance.</p></div>
                    <div class="qa-item"><h5>32) How would you validate model stability?</h5><p>Use cross-validation or test the model on different time periods or locations to see if performance stays consistent.</p></div>
                </div>
            </div>
        </section>

        <footer>
            Built for the Temperature Prediction project. Designed to be readable, visual, and interview-ready.
        </footer>
    </body>
</html>
