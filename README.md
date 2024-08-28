## Q-1. Make model to store data ( Make Schemas ) Insert Record into MongoDB


1. **Define a Schema**:
   - In MongoDB, schemas are typically defined using a library like Mongoose if you’re using Node.js. A schema is a blueprint for the structure of your data, specifying fields, their types, and any constraints.
   - For example, if you’re creating a schema for a `User` collection, you might define fields like `name`, `email`, and `age`, along with their data types and validation rules.

2. **Create a Model**:
   - Once you’ve defined a schema, you create a model based on that schema. A model is a constructor function that you use to interact with the MongoDB collection corresponding to the schema.
   - The model provides methods for CRUD (Create, Read, Update, Delete) operations.

3. **Insert Records**:
   - To insert records, you create an instance of the model with the data you want to store and then call the `save` method on that instance.
   - Alternatively, you can use methods like `insertMany` to add multiple records at once.


## Q-2. Fetch record from mongoDB Delete Record from MongoDB


Fetching and deleting records in MongoDB involves using various methods provided by MongoDB drivers or libraries. Here’s a brief explanation of each operation:

### Fetch Record from MongoDB

1. **Choose a Query Method**:
   - **Find One**: Use the `findOne` method to fetch a single document that matches a query.
   - **Find Many**: Use the `find` method to fetch multiple documents that match a query.

2. **Specify Query Criteria**:
   - Provide criteria to filter the records. For example, you might query by a specific field like `name` or `email`.

3. **Execute the Query**:
   - The method will return the document(s) that match the criteria. If you’re using an ORM like Mongoose, this typically returns a promise or a callback with the result.

### Delete Record from MongoDB

1. **Choose a Deletion Method**:
   - **Delete One**: Use the `deleteOne` method to delete a single document that matches the criteria.
   - **Delete Many**: Use the `deleteMany` method to delete multiple documents that match the criteria.

2. **Specify Deletion Criteria**:
   - Provide criteria to identify which document(s) to delete. This might be a specific field or a condition that matches multiple documents.

3. **Execute the Deletion**:
   - The method will remove the document(s) from the collection. Like with fetching, this operation typically returns a promise or a callback indicating the result of the deletion.

### Summary

- **Fetching Records**: Use `findOne` for a single document or `find` for multiple documents, providing query criteria.
- **Deleting Records**: Use `deleteOne` for a single document or `deleteMany` for multiple documents, specifying deletion criteria.


## Q-3.UPDATE OR MODIFY OR CHANGE RECORD IN MONGODB


Updating or modifying records in MongoDB involves using specific methods to alter existing documents in a collection. Here’s a brief overview of how you can perform these operations:

### Update or Modify Records in MongoDB

1. **Choose an Update Method**:
   - **Update One**: Use the `updateOne` method to update a single document that matches the specified criteria.
   - **Update Many**: Use the `updateMany` method to update multiple documents that match the criteria.

2. **Specify Update Criteria**:
   - Define a query to locate the document(s) you want to update. This is similar to the query used for fetching records.

3. **Specify Update Operations**:
   - Use update operators to define how the document(s) should be modified. Common update operators include:
     - `$set`: Updates the value of a field.
     - `$inc`: Increments the value of a field.
     - `$push`: Adds an item to an array.
     - `$pull`: Removes an item from an array.

4. **Execute the Update**:
   - Call the appropriate update method with the query criteria and update operations. This will apply the changes to the matched document(s).

### Example Workflow

- **Update One Document**:
  1. **Define Criteria**: `{ _id: 123 }` (Find the document with a specific `_id`).
  2. **Define Update**: `{ $set: { status: "active" } }` (Set the `status` field to "active").
  3. **Execute**: Call `updateOne` with the criteria and update.

- **Update Many Documents**:
  1. **Define Criteria**: `{ age: { $lt: 30 } }` (Find documents where age is less than 30).
  2. **Define Update**: `{ $inc: { age: 1 } }` (Increment the `age` field by 1).
  3. **Execute**: Call `updateMany` with the criteria and update.

### Summary

- **Update One Document**: Use `updateOne` with a query and an update operation to modify a single document.
- **Update Many Documents**: Use `updateMany` with a query and update operations to modify multiple documents that match the criteria.


## Q-4. Node.js App Types of Requests (GET, POST, PUT, DELETE) CRUD operation with API

In a Node.js application, you often work with RESTful APIs to perform CRUD (Create, Read, Update, Delete) operations. Here's a brief overview of the different types of HTTP requests used for these operations:

1. **GET**:
   - **Purpose**: Retrieve data from the server.
   - **Usage**: Fetch information from a database or resource. For example, `GET /users` might retrieve a list of users.
   - **Characteristics**: Does not modify data. It is safe and idempotent (calling it multiple times has the same effect as calling it once).

2. **POST**:
   - **Purpose**: Submit data to the server to create a new resource.
   - **Usage**: Send data to the server, such as creating a new user with `POST /users`.
   - **Characteristics**: Modifies data. It is not idempotent (calling it multiple times may create multiple resources).

3. **PUT**:
   - **Purpose**: Update an existing resource or create a resource if it does not exist.
   - **Usage**: Replace the entire resource with the provided data. For example, `PUT /users/1` might update user data with ID 1.
   - **Characteristics**: Modifies data. It is idempotent (calling it multiple times will have the same result as calling it once).

4. **DELETE**:
   - **Purpose**: Remove a resource from the server.
   - **Usage**: Delete a resource such as a user with `DELETE /users/1`.
   - **Characteristics**: Modifies data. It is idempotent (calling it multiple times will have the same result as calling it once).

**Example with Express.js**:

```javascript
const express = require('express');
const app = express();
app.use(express.json());

let users = []; // Example in-memory data store

// GET /users
app.get('/users', (req, res) => {
  res.json(users);
});

// POST /users
app.post('/users', (req, res) => {
  const user = req.body;
  users.push(user);
  res.status(201).json(user);
});

// PUT /users/:id
app.put('/users/:id', (req, res) => {
  const userId = parseInt(req.params.id, 10);
  const updatedUser = req.body;
  users = users.map(user => user.id === userId ? updatedUser : user);
  res.json(updatedUser);
});

// DELETE /users/:id
app.delete('/users/:id', (req, res) => {
  const userId = parseInt(req.params.id, 10);
  users = users.filter(user => user.id !== userId);
  res.status(204).end();
});

app.listen(3000, () => {
  console.log('Server is running on port 3000');
});
```

This code snippet illustrates how each request type is handled in an Express.js application.

