# Diagrama de clases Restaurant menu
```mermaid
classDiagram
direction TB
    class MenuItem {
        +string name
        +float price
        +calculate_price(quantity: int) float
        +__str__() str
    }

    class Beverage {
        +string size
        +bool is_alcoholic
        +__init__(name: str, price: float, size: str, is_alcoholic: bool)
        +__str__() str
    }

    class Appetizer {
        +bool is_vegan
        +string portion_size
        +__init__(name: str, price: float, is_vegan: bool, portion_size: str)
        +__str__() str
    }

    class MainCourse {
        +string cuisine
        +int calories
        +__init__(name: str, price: float, cuisine: str, calories: int)
        +__str__() str
    }

    class Order {
        +List(MenuItem,int)
        +add_item(item: MenuItem, quantity: int)
        +beverage_discount() float
        +appetizer_main_combo_discount() float
        +extra_total_discount(subtotal_after: float) float
        +calculate_total() float
        +__str__() str
    }


    MenuItem <|-- Beverage
    MenuItem <|-- Appetizer
    MenuItem <|-- MainCourse
    Order --> MenuItem
```
