# Movies Explorer Backend

A comprehensive Django REST API for exploring movies, actors, directors, and genres. Built with Django REST Framework, PostgreSQL, and comprehensive Swagger documentation.

## Features

- **Complete CRUD operations** for Movies, Actors, Directors, and Genres
- **Advanced filtering** capabilities for all entities
- **Comprehensive API documentation** with Swagger/OpenAPI
- **Relationship management** between movies, actors, directors, and genres
- **Unit tests** with good coverage
- **Docker support** with PostgreSQL
- **Sample data** for testing and development
- **Admin interface** for data management

## Tech Stack

- **Backend**: Django 5.2.8, Django REST Framework 3.15.2
- **Database**: PostgreSQL 15
- **Documentation**: drf-spectacular (Swagger/OpenAPI)
- **Filtering**: django-filter
- **Containerization**: Docker & Docker Compose

## API Endpoints

### Movies

- `GET /api/movies/` - List all movies with filtering
- `POST /api/movies/` - Create a new movie
- `GET /api/movies/{id}/` - Get movie details
- `PUT /api/movies/{id}/` - Update movie
- `PATCH /api/movies/{id}/` - Partial update movie
- `DELETE /api/movies/{id}/` - Delete movie
- `GET /api/movies/by_genre/?name={genre}` - Movies by genre
- `GET /api/movies/by_director/?name={director}` - Movies by director

### Actors

- `GET /api/actors/` - List all actors with filtering
- `POST /api/actors/` - Create a new actor
- `GET /api/actors/{id}/` - Get actor details with movies
- `PUT /api/actors/{id}/` - Update actor
- `DELETE /api/actors/{id}/` - Delete actor

### Directors

- `GET /api/directors/` - List all directors with filtering
- `POST /api/directors/` - Create a new director
- `GET /api/directors/{id}/` - Get director details with movies
- `PUT /api/directors/{id}/` - Update director
- `DELETE /api/directors/{id}/` - Delete director

### Genres

- `GET /api/genres/` - List all genres
- `POST /api/genres/` - Create a new genre
- `GET /api/genres/{id}/` - Get genre details
- `PUT /api/genres/{id}/` - Update genre
- `DELETE /api/genres/{id}/` - Delete genre

## Filtering Options

### Movies

- `title` - Filter by title (contains)
- `release_year` - Filter by exact year
- `release_year_gte` - Filter by year greater than or equal
- `release_year_lte` - Filter by year less than or equal
- `director` - Filter by director name (contains)
- `director_id` - Filter by director ID
- `actor` - Filter by actor name (contains)
- `actor_id` - Filter by actor ID
- `genre` - Filter by genre name (contains)
- `genre_id` - Filter by genre ID
- `rating_gte` - Filter by rating greater than or equal
- `rating_lte` - Filter by rating less than or equal

### Actors

- `name` - Filter by name (contains)
- `nationality` - Filter by nationality (contains)
- `movie` - Filter by movie title (contains)
- `movie_id` - Filter by movie ID
- `genre` - Filter by genre of movies acted in
- `genre_id` - Filter by genre ID of movies acted in

### Directors

- `name` - Filter by name (contains)
- `nationality` - Filter by nationality (contains)
- `movie` - Filter by movie title (contains)
- `movie_id` - Filter by movie ID

## Quick Start

### Using Docker (Recommended)

1. **Clone the repository**

   ```bash
   git clone <repository-url>
   cd movies_explorere_backend
   ```
2. **Build and run with Docker Compose**

   ```bash
   docker-compose up --build
   ```
3. **Access the application**

   - API: http://localhost:8000/api/
   - Swagger Documentation: http://localhost:8000/api/docs/
   - ReDoc Documentation: http://localhost:8000/api/redoc/
   - Admin Interface: http://localhost:8000/admin/

### Local Development

1. **Install dependencies**

   ```bash
   pip install -r requirements.txt
   ```
2. **Set up PostgreSQL database**

   ```bash
   # Create database
   createdb movies_explorer
   ```
3. **Run migrations**

   ```bash
   python manage.py migrate
   ```
4. **Load sample data**

   ```bash
   python manage.py load_sample_data
   ```
5. **Create superuser (optional)**

   ```bash
   python manage.py createsuperuser
   ```
6. **Run development server**

   ```bash
   python manage.py runserver
   ```

## Testing

Run the test suite:

```bash
python manage.py test
```

Run tests with coverage:

```bash
pip install coverage
coverage run --source='.' manage.py test
coverage report
```

## API Documentation

The API is fully documented using Swagger/OpenAPI specification:

- **Swagger UI**: http://localhost:8000/api/docs/
- **ReDoc**: http://localhost:8000/api/redoc/
- **OpenAPI Schema**: http://localhost:8000/api/schema/

## Sample API Usage

### Get all movies

```bash
curl http://localhost:8000/api/movies/
```

### Filter movies by genre

```bash
curl "http://localhost:8000/api/movies/?genre=Action"
```

### Filter movies by director and year

```bash
curl "http://localhost:8000/api/movies/?director=Nolan&release_year_gte=2010"
```

### Create a new movie

```bash
curl -X POST http://localhost:8000/api/movies/ \
  -H "Content-Type: application/json" \
  -d '{
    "title": "Dune",
    "release_year": 2021,
    "director_id": 1,
    "genre_ids": [1, 2],
    "actor_ids": [1, 2],
    "rating": 8.1,
    "duration": 155,
    "plot": "A noble family becomes embroiled in a war for control over the galaxy."
  }'
```

## Database Schema

### Models Relationships

- **Movie** belongs to one **Director** (Many-to-One)
- **Movie** can have multiple **Actors** (Many-to-Many)
- **Movie** can belong to multiple **Genres** (Many-to-Many)

### Key Fields

- **Movie**: title, release_year, duration, plot, poster_url, rating
- **Actor**: name, birth_date, nationality, biography
- **Director**: name, birth_date, nationality, biography
- **Genre**: name, description

## Environment Variables

- `DATABASE_URL`: PostgreSQL connection string (for production)
- `DEBUG`: Django debug mode (default: True)
- `SECRET_KEY`: Django secret key

## License

This project is licensed under the MIT License.
