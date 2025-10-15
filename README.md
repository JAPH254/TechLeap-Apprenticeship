# Technical Assessment Answers

## SECTION 1: Logic & Problem Solving (10 marks)

### Question 1: Second-Largest Number Function

**Question:** Write a function that returns the second-largest number in a given list of integers.

```python
def second_largest(numbers):
    if len(numbers) < 2:
        return None
    
    unique_nums = sorted(set(numbers))
    
    if len(unique_nums) < 2:
        return None
    
    return unique_nums[-2]
```

**Approach Explanation:**
```
1. Check if the list has at least two elements. If not, return None.
2. Convert the list to a set to remove duplicates.
3. Sort the set of unique numbers.
4. If after removing duplicates we have less than two distinct numbers, return None.
5. Otherwise, return the second last element (which is the second largest).
```

---

### Question 2: Page Optimization Strategies

**Question:** Explain how you would optimize a page that loads too slowly. Mention at least three causes and how you'd fix each.

####  **Large or Unoptimized Images**
- **Cause:** Images are too large or in heavy formats (like PNG for photos)
- **Fix:** Compress and convert images to WebP or AVIF, and enable lazy loading
- **Example:**
  ```html
  <!-- Before -->
  <img src="banner.png" alt="Banner" />
  
  <!-- After -->
  <img src="banner.webp" alt="Banner" loading="lazy" />
  ```

####  **Too Many or Unminified Scripts and Styles**
- **Cause:** Multiple CSS/JS files or unminified code increases HTTP requests
- **Fix:** Bundle and minify assets using build tools (Webpack, Vite, Parcel) and defer scripts
- **Example:**
  ```html
  <!-- Before -->
  <script src="jquery.js"></script>
  <script src="main.js"></script>
  
  <!-- After -->
  <script src="bundle.min.js" defer></script>
  ```

####  **No Browser Caching**
- **Cause:** Each visit re-downloads all files, increasing load time
- **Fix:** Use caching headers or service workers to store static assets
- **Example (Nginx config):**
  ```nginx
  location ~* \.(js|css|png|jpg|jpeg|gif|webp|svg)$ {
      expires 30d;
      add_header Cache-Control "public";
  }
  ```

---

## SECTION 2: Web/Software Development (15 marks)

### Question 3: User Profile Component (React)

**Question:** You are creating a simple profile page that fetches user data from an API. Explain or show code for fetching and displaying the user's name and email, and handling loading and error states.

```jsx
import React, { useEffect, useState } from "react";

const UserProfile = () => {
  const [user, setUser] = useState(null);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);

  useEffect(() => {
    fetch("https://jsonplaceholder.typicode.com/users/1")
      .then((response) => {
        if (!response.ok) throw new Error("Failed to fetch user data");
        return response.json();
      })
      .then((data) => {
        setUser(data);
        setLoading(false);
      })
      .catch((err) => {
        setError(err.message);
        setLoading(false);
      });
  }, []);

  if (loading) return <p>Loading user data...</p>;
  if (error) return <p style={{ color: "red" }}>Error: {error}</p>;

  return (
    <div style={{ padding: "1rem", fontFamily: "sans-serif" }}>
      <h2>User Profile</h2>
      <p><strong>Name:</strong> {user.name}</p>
      <p><strong>Email:</strong> {user.email}</p>
    </div>
  );
};

export default UserProfile;
```

**Approach Explanation:**
```
1. useEffect runs once on mount to fetch the user data.
2. loading is set to true while waiting for the API response.
3. On success → user is updated and loading stops.
4. On failure → error is set and displayed.
5. Conditional rendering handles all three states clearly.
```

---

### Question 4: Total Sales Calculation

**Question:** A small store wants to calculate total sales from this dataset. Write a short function to calculate the total revenue.

```python
def calculate_total_sales(data):
    total = sum(item["price"] * item["quantity"] for item in data)
    return total

# Example usage
sales = [
    {"item": "Pen", "price": 20, "quantity": 3},
    {"item": "Book", "price": 200, "quantity": 2},
    {"item": "Bag", "price": 800, "quantity": 1}
]

print("Total Revenue:", calculate_total_sales(sales))
```

---

## SECTION 3: Debugging & Reasoning (10 marks)

### Question 5: Code Analysis

**Question:** You've been given this code snippet. What's wrong with the code? What will it output? How would you fix it to remove even numbers correctly?

```python
numbers = [1, 2, 3, 4, 5]
for i in range(len(numbers)):
    if i % 2 == 0:
        numbers.remove(i)
print(numbers)
```

**Problem Analysis:**
```
i is an index, not the actual number.
The code calls numbers.remove(i) — but remove() deletes a value, not an index.
So it's removing elements whose value equals the index, not even numbers.
```

**Current Output:**
```
[1, 3, 5]
```

**Corrected Code:**
```python
numbers = [1, 2, 3, 4, 5]
numbers = [n for n in numbers if n % 2 != 0]
print(numbers)
```

---

## SECTION 4: Version Control & Collaboration (5 marks)

### Question 6: Git Collaboration Workflow

**Question:** Explain how you would use Git to collaborate on a team project with other developers. Mention at least one common Git command you use often and one problem you've faced while using Git and how you solved it.

####  **Team Collaboration Process**

```bash
# Start with Latest Code
git pull origin main

# Create Feature Branch
git checkout -b feature/user-login

# Commit Regularly
git add .
git commit -m "Add user authentication form"

# Push Your Branch
git push -u origin feature/user-login
```

**Process Explanation:**
```
1. Start with the latest code from main branch
2. Create descriptive feature branches for isolation
3. Make small, logical commits with clear messages
4. Push branches to remote repository
5. Open Pull Requests for code review and discussion
6. Address feedback and merge approved changes
7. Delete feature branches after merging
```

####  **Common Git Command**
```bash
git status
```

**Usage Explanation:**
```
I use this command constantly throughout my workflow. It gives you a quick overview of:
- Which branch you are currently on
- What files have been changed since your last commit
- What changes are staged vs unstaged
- Branch synchronization status with remote
```

####  **Common Problem: Merge Conflicts**

**Problem Description:**
```
Merge conflicts occur when multiple developers modify the same parts of the same file.
Git cannot automatically determine which changes to keep.
```

**Solution:**
```bash
# 1. Identify conflicts
git status

# 2. Resolve conflicts in files by editing and removing markers:
# <<<<<<< HEAD
# my changes
# =======
# their changes  
# >>>>>>> branch-name

# 3. Complete the resolution
git add resolved-file.py
git commit -m "Resolve merge conflict in resolved-file.py"
```