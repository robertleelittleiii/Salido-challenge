
## The Challenge
### Objective
Define and explain a set of data models that facilitate menu item pricing determined by a combination of 3 factors: restaurant location, order type, and time of day.

### Business Requirements
* Each restaurant **Brand** using the SALIDO platform has multiple **Locations**.
* Each **Brand** has various **Menu Items** that may be used by any of its **Locations** (e.g. Cafe Bangarang's FiDi and SoHo locations both sell a "Spicy Reuben").
* Each **Brand** has various **Price Levels** (e.g. `Regular`, `Happy Hour`) that may be used by any of its **Locations**.
* Each **Menu Item** may have a price assigned for each available **Price Level** (e.g. Spicy Reuben Prices: `Regular: $4`, `Happy Hour: $2`).
* Each **Brand** has various **Order Types** (e.g. `Dine In`, `Take Out`, `Delivery`) that may be used by any of its **Locations**. 
* Each **Location** has one or more **Day Parts**, and every moment of the day must be covered by a **Day Part** (e.g. `Breakfast: [02:00, 11:00)`, `Lunch: [11:00, 17:00)`, `Dinner: [17:00, 02:00)`).
* Each **Price Level** is configured by correlating it with an **Order Type** and optional **Day Part**. These configurations are scoped to a **Location**.
  * e.g. For the FiDi location:
    * The "Regular" price level is applied if the order type is "Dine In"
    * The "Happy Hour" price level is applied if the order type is "Dine In" and the day part is "Dinner"
    * The "Delivery" price level is applied if the order type is "Delivery"
* The applicable **Price Level** for any given **Menu Item** is determined at the point of sale by assessing the **Price Level** configurations for the current **Location**. Here's the basic logic:
  * If the **Menu Item** has a price specified for the **Price Level** that correlates with both the current **Order Type** and **Day Part**, use that **Price Level**.
  * Else, if the **Menu Item** has a price specified for the **Price Level** that correlates with only the current **Order Type**, use that **Price Level**.
  * Otherwise, the **Menu Item** has no currently applicable **Price Level** and cannot be purchased.

## The Solution
### The Date Model:
![schema_drawing.db](docs/images/schema.png)

