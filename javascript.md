# Modern JavaScript Tutorial

The Modern JavaScript Tutorial is a comprehensive educational resource covering JavaScript from fundamentals to advanced topics. Published at javascript.info, it provides in-depth explanations of the JavaScript language, browser APIs, and web development techniques through well-structured articles, interactive examples, and practical tasks. The tutorial is organized into numbered chapters and sections, each containing markdown-formatted articles with code examples, exercises with solutions, and visual diagrams.

The repository structure uses a hierarchical folder system where each chapter and article resides in its own directory named with a number prefix for ordering (e.g., `1-js`, `2-ui`). Articles are written in an enhanced markdown format with `article.md` files for content, `task.md` for exercises, and `solution.md` for answers. The content covers core JavaScript (`1-js`), browser DOM and events (`2-ui`), frames and windows (`3-frames-and-windows`), binary data (`4-binary`), network requests (`5-network`), data storage (`6-data-storage`), animations (`7-animation`), web components (`8-web-components`), and regular expressions (`9-regular-expressions`).

## Variables and Data Types

Declaring and working with JavaScript variables and primitive types

```javascript
// Variable declarations
let name = "John";
const age = 30;
var oldStyle = "avoid using var";

// String operations
let str = "Hello, World!";
console.log(str.length);        // 13
console.log(str.toUpperCase()); // "HELLO, WORLD!"
console.log(str.slice(0, 5));   // "Hello"

// Template literals
let greeting = `Hello, ${name}! You are ${age} years old.`;
console.log(greeting); // "Hello, John! You are 30 years old."

// Numbers
let price = 120;
let discount = 0.1;
let finalPrice = price * (1 - discount);
console.log(finalPrice); // 108

// Type conversion
let strNum = "123";
let num = Number(strNum);
console.log(num + 1); // 124
```

## Array Methods

Manipulating arrays with built-in methods

```javascript
// Creating and modifying arrays
let arr = [1, 2, 3, 4, 5];

// map - transform each element
let doubled = arr.map(x => x * 2);
console.log(doubled); // [2, 4, 6, 8, 10]

// filter - select elements matching criteria
let evens = arr.filter(x => x % 2 === 0);
console.log(evens); // [2, 4]

// reduce - accumulate values
let sum = arr.reduce((acc, curr) => acc + curr, 0);
console.log(sum); // 15

// splice - modify array in place
let items = ["I", "study", "JavaScript"];
items.splice(1, 1); // remove 1 element at index 1
console.log(items); // ["I", "JavaScript"]

// slice - create copy
let copy = arr.slice(1, 3);
console.log(copy); // [2, 3]

// find - get first matching element
let users = [
  {id: 1, name: "John"},
  {id: 2, name: "Pete"},
  {id: 3, name: "Mary"}
];
let user = users.find(u => u.id === 2);
console.log(user); // {id: 2, name: "Pete"}
```

## Object Basics

Creating and manipulating JavaScript objects

```javascript
// Object literal
let user = {
  name: "John",
  age: 30,
  isAdmin: true
};

// Accessing properties
console.log(user.name);     // "John"
console.log(user["age"]);   // 30

// Adding/modifying properties
user.email = "john@example.com";
user.age = 31;

// Deleting properties
delete user.isAdmin;

// Checking property existence
console.log("name" in user);    // true
console.log("isAdmin" in user); // false

// Iterating over properties
for (let key in user) {
  console.log(`${key}: ${user[key]}`);
}
// Output:
// name: John
// age: 31
// email: john@example.com

// Object.keys, Object.values, Object.entries
let keys = Object.keys(user);
console.log(keys); // ["name", "age", "email"]

let values = Object.values(user);
console.log(values); // ["John", 31, "john@example.com"]

let entries = Object.entries(user);
console.log(entries);
// [["name", "John"], ["age", 31], ["email", "john@example.com"]]
```

## Classes

Creating reusable object templates with ES6 classes

```javascript
// Basic class definition
class User {
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }

  sayHi() {
    return `Hi, I'm ${this.name}`;
  }

  getAge() {
    return this.age;
  }
}

// Creating instances
let john = new User("John", 30);
console.log(john.sayHi());    // "Hi, I'm John"
console.log(john.getAge());   // 30

// Class inheritance
class Admin extends User {
  constructor(name, age, role) {
    super(name, age);
    this.role = role;
  }

  sayHi() {
    return `${super.sayHi()}. I'm an ${this.role}.`;
  }

  hasAccess(resource) {
    return this.role === "superadmin" || resource === "public";
  }
}

let admin = new Admin("Alice", 28, "superadmin");
console.log(admin.sayHi()); // "Hi, I'm Alice. I'm an superadmin."
console.log(admin.hasAccess("database")); // true

// Getters and setters
class Temperature {
  constructor(celsius) {
    this._celsius = celsius;
  }

  get fahrenheit() {
    return this._celsius * 9/5 + 32;
  }

  set fahrenheit(value) {
    this._celsius = (value - 32) * 5/9;
  }
}

let temp = new Temperature(25);
console.log(temp.fahrenheit); // 77
temp.fahrenheit = 86;
console.log(temp._celsius);   // 30
```

## Promises and Async/Await

Handling asynchronous operations

```javascript
// Creating a Promise
function loadData(url) {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      if (url.startsWith("https://")) {
        resolve({data: "Success", url: url});
      } else {
        reject(new Error("Invalid URL"));
      }
    }, 1000);
  });
}

// Using .then/.catch
loadData("https://api.example.com")
  .then(result => {
    console.log(result.data); // "Success"
    return result.url;
  })
  .then(url => {
    console.log(`Loaded from: ${url}`);
  })
  .catch(error => {
    console.error("Error:", error.message);
  });

// Using async/await
async function fetchUserData(userId) {
  try {
    let response = await loadData(`https://api.example.com/users/${userId}`);
    console.log("User data loaded:", response.data);
    return response;
  } catch (error) {
    console.error("Failed to load user:", error.message);
    return null;
  }
}

// Calling async function
fetchUserData(123).then(data => {
  if (data) {
    console.log("Processing:", data);
  }
});

// Promise.all - run multiple promises in parallel
async function loadMultipleUsers(userIds) {
  try {
    let promises = userIds.map(id =>
      loadData(`https://api.example.com/users/${id}`)
    );
    let results = await Promise.all(promises);
    return results;
  } catch (error) {
    console.error("One of the requests failed:", error);
    return [];
  }
}

loadMultipleUsers([1, 2, 3]).then(users => {
  console.log(`Loaded ${users.length} users`);
});
```

## Fetch API

Making HTTP requests to servers

```javascript
// Basic GET request
async function getUsers() {
  try {
    let response = await fetch('https://api.github.com/users');

    if (!response.ok) {
      throw new Error(`HTTP error! status: ${response.status}`);
    }

    let users = await response.json();
    console.log(users);
    return users;
  } catch (error) {
    console.error("Fetch error:", error.message);
    return [];
  }
}

// POST request with JSON data
async function createUser(userData) {
  try {
    let response = await fetch('https://api.example.com/users', {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
        'Authorization': 'Bearer token123'
      },
      body: JSON.stringify(userData)
    });

    if (!response.ok) {
      throw new Error(`HTTP error! status: ${response.status}`);
    }

    let result = await response.json();
    console.log("User created:", result);
    return result;
  } catch (error) {
    console.error("Failed to create user:", error.message);
    return null;
  }
}

// Using the function
createUser({
  name: "John Doe",
  email: "john@example.com",
  age: 30
}).then(user => {
  if (user) {
    console.log("New user ID:", user.id);
  }
});

// Fetch with timeout
async function fetchWithTimeout(url, timeout = 5000) {
  const controller = new AbortController();
  const timeoutId = setTimeout(() => controller.abort(), timeout);

  try {
    let response = await fetch(url, {
      signal: controller.signal
    });
    clearTimeout(timeoutId);
    return await response.json();
  } catch (error) {
    if (error.name === 'AbortError') {
      console.error('Request timed out');
    } else {
      console.error('Fetch failed:', error.message);
    }
    return null;
  }
}
```

## DOM Manipulation

Modifying HTML documents dynamically

```javascript
// Creating elements
let div = document.createElement('div');
div.className = 'alert';
div.innerHTML = '<strong>Hi there!</strong> Important message.';

