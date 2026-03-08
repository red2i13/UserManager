# Express Validation Learning App

A simple Express application to learn **express-validator** - a library for validating request input data.

## Project Structure

```
├── app.js                    # Main Express application entry point
├── controllers/
│   └── homeController.js     # Controller with request handlers
├── routes/
│   └── homeRoutes.js         # Route definitions with validation rules
└── package.json              # Project dependencies
```

## Setup

1. Install dependencies:
   ```bash
   npm install
   ```

2. Start the server:
   ```bash
   npm start
   ```
   For development with auto-reload:
   ```bash
   npm run dev
   ```

3. Server runs on `http://localhost:3000`

## API Endpoints

### 1. GET `/` (Home Route)
Returns a simple welcome message.

**Example:**
```bash
curl http://localhost:3000/
```

**Response:**
```json
{
  "message": "Welcome to the Home Page!",
  "timestamp": "2026-03-07T..."
}
```

### 2. POST `/submit` (Form Submission with Validation)
Accepts form data and validates:
- **name**: Required, minimum 2 characters
- **email**: Required, valid email format
- **age**: Required, integer between 1-120

**Example:**
```bash
curl -X POST http://localhost:3000/submit \
  -H "Content-Type: application/json" \
  -d '{"name": "John Doe", "email": "john@example.com", "age": 30}'
```

**Valid Response:**
```json
{
  "success": true,
  "message": "Form submitted successfully!",
  "data": {
    "name": "John Doe",
    "email": "john@example.com",
    "age": 30
  }
}
```

**Invalid Response (missing name):**
```json
{
  "success": false,
  "errors": [
    {
      "type": "field",
      "value": "",
      "msg": "Name is required",
      "path": "name",
      "location": "body"
    }
  ]
}
```

## Express-Validator Key Concepts

### 1. **Validation Rules** (in routes)
```javascript
body('fieldName')
  .notEmpty().withMessage('Message if empty')
  .isInt().withMessage('Message if not int')
```

### 2. **sanitization**
```javascript
body('name').trim()  // Remove whitespace
```

### 3. **Check Results**
```javascript
const errors = validationResult(req);
if (!errors.isEmpty()) {
  // Handle validation errors
}
```

### 4. **Middleware Chain**
- **Validation Rules**: Applied to request data
- **Error Checking Middleware**: Stops execution if errors found
- **Controller Handler**: Only executes if validation passes

## Common Validation Methods

| Method | Purpose |
|--------|---------|
| `.notEmpty()` | Field must have a value |
| `.isEmail()` | Must be valid email format |
| `.isInt()` | Must be an integer |
| `.isLength()` | Check string length |
| `.trim()` | Remove whitespace |
| `.escape()` | Escape special characters |
| `.custom()` | Custom validation logic |

## Learning Path

1. **Understand the flow**: Request → Validation → Error Check → Controller
2. **Modify validation rules**: Try adding more complex validations
3. **Add custom validators**: Use `.custom()` for unique business logic
4. **Combine multiple rules**: Chain validators for comprehensive checks

## Testing

Use your preferred tool to test:
- **cURL** (command line)
- **Postman** (GUI)
- **REST Client** (VS Code extension)
- **Thunder Client** (VS Code extension)
