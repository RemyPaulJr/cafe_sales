Columns:
Transaction ID - Non null - Object
Item - Non null - Object
Quantity - Non null - Object
Price Per Unit - Non null - Object
Total Spent - Non null - Object
Payment Method - Non null - Object
Location - Non null - Object
Transaction Date - Non null - Object

We have 8 columns all of object data type.

Null counts:
1 - 0
2 - 333
3 - 138
4 - 179
5 - 173
6 - 2579
7 - 3265    
8 - 159

Each transaction is unique. This column needs to be unique so that is good.

Unique Values:
- Transaction ID - All unique
- Item - UNKNOWN, ERROR - Need to handle these, format all lowercase and group similar variations ("latte", "late", "latte ")
- Quantity - UKNOWN, ERROR - Can calulate this using total spent / price per unit
- Price Per Unit - ERROR, UNKNOWN - Can calulate these using the total spent / quantity
- Total Spent - UNKNOWN, ERROR - Can calculate this using Total Spent / Price Per Unit, but only if both are present and valid. Otherwise, flag the row for review. 
- Payment Method - ERROR, UNKNOWN - Can use the mode? or impute based on related columns (large transactions -> credit card), Will be either digital wallet, credit card, or cash
- Location - Impute missing or placeholder values using the mode after removing ‘ERROR’ and ‘UNKNOWN’ to avoid skew.
- Transaction Date - UKNOWN, ERROR - try parsing, flag ones that can't be parsed, or drop or replace unparseable dates. Derived columns like day of the week, hour of the day for further analysis?? Use errors='coerce' with pd.to_datetime

> Some of these columns also have NaN 