// Adding to document
document.body.append(div);

// Selecting elements
let button = document.getElementById('myButton');
let items = document.querySelectorAll('.item');
let firstItem = document.querySelector('.item');

// Modifying element properties
button.textContent = 'Click Me';
button.style.backgroundColor = 'blue';
button.style.color = 'white';

// Adding/removing classes
button.classList.add('active');
button.classList.remove('disabled');
button.classList.toggle('selected');

// Setting attributes
button.setAttribute('data-id', '123');
let id = button.getAttribute('data-id');
button.removeAttribute('disabled');

// Creating a complete element
function createUserCard(name, email) {
  let card = document.createElement('div');
  card.className = 'user-card';

  card.innerHTML = `
    <h3>${name}</h3>
    <p>${email}</p>
    <button class="btn-delete">Delete</button>
  `;

  // Add event listener
  let deleteBtn = card.querySelector('.btn-delete');
  deleteBtn.addEventListener('click', () => {
    card.remove();
  });

  return card;
}

// Using the function
let container = document.getElementById('users');
let userCard = createUserCard('John Doe', 'john@example.com');
container.append(userCard);

// Batch manipulation
let items = ['Apple', 'Banana', 'Cherry'];
let list = document.createElement('ul');

items.forEach(item => {
  let li = document.createElement('li');
  li.textContent = item;
  list.append(li);
});

document.body.append(list);
```

## Event Handling

Responding to user interactions

```javascript
// Basic event listener
let button = document.getElementById('myButton');

button.addEventListener('click', function(event) {
  console.log('Button clicked!');
  console.log('Event type:', event.type);
  console.log('Target element:', event.target);
});

// Using arrow function
button.addEventListener('click', (e) => {
  e.target.style.backgroundColor = 'green';
});

// Preventing default behavior
let form = document.getElementById('myForm');

form.addEventListener('submit', function(event) {
  event.preventDefault();

  let formData = new FormData(form);
  let data = Object.fromEntries(formData);

  console.log('Form data:', data);

  // Send data asynchronously
  fetch('/api/submit', {
    method: 'POST',
    headers: {'Content-Type': 'application/json'},
    body: JSON.stringify(data)
  });
});

// Event delegation - handle events on multiple elements
let list = document.getElementById('todoList');

list.addEventListener('click', function(event) {
  if (event.target.tagName === 'BUTTON') {
    let listItem = event.target.closest('li');
    listItem.remove();
    console.log('Item removed');
  }
});

// Keyboard events
let input = document.getElementById('searchBox');

input.addEventListener('keydown', function(event) {
  console.log('Key pressed:', event.key);

  if (event.key === 'Enter') {
    console.log('Search for:', input.value);
  }

  if (event.key === 'Escape') {
    input.value = '';
  }
});

// Mouse events
let box = document.getElementById('box');

box.addEventListener('mouseenter', () => {
  box.style.backgroundColor = 'yellow';
});

box.addEventListener('mouseleave', () => {
  box.style.backgroundColor = 'white';
});

// Removing event listeners
function handleClick() {
  console.log('Clicked!');
}

button.addEventListener('click', handleClick);
button.removeEventListener('click', handleClick);
```

## Local Storage

Storing data in the browser

```javascript
// Saving data
localStorage.setItem('username', 'john_doe');
localStorage.setItem('theme', 'dark');

// Saving objects as JSON
let user = {
  id: 123,
  name: 'John Doe',
  email: 'john@example.com'
};
localStorage.setItem('user', JSON.stringify(user));

// Reading data
let username = localStorage.getItem('username');
console.log(username); // "john_doe"

// Reading and parsing JSON
let storedUser = localStorage.getItem('user');
if (storedUser) {
  let userObject = JSON.parse(storedUser);
  console.log(userObject.name); // "John Doe"
}

// Removing item
localStorage.removeItem('theme');

// Clearing all storage
localStorage.clear();

// Checking if key exists
if (localStorage.getItem('username')) {
  console.log('Username exists');
}

