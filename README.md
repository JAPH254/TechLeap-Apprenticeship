**SECTION 1: Logic & Problem Solving (10 marks)**
**Question 1:**

 Write a function that returns the second-largest number in a given list of integers.
 (Provide your code and a short explanation of your approach.)
 
```python
def second_largest(numbers):
    if len(numbers) < 2:
        return None
    
    unique_nums = sorted(set(numbers))
    
    if len(unique_nums) < 2:
        return None
    
    return unique_nums[-2]
```

***Approach***
```
1. Check if the list has at least two elements. If not, return None.
2. Convert the list to a set to remove duplicates.
3. Sort the set of unique numbers.
4. If after removing duplicates we have less than two distinct numbers, return None.
5. Otherwise, return the second last element (which is the second largest).
```

**Question 2:**

 Explain how you would optimize a page that loads too slowly. Mention at least three causes and how you’d fix each.
 

***i. Large or Unoptimized Images***

**Cause:***
Images are too large or in heavy formats (like PNG for photos).

***Fix:***
Compress and convert images to WebP or AVIF, and enable lazy loading.

***Example:***

<!-- Before -->
<img src="banner.png" alt="Banner" />

<!-- After -->
<img src="banner.webp" alt="Banner" loading="lazy" />


***ii. Too Many or Unminified Scripts and Styles***

***Cause:***

Multiple CSS/JS files or unminified code increases HTTP requests.

Fix:
Bundle and minify assets using build tools (Webpack, Vite, Parcel) and defer scripts.

Example:

<!-- Before -->
<script src="jquery.js"></script>
<script src="main.js"></script>

<!-- After -->
<script src="bundle.min.js" defer></script>


***iii. No Browser Caching***

***Cause:***

Each visit re-downloads all files, increasing load time.

Fix:
Use caching headers or service workers to store static assets.

Example (Nginx config):

location ~* \.(js|css|png|jpg|jpeg|gif|webp|svg)$ {
    expires 30d;
    add_header Cache-Control "public";
}

***iv. Slow Server or Database Queries***

***Cause:***
Backend takes too long to respond due to heavy database queries.

Fix:
Use pagination, indexes, and optimize queries.

Example (Django):

# Before
posts = Post.objects.all()

# After – use pagination
posts = Post.objects.all()[:20]


***v. Render-Blocking Resources***

***Cause:***

CSS or JS files block the browser from rendering content quickly.

Fix:
Inline critical CSS and defer non-critical scripts.

Example:

<!-- Inline small critical CSS -->
<style>
  body { font-family: Arial; background: #fff; }
</style>

<!-- Defer non-critical JS -->
<script src="analytics.js" defer></script>

**SECTION 2: Web/Software Development (15 marks)**
**Question 3 (Front-end):**

 You are creating a simple profile page that fetches user data from an API (https://jsonplaceholder.typicode.com/users/1).
 Explain or show code for:
Fetching and displaying the user’s name and email.


Handling the loading and error states.


(You may use plain JS, React, or any stack you’re comfortable with.)


**Question 4 (Back-end / Logic):**

 A small store wants to calculate total sales from this dataset:
[
  {"item": "Pen", "price": 20, "quantity": 3},
  {"item": "Book", "price": 200, "quantity": 2},
  {"item": "Bag", "price": 800, "quantity": 1}
]

Write a short function to calculate the total revenue.



**SECTION 3: Debugging & Reasoning (10 marks)**
**Question 5:**

 You’ve been given this code snippet:
numbers = [1, 2, 3, 4, 5]
for i in range(len(numbers)):
    if i % 2 == 0:
        numbers.remove(i)
print(numbers)

What’s wrong with the code?


What will it output?


How would you fix it to remove even numbers correctly?


**SECTION 4: Version Control & Collaboration (5 marks)**
**Question 6:**

 Explain how you would use Git to collaborate on a team project with other developers.
 Mention at least:
One common Git command you use often.


One problem you’ve faced while using Git and how you solved it.

