# used_car_market_EDA
Exploratory Data Analysis of the used car market, exploring pricing patterns, vehicle characteristics, condition, and sales performance using Python, Pandas, NumPy, and Plotly.

## Data Cleaning

| Before Cleaning | After Cleaning |
|---|---|
| ![Before](images/before_cleaning.png) | ![After](images/after_cleaning.png) |

The raw dataset was cleaned in `datacleaning_organized.ipynb` following these steps:

### 1. Duplicates
- Removed fully duplicated rows.
- Removed rows with a repeated `listing_id` (kept the first occurrence), since each listing should be unique.

### 2. Rows with Too Many Missing Values
- Dropped rows that had 3 or more missing values.

### 3. Standardizing Text Values
- Stripped extra spaces and applied title case to `brand`, `model`, `city`, `color`, `fuel_type`, `body_type`, `seller_type`, and `transmission`.
- Unified inconsistent names, for example:
  - `Bmw` → `BMW`, `Mg` → `MG`
  - `Mercedes` / `Mercedes Benz` → `Mercedes-Benz`
  - `Auto` → `Automatic`
  - `Suv` → `SUV`
  - `320I` → `320i`

### 4. Handling Missing Values
| Column(s) | Strategy |
|---|---|
| `transmission`, `fuel_type`, `color`, `city`, `seller_type` | Filled with `"Unknown"` |
| `mileage_km`, `previous_owners` | Median of the same `year` |
| `engine_cc` | Median of the same `model` |
| `photos_count` | Filled with `0` |
| `condition_rating` | Converted to numeric (Poor=1 … Excellent=4), filled with the median of the same `accident_history`, then converted back to labels |

### 5. Outliers
| Column | Rule |
|---|---|
| `year` | Removed values outside 1926–2026 |
| `mileage_km` | Removed values above 1,000,000 km |
| `price_egp` | Removed values below 60,000 or above 5,000,000 EGP |
| `engine_cc` | Removed values below 1400 cc or above 2000 cc |

`photos_count` and `previous_owners` were checked for invalid values (negative, zero, or extreme) as well.

### Output
The cleaned data is saved as `cleaned_used_cars_dataset.csv` with no missing values.

| | Rows | Columns |
|---|---|---|
| Before cleaning | 3,000 | 18 |
| After cleaning | 2,901 | 18 |

A total of 99 rows were removed (duplicates, rows with too many missing values, and outliers).