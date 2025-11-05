# Step 1: Introduction to Node.js

Welcome to your first step! In this module, you'll learn the fundamentals of Node.js.

## Learning Objectives

By the end of this step, you will:

- Understand what Node.js is and how it works
- Learn about Node.js modules (CommonJS)
- Work with the File System (fs) module
- Use the Path module
- Create and organize your own modules

##  What is Node.js?

Node.js is a JavaScript runtime built on Chrome's V8 JavaScript engine. It allows you to run JavaScript on the server side, outside of the browser.

## Exercises

### Exercise 1: Understanding Modules

In Node.js, we use modules to organize code. Let's start by creating a simple module.

**Task:** Create a file called `greetings.js` that exports a function to greet users.

**Instructions:**

1. Create a file `greetings.js`
2. Export a function that takes a name and returns a greeting message
3. Create a file `app.js` that imports and uses this function

**Hint:** Use `module.exports` to export and `require()` to import.

### Exercise 2: Working with File System

The `fs` module allows you to interact with the file system.

**Task:** Create a program that reads a file and displays its contents.

**Instructions:**

1. Create a text file `data.txt` with some content
2. Create `readFile.js` that reads and displays the file content
3. Handle errors appropriately

**Hint:** Use `fs.readFile()` or `fs.readFileSync()`.

### Exercise 3: Working with Paths

The `path` module helps you work with file and directory paths.

**Task:** Create a program that joins paths and gets file information.

**Instructions:**

1. Create `pathDemo.js`
2. Use `path.join()` to create file paths
3. Use `path.basename()` and `path.extname()` to get file information

### Exercise 4: Creating a File Manager Module

**Task:** Create a reusable module for file operations.

**Instructions:**

1. Create `fileManager.js` with functions to:
   - Read a file
   - Write to a file
   - Check if a file exists
2. Export these functions
3. Create `testFileManager.js` to test your module

## Hints and Tips

### For Exercise 1: Understanding Modules
- Use `module.exports` to export your function from `greetings.js`
- Use `require('./greetings')` to import it in `app.js`
- The function should take a `name` parameter and return a string
- Remember: `module.exports` can export functions, objects, or any value

### For Exercise 2: Working with File System
- Use `const fs = require('fs')` to import the file system module
- `fs.readFile()` takes three parameters: file path, encoding ('utf8'), and a callback function
- The callback receives `(err, data)` - always check for errors first!
- Use `path.join(__dirname, 'data.txt')` to create a proper file path

### For Exercise 3: Working with Paths
- Import path module: `const path = require('path')`
- `path.join()` combines path segments safely
- `path.basename()` extracts the filename from a full path
- `path.extname()` gets the file extension (e.g., '.txt')

### For Exercise 4: Creating a File Manager Module
- Create functions that return Promises for async operations
- Use `fs.existsSync()` to check if a file exists (synchronous)
- Wrap `fs.readFile()` and `fs.writeFile()` in Promises
- Export an object containing all your functions: `module.exports = { readFile, writeFile, fileExists }`

## Testing Your Code

1. Run your Node.js files using:

   ```bash
   node app.js
   ```

2. Make sure you're in the correct directory:
   ```bash
   cd step-01-intro-nodejs
   ```

## Checklist

Before moving to Step 2, make sure you can:

- [ ] Create and export modules
- [ ] Import and use modules with `require()`
- [ ] Read and write files using `fs` module
- [ ] Use `path` module to work with file paths
- [ ] Understand the difference between synchronous and asynchronous operations

## Key Concepts

### CommonJS Modules

- `module.exports` - Export a module
- `require()` - Import a module

### File System Module

- `fs.readFile()` - Asynchronous file reading
- `fs.readFileSync()` - Synchronous file reading
- `fs.writeFile()` - Write to a file

### Path Module

- `path.join()` - Join path segments
- `path.basename()` - Get filename from path
- `path.extname()` - Get file extension

## Next Steps

Once you've completed all exercises and understand the concepts, you're ready for:
**[Step 2: Building HTTP Server](../step-02-http-server/README.md)**

## Common Issues

**Issue:** `Cannot find module` error

- **Solution:** Make sure your file paths are correct and you're using `./` for relative paths

**Issue:** File not found

- **Solution:** Check that you're running the command from the correct directory

**Issue:** Permission denied

- **Solution:** Make sure you have read/write permissions in the directory

---

**Ready to code?** Start with Exercise 1!
