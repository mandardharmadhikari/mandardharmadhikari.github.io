---
type : "tags"
layout : "shelf"
title: "Paper Shelf"
---

I have read following papers

* CAP Theorem Critique([Notes](/posts/2020/install-hugo/), [A critique of CAP Theorem](https://arxiv.org/pdf/1509.05393v1))

``` python
import requests

# Base URL for the example API (JSONPlaceholder is a free test API)
BASE_URL = "https://jsonplaceholder.typicode.com"

def get_posts():
    """Fetch a list of posts from the API."""
    try:
        response = requests.get(f"{BASE_URL}/posts", timeout=5)
        response.raise_for_status()  # Raise HTTPError for bad responses
        posts = response.json()
        print(f"Fetched {len(posts)} posts successfully.")
        # Display first 3 posts
        for post in posts[:3]:
            print(f"ID: {post['id']}, Title: {post['title']}")
    except requests.exceptions.RequestException as e:
        print(f"Error fetching posts: {e}")

def create_post(title, body, user_id):
    """Create a new post via POST request."""
    if not title or not body or not isinstance(user_id, int):
        print("Invalid input: title/body must be non-empty, user_id must be integer.")
        return

    payload = {
        "title": title,
        "body": body,
        "userId": user_id
    }

    try:
        response = requests.post(f"{BASE_URL}/posts", json=payload, timeout=5)
        response.raise_for_status()
        created_post = response.json()
        print("Post created successfully:")
        print(created_post)
    except requests.exceptions.RequestException as e:
        print(f"Error creating post: {e}")

if __name__ == "__main__":
    print("=== GET Request Example ===")
    get_posts()

    print("\n=== POST Request Example ===")
    create_post("My New Post", "This is the body of my new post.", 1)

```

``` csharp
using Microsoft.AspNetCore.Builder;
using Microsoft.AspNetCore.Http;
using Microsoft.Extensions.Hosting;

var builder = WebApplication.CreateBuilder(args);

// Optional: Add services (e.g., for dependency injection, database, etc.)
builder.Services.AddEndpointsApiExplorer();
builder.Services.AddSwaggerGen();

var app = builder.Build();

// Enable Swagger UI for testing
if (app.Environment.IsDevelopment())
{
    app.UseSwagger();
    app.UseSwaggerUI();
}

// Example GET endpoint
app.MapGet("/", () => "Hello, Minimal API!");

// Example GET with route parameter
app.MapGet("/greet/{name}", (string name) =>
{
    if (string.IsNullOrWhiteSpace(name))
        return Results.BadRequest("Name cannot be empty.");

    return Results.Ok($"Hello, {name}!");
});

// Example POST endpoint with JSON body
app.MapPost("/sum", (Numbers numbers) =>
{
    if (numbers == null)
        return Results.BadRequest("Invalid input.");

    return Results.Ok(new { Sum = numbers.A + numbers.B });
});

// Example PUT endpoint
app.MapPut("/update/{id}", (int id, Item item) =>
{
    if (id <= 0)
        return Results.BadRequest("Invalid ID.");

    return Results.Ok(new { Message = $"Item {id} updated.", Data = item });
});

// Example DELETE endpoint
app.MapDelete("/delete/{id}", (int id) =>
{
    if (id <= 0)
        return Results.BadRequest("Invalid ID.");

    return Results.Ok($"Item {id} deleted.");
});

app.Run();

// Record types for request bodies
record Numbers(int A, int B);
record Item(string Name, decimal Price);

```
