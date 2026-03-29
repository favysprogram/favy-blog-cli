# favy-blog-cli
blog
import json
import os

FILE_NAME = "posts.json"

# Load posts
def load_posts():
    if not os.path.exists(FILE_NAME):
        return []
    with open(FILE_NAME, "r") as file:
        return json.load(file)

# Save posts
def save_posts(posts):
    with open(FILE_NAME, "w") as file:
        json.dump(posts, file, indent=4)

# Create post
def create_post():
    title = input("Enter post title: ")
    content = input("Enter post content: ")

    posts = load_posts()
    post = {
        "id": len(posts) + 1,
        "title": title,
        "content": content
    }
    posts.append(post)
    save_posts(posts)

    print("✅ Post created successfully!")

# View all posts
def view_posts():
    posts = load_posts()
    if not posts:
        print("No posts available.")
        return

    for post in posts:
        print(f"{post['id']}. {post['title']}")

# Read single post
def read_post():
    post_id = int(input("Enter post ID: "))
    posts = load_posts()

    for post in posts:
        if post["id"] == post_id:
            print("\n---")
            print(f"Title: {post['title']}")
            print(f"Content: {post['content']}")
            print("---\n")
            return

    print("❌ Post not found.")

# Delete post
def delete_post():
    post_id = int(input("Enter post ID to delete: "))
    posts = load_posts()

    new_posts = [post for post in posts if post["id"] != post_id]

    save_posts(new_posts)
    print("🗑️ Post deleted.")

# CLI menu
def menu():
    while True:
        print("\n📘 Blog CLI")
        print("1. Create Post")
        print("2. View Posts")
        print("3. Read Post")
        print("4. Delete Post")
        print("5. Exit")

        choice = input("Choose an option: ")

        if choice == "1":
            create_post()
        elif choice == "2":
            view_posts()
        elif choice == "3":
            read_post()
        elif choice == "4":
            delete_post()
        elif choice == "5":
            print("Goodbye 👋")
            break
        else:
            print("Invalid choice.")

if __name__ == "__main__":
    menu()
