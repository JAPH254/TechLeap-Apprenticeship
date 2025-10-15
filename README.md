# Technical Assessment Answers

## SECTION 1: Logic & Problem Solving (10 marks)

### Question 1: Second-Largest Number Function

```python
def second_largest(numbers):
    if len(numbers) < 2:
        return None
    
    unique_nums = sorted(set(numbers))
    
    if len(unique_nums) < 2:
        return None
    
    return unique_nums[-2]
```

**Approach:**
1. Check if the list has at least two elements. If not, return None.
2. Convert the list to a set to remove duplicates.
3. Sort the set of unique numbers.
4. If after removing duplicates we have less than two distinct numbers, return None.
5. Otherwise, return the second last element (which is the second largest).

---

### Question 2: Page Optimization Strategies

#### 🖼️ **Large or Unoptimized Images**
- **Cause:** Images are too large or in heavy formats (like PNG for photos)
- **Fix:** Compress and convert images to WebP or AVIF, and enable lazy loading
- **Example:**
  ```html
  <!-- Before -->
  <img src="banner.png" alt="Banner" />
  
  <!-- After -->
  <img src="banner.webp" alt="Banner" loading="lazy" />
  ```

#### 📦 **Too Many or Unminified Scripts and Styles**
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

#### 💾 **No Browser Caching**
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

**Explanation:**
1. `useEffect` runs once on mount to fetch the user data
2. `loading` is set to true while waiting for the API response
3. On success → user is updated and loading stops
4. On failure → error is set and displayed
5. Conditional rendering handles all three states clearly

---

### Question 4: Total Sales Calculation

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

**Problem:**  
The code uses `numbers.remove(i)` where `i` is the index, not the actual number. The `remove()` method deletes by value, not by index.

**Current Output:**  
`[1, 3, 5]`

**Corrected Code:**
```python
numbers = [1, 2, 3, 4, 5]
numbers = [n for n in numbers if n % 2 != 0]
print(numbers)
```

---

## SECTION 4: Version Control & Collaboration (5 marks)

### Question 6: Git Collaboration Workflow

#### 🔄 **Team Collaboration Process**

1. **Start with Latest Code:**
   ```bash
   git pull origin main
   ```

2. **Create Feature Branch:**
   ```bash
   git checkout -b feature/user-login
   ```

3. **Commit Regularly:**
   ```bash
   git add .
   git commit -m "Add user authentication form"
   ```

4. **Push Your Branch:**
   ```bash
   git push -u origin feature/user-login
   ```

5. **Open Pull Request (PR)** for code review and discussion
6. **Address Feedback** by adding more commits
7. **Merge** approved PR and delete feature branch

#### 🛠️ **Common Git Command**
```bash
git status
```
- Shows current branch
- Displays changed files
- Indicates staged/unstaged changes
- Shows branch synchronization status

#### ⚠️ **Common Problem: Merge Conflicts**

**Solution:**
1. **Identify conflicts** with `git status`
2. **Edit conflicted files** and remove conflict markers:
   ```python
   <<<<<<< HEAD
   print("This is my change")
   =======
   print("This is my teammate's change")
   >>>>>>> feature/teammate-branch
   ```
3. **Resolve** by keeping correct code and removing markers
4. **Complete the process:**
   ```bash
   git add conflicted-file.py
   git commit -m "Resolve merge conflict in conflicted-file.py"
   ```