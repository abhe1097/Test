## Create Laravel API with Postgres database

### Step 1: Laravel Init
To initialize a Laravel project, create a parent folder:

```sh
mkdir project-folder
```

Inside that folder, run the command:

```sh
composer create-project laravel/laravel .
```

### Installing PostgreSQL with Podman
#### Pull the PostgreSQL Image
```sh
podman pull docker.io/library/postgres:latest
```

#### Run the PostgreSQL Container
```sh
podman run -d \
  --name postgres \
  -e POSTGRES_USER=myuser \
  -e POSTGRES_PASSWORD=mypassword \
  -e POSTGRES_DB=mydatabase \
  -v /home/abhishek/p-data:/var/lib/postgresql/data \
  docker.io/library/postgres:latest
```

#### Explanation of parameters:
- `-d`: Run the container in detached mode.
- `--name postgres`: Assigns a name to the container.
- `-e POSTGRES_USER=myuser`: Sets the database username.
- `-e POSTGRES_PASSWORD=mypassword`: Sets the database password.
- `-e POSTGRES_DB=mydatabase`: Creates a default database.
- `-v /home/abhishek/p-data:/var/lib/postgresql/data`: Maps a volume for persistent storage.

#### Verify PostgreSQL Installation
```sh
podman ps
```

#### Restarting and Stopping PostgreSQL
```sh
podman stop postgres
```
```sh
podman start postgres
```

#### Connecting to PostgreSQL
```sh
podman exec -it postgres psql -U myuser -d mydatabase
```

---

### Step 2: Configure the database
In the `database.php` file within the `app/config` folder, the default connection should be changed:

```php
'default' => env('DB_CONNECTION', 'pgsql')
```

Go to the root directory and find the `.env` file. Modify it as per your project needs:

```ini
DB_CONNECTION=pgsql
DB_HOST=127.0.0.1
DB_PORT=5432
DB_DATABASE=laravel_todos
DB_USERNAME=myuser
DB_PASSWORD=mypassword
DATABASE_URL=
```

---

### Step 3: Create app
Navigate to the root folder and run the command:

```sh
php artisan make:model Todo -a
```

This will create a model, controller, and a migration file.

---

### Step 4: Create Models and Schemas
Edit the `Todo.php` file in the `app/Models` folder:

```php
<?php
namespace App\Models;
use Illuminate\Database\Eloquent\Factories\HasFactory;
use Illuminate\Database\Eloquent\Model;
use Illuminate\Database\Eloquent\Concerns\HasUuids;
use Illuminate\Support\Str;

class Todo extends Model
{
   use HasFactory, HasUuids;

   protected $table = 'todos';
   protected $primaryKey = 'id';
   public $incrementing = false;
   protected $keyType = 'string'; // UUIDs stored as strings
   protected $fillable = ['id', 'title', 'completed'];

   protected static function boot()
   {
       parent::boot();
       static::creating(function ($model) {
           if (empty($model->id)) {
               $model->id = (string) Str::uuid(); // Automatically generate UUID
           }
       });
   }
}
```

Create a new response model in `app/Models/TodoResponse.php`:

```php
<?php
namespace App\Models;

class TodoResponse
{
 public bool $success;
 public string $message;
 public $payload;

 public function __construct(bool $success, string $message, $payload)
 {
   $this->success = $success;
   $this->message = $message;
   $this->payload = $payload;
 }

 public function to_json()
 {
   return [
     "success" => $this->success,
     "message" => $this->message,
     "payload" => $this->payload
   ];
 }
}
```

---

### Step 5: Edit the migration file
Modify the migration file in `database/migrations`:

```php
<?php
use Illuminate\Database\Migrations\Migration;
use Illuminate\Database\Schema\Blueprint;
use Illuminate\Support\Facades\Schema;

return new class extends Migration
{
   public function up(): void
   {
       Schema::create('todos', function (Blueprint $table) {
           $table->uuid('id')->primary();
           $table->string("title");
           $table->boolean("completed");
           $table->timestamps();
       });
   }

   public function down(): void
   {
       Schema::dropIfExists('todos');
   }
};
```

---

### Step 6: Migrate the database
Connect to PostgreSQL and create the database:

```sh
podman exec -it my_postgres /bin/bash
psql -U myuser -d postgres
CREATE DATABASE laraveltodos;
```

Run the migration command:

```sh
php artisan migrate
```

Verify the database tables:

```sh
psql -U myuser -d laraveltodos
\d todos
SELECT * FROM todos;
```

---

### Step 7: Create the controllers
Modify the `TodoController.php` in `app/Http/Controllers`:

```php
public function index()
{
   return response()->json(["success" => true, "message" => "Got todos", "data" => Todo::orderBy("updated_at", "desc")->get()], 200);
}
```

---

### Step 8: Create the routes
Modify `routes/api.php`:

```php
use Illuminate\Support\Facades\Route;
use App\Http\Controllers\TodoController;

Route::prefix('/v1')->group(function () {
   Route::get("/todos", [TodoController::class, "index"]);
   Route::get("/todos/{id}", [TodoController::class, "show"]);
   Route::post("/todos", [TodoController::class, "store"]);
   Route::put("/todos/{id}", [TodoController::class, "update"]);
   Route::delete("/todos/{id}", [TodoController::class, "delete"]);
});
```

---

Your Laravel API with PostgreSQL is now set up! 🚀


