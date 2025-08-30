# Recipe Manager CLI

A command-line interface (CLI) application for managing recipes, built with Python, SQLAlchemy ORM, and Alembic for database migrations.

## Features

- **Add Recipes**: Create new recipes with title, instructions, category, and ingredients
- **List Recipes**: View all recipes with their categories
- **Search by Ingredient**: Find recipes that contain specific ingredients
- **Remove Recipes**: Delete recipes from the database
- **Database Management**: Uses SQLAlchemy ORM with Alembic migrations

## Installation

1. **Clone the repository**:
   ```bash
   git clone <repository-url>
   cd Recipe-Manager-CLI
   ```

2. **Install dependencies**:
   ```bash
   pipenv install
   ```

3. **Set up the database**:
   ```bash
   pipenv run alembic upgrade head
   ```

## Usage

Run the application:
```bash
pipenv run python -m app.main
```

### Menu Options

1. **Add Recipe**: Create a new recipe
   - Prompts for title, instructions, category, and ingredients
   - Validates that title and instructions are not empty
   - Ingredients can be entered as comma-separated values

2. **List Recipes**: Display all recipes
   - Shows recipe ID, title, and category
   - Recipes are ordered alphabetically by title

3. **Search by Ingredient**: Find recipes containing specific ingredients
   - Enter one or more ingredient names
   - Returns recipes that contain any of the specified ingredients

4. **Remove Recipe**: Delete a recipe by title
   - Enter the exact title of the recipe to remove
   - Confirms successful removal or notifies if recipe not found

5. **Quit**: Exit the application

## Database Schema

The application uses SQLAlchemy ORM with the following tables:

### Categories Table
- `id`: Primary key (Integer)
- `name`: Category name (String, unique, not null)
- `description`: Optional description (Text)

### Recipes Table
- `id`: Primary key (Integer)
- `title`: Recipe title (String, not null)
- `instructions`: Cooking instructions (Text)
- `cooking_time`: Optional cooking time in minutes (Integer)
- `category_id`: Foreign key to categories table (Integer)

### Ingredients Table
- `id`: Primary key (Integer)
- `name`: Ingredient name (String, not null)
- `quantity`: Optional quantity information (String)
- `recipe_id`: Foreign key to recipes table (Integer)

## API Functions

### `add_recipe(title, instructions, category, ingredients)`
Adds a new recipe to the database.
- **Parameters**:
  - `title`: Recipe title (required)
  - `instructions`: Cooking instructions (required)
  - `category`: Recipe category (optional, defaults to "Uncategorized")
  - `ingredients`: List of ingredient names (optional)
- **Returns**: Dictionary with added recipe title

### `list_recipes(category=None)`
Lists all recipes, optionally filtered by category.
- **Parameters**:
  - `category`: Filter by category name (optional)
- **Returns**: List of Recipe objects

### `find_by_ingredient(ingredient_name)`
Finds recipes containing specific ingredients.
- **Parameters**:
  - `ingredient_name`: Comma-separated ingredient names
- **Returns**: List of dictionaries with recipe titles and IDs

### `remove_recipe(recipe_title)`
Removes a recipe by title.
- **Parameters**:
  - `recipe_title`: Title of recipe to remove
- **Returns**: Boolean indicating success

## Database Migrations

The project uses Alembic for database migrations. To create new migrations:

```bash
pipenv run alembic revision --autogenerate -m "migration_description"
pipenv run alembic upgrade head
```

## Dependencies

- **SQLAlchemy**: Object-Relational Mapping (ORM) for database operations
- **Click**: Command-line interface creation
- **Aiosqlite**: Async SQLite support
- **Alembic**: Database migration tool

## Project Structure

```
Recipe-Manager-CLI/
├── app/
│   ├── __init__.py
│   ├── main.py          # CLI interface
│   ├── models.py        # SQLAlchemy models
│   ├── services.py      # Business logic functions
│   └── db.py           # Database configuration
├── alembic/            # Database migrations
├── Pipfile             # Dependencies
├── Pipfile.lock        # Locked dependencies
└── README.md           # This file
```

## Development

To contribute to this project:

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Add/update tests if applicable
5. Submit a pull request

## Author
Claire