// Complete example: Saving form data
function saveFormData() {
  let formData = {
    name: document.getElementById('name').value,
    email: document.getElementById('email').value,
    preferences: {
      newsletter: document.getElementById('newsletter').checked,
      theme: document.getElementById('theme').value
    },
    timestamp: Date.now()
  };

  try {
    localStorage.setItem('formData', JSON.stringify(formData));
    console.log('Form data saved successfully');
  } catch (error) {
    console.error('Failed to save data:', error);
  }
}

// Loading form data
function loadFormData() {
  try {
    let data = localStorage.getItem('formData');
    if (data) {
      let formData = JSON.parse(data);
      document.getElementById('name').value = formData.name;
      document.getElementById('email').value = formData.email;
      document.getElementById('newsletter').checked = formData.preferences.newsletter;
      document.getElementById('theme').value = formData.preferences.theme;
      console.log('Form data loaded');
    }
  } catch (error) {
    console.error('Failed to load data:', error);
  }
}

// Session storage (similar API, but cleared when tab closes)
sessionStorage.setItem('sessionId', '123456');
let sessionId = sessionStorage.getItem('sessionId');
```

## Regular Expressions

Pattern matching in strings

```javascript
// Creating regular expressions
let regex1 = /pattern/;
let regex2 = new RegExp('pattern', 'gi');

// Basic pattern matching
let str = "Hello, World!";
let hasHello = /Hello/.test(str);
console.log(hasHello); // true

// Finding matches
let text = "The quick brown fox jumps over the lazy dog";
let matches = text.match(/\w+/g);
console.log(matches); // ["The", "quick", "brown", "fox", ...]

// String replacement
let message = "Hello, World!";
let newMessage = message.replace(/World/, "JavaScript");
console.log(newMessage); // "Hello, JavaScript!"

// Email validation
function validateEmail(email) {
  let emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
  return emailRegex.test(email);
}

console.log(validateEmail("test@example.com")); // true
console.log(validateEmail("invalid.email"));     // false

// Phone number formatting
function formatPhone(phone) {
  let cleaned = phone.replace(/\D/g, '');
  let match = cleaned.match(/^(\d{3})(\d{3})(\d{4})$/);
  if (match) {
    return `(${match[1]}) ${match[2]}-${match[3]}`;
  }
  return phone;
}

console.log(formatPhone("1234567890")); // "(123) 456-7890"

// Extracting data with groups
let dateStr = "2024-03-15";
let dateRegex = /(\d{4})-(\d{2})-(\d{2})/;
let dateMatch = dateStr.match(dateRegex);

if (dateMatch) {
  console.log("Year:", dateMatch[1]);   // "2024"
  console.log("Month:", dateMatch[2]);  // "03"
  console.log("Day:", dateMatch[3]);    // "15"
}

// Finding all URLs in text
let content = "Visit https://example.com and http://test.org";
let urlRegex = /https?:\/\/[^\s]+/g;
let urls = content.match(urlRegex);
console.log(urls); // ["https://example.com", "http://test.org"]

// Replace with function
let prices = "Items: $10, $25, $100";
let discounted = prices.replace(/\$(\d+)/g, (match, price) => {
  return '$' + (parseInt(price) * 0.9);
});
console.log(discounted); // "Items: $9, $22.5, $90"
```

## Summary

The Modern JavaScript Tutorial serves as a complete learning resource for JavaScript developers, from beginners to advanced practitioners. It covers essential language features including variables, data types, functions, objects, and classes, as well as modern JavaScript concepts like promises, async/await, modules, and ES6+ syntax. The structured approach with numbered chapters makes it easy to follow a learning path, while the enhanced markdown format with interactive examples provides hands-on practice.

Integration with this tutorial is straightforward for learners and contributors. Content is organized in a hierarchical folder structure where each topic has its own directory containing articles, tasks, and solutions. The tutorial uses standard web technologies and can be served locally using the server available at github.com/javascript-tutorial/server. Contributions are welcomed through pull requests, and translations are supported for multiple languages. The tutorial emphasizes practical examples and real-world use cases, making it an invaluable resource for understanding JavaScript in both browser and modern development environments.
