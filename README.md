# Extra Lab: Posts Feature (Full Stack)

## Setup

1. Clone both the **backend** and **frontend** templates.
2. Follow the setup instructions in each repository.
3. Run both applications.
4. Verify everything works by attempting to **log in**.

---

## Backend

### 1. Create Post Model

Create a new model called `Post` with the following fields:

* `imageURL`: `String` (required)
* `postBody`: `String` (required)
* `owner`: `ObjectId` (required, references the `User` model)

---

### 2. Controller & Routing

* Create a controller for the `Post` model.
* Mount the controller in `server.js`.

---

### 3. Route Protection Rules

* Only **logged-in users** can:

  * Create posts
  * Update posts
  * Delete posts
* All users can:

  * View posts

* Protect the routes for creating, updating and deleting posts. The user should only be able to see all the posts and not perform any other actions


---

### 4. Implement Routes

#### GET `/posts`

* Fetch all posts from the database
* Use `try/catch` for error handling (console.log the error and send it back as a clean response)

---

#### POST `/posts`

* Allow only authenticated users (add `verifyToken` middleware)
* Make sure to add the `id` of the logged in user as the owner of the post. **HINT**: the verifyToken will make it so `req.user` contains the object of the logged in user and `req.user._id` is the id of the logged in user


**Hint:**
`verifyToken` adds the user object to `req.user`

**Test in Postman:**

* Test this route on postman (**HINT**: remember to log in first with a request to `/auth/sign-in` and send the token with the request)


---

#### PUT `/posts/:id`

* Only authenticated users can update
* Users can **only update their own posts**
* IMPORTANT: user should only be able to edit their own posts. Remember the Post model contains an owner field and the request should come with the token containing the id of the logged in user (like the previous step for POST)

**Important:**

* Compare:

  * `req.user._id`
  * `post.owner`

---

#### DELETE `/posts/:id`

* Only authenticated users can delete
* Users can **only delete their own posts**

---

## Frontend

### 1. AllPosts Page

Create: `AllPosts.jsx` (inside `pages` folder)

* Make an Axios request to:

  * `GET /posts`
* Display all posts using `.map()`
* Add a link to this page in the **Navbar**
* This page is accessible to **all users**

---

### 2. CreatePost Page

Create: `CreatePost.jsx`

* Only visible to **logged-in users**
* Send a POST request to `/posts`

  * Include the authentication token from localStorage (**HINT**: `localstorage.getItem('token')`)   
* On success:

  * Redirect to `AllPosts`

---

### 3. Update Post

* Implement update functionality similar to create:

  * Authenticated users only
  * Must own the post

---

### 4. Delete Post

* Add a **Delete button** in `AllPosts.jsx`
* Only show the button if:

  * Logged-in user is the **owner** of the post
