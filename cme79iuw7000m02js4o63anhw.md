---
title: "Step-by-Step Guide to Creating Your First Laravel CRUD App"
seoTitle: "Laravel CRUD App: A Beginner's Guide"
seoDescription: "Learn how to create a full CRUD app with Laravel, perfect for beginners and developers wanting to refresh their knowledge"
datePublished: Mon Aug 11 2025 15:23:42 GMT+0000 (Coordinated Universal Time)
cuid: cme79iuw7000m02js4o63anhw
slug: step-by-step-guide-to-creating-your-first-laravel-crud-app
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/cfE5i6sHCFA/upload/a8795c19536add2c0c21671f2d0b2986.jpeg
tags: laravel, beginners, composer

---

Laravel is an elegant framework that simplifies backend development. This tutorial guides you through creating your **first CRUD (Create, Read, Update, Delete)** application — a **Blog Post Management System**. Perfect for beginners and developers looking to refresh their Laravel knowledge.

## 🚧 Introduction

🔹 **Why Laravel?**

* Developer-friendly syntax
    
* Built-in tools (Artisan, Eloquent ORM, Blade templating)
    
* Rapid CRUD development
    

🔹 **Project Objective**:

Create a **Blog Post Manager** with full CRUD functionality.

🔹 **Tech Stack**:

* Laravel (v10 or latest)
    
* Composer
    
* PHP (≥8.1)
    
* XAMPP / Laravel Sail / Valet
    

## 🔧 Step 1: Configure Your Laravel Environment

### ⚙️ Install Laravel

```bash
composer create-project laravel/laravel blog-crud
cd blog-crud

```

Or use Laravel Sail for Docker-powered setup:

```bash
./vendor/bin/sail up

```

### 🌐 Set Up Environment

* Edit `.env` file for DB settings:
    

```php
DB_DATABASE=blog_db
DB_USERNAME=root
DB_PASSWORD=

```

* Create database manually or via migration
    
* Run migrations:
    

```bash
php artisan migrate

```

---

## 🧱 Step 2: Generate Model, Migration & Controller

Run one-liner to generate all three:

```bash
php artisan make:model Post -mcr

```

🔧 In `database/migrations/xxxx_create_posts_table.php`:

```php
Schema::create('posts', function (Blueprint $table) {
    $table->id();
    $table->string('title');
    $table->text('body');
    $table->timestamps();
});

```

Run migration:

```bash
php artisan migrate

```

---

## 🛣️ Step 3: Configure Routes

In `routes/web.php`, register a **resource route**:

```php
use App\\Http\\Controllers\\PostController;

Route::resource('posts', PostController::class);

```

This creates all 7 RESTful routes automatically (`index`, `create`, `store`, etc.)

---

## 🖼️ Step 4: Build Blade Templates

🔹 Create a `resources/views/posts` directory

🔹 Add files: `index.blade.php`, `create.blade.php`, `edit.blade.php`, `show.blade.php`

Each form should use:

```php
@csrf
@method('PUT') {{-- only for edit --}}

```

Use route helpers like:

```php
<form action="{{ route('posts.store') }}" method="POST">

```

---

## 🧠 Step 5: Add Controller Logic

Inside `PostController.php`:

```php
public function index() {
    $posts = Post::all();
    return view('posts.index', compact('posts'));
}

public function create() {
    return view('posts.create');
}

public function store(Request $request) {
    Post::create($request->all());
    return redirect()->route('posts.index');
}

public function edit(Post $post) {
    return view('posts.edit', compact('post'));
}

public function update(Request $request, Post $post) {
    $post->update($request->all());
    return redirect()->route('posts.index');
}

public function destroy(Post $post) {
    $post->delete();
    return redirect()->route('posts.index');
}

```

👉 Add `fillable` fields in `Post.php`:

```php
protected $fillable = ['title', 'body'];
```

## ✅ Step 6: Test Your Application

```bash
php artisan serve
```

Visit: [`http://127.0.0.1:8000/posts`](http://127.0.0.1:8000/posts)

Perform the full **CRUD cycle**:

* 📝 Create
    
* 📖 Read
    
* ✏️ Update
    
* ❌ Delete
    

You've now created a **fully functional CRUD app** with Laravel!

Next steps for scaling this project:

* ✅ Add form validation (`$request->validate()`)
    
* ✅ Implement Laravel UI or Breeze for authentication
    
* ✅ Introduce Eloquent relationships (e.g., `User → Posts`)
    
* ✅ Deploy via Laravel Forge or Vercel (with APIs)
    

## 📁 Supplementary Resources

* [Laravel Official Docs](https://laravel.com/docs)