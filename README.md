# GrubDash
This project creates the routes and handlers for the GrubDash application using Express.js

## Routes
### GET /dishes
Responds with a list of all dishes, with the following as a sample response:

{
  "data": [
    {
      "id": "d351db2b49b69679504652ea1cf38241",
      "name": "Dolcelatte and chickpea spaghetti",
      "description": "Spaghetti topped with a blend of dolcelatte and fresh chickpeas",
      "price": 19,
      "image_url": "https://images.pexels.com/photos/1279330/pexels-photo-1279330.jpeg?h=530&w=350"
    }
  ]
}

### POST /dishes
Creates a new dish and validates that all fields (except id which will be assigned at creation) are present and viable. If any failures in validation occur, a status of 400 is returned. When the POST is complete, it returns a response of 201.

### GET /dishes/:dishId
Reads a dish with a specified id, or returns 404 if the id is invalid. Returns a status of 200 if successful.

### PUT /dishes/:dishId
Updates a dish with the specified fields, validating that all fields (except id) are present and viable. If the :dishId doesn't exist, it returns a 404 error. An id does not need to be provided in the fields for update, but if it is, it must match the :dishId.

### GET /orders
Returns a list of all orders and a status of 200. Sample below:

{
  "data": [
    {
      "id": "5a887d326e83d3c5bdcbee398ea32aff",
      "deliverTo": "308 Negra Arroyo Lane, Albuquerque, NM",
      "mobileNumber": "(505) 143-3369",
      "status": "delivered",
      "dishes": [
        {
          "id": "d351db2b49b69679504652ea1cf38241",
          "name": "Dolcelatte and chickpea spaghetti",
          "description": "Spaghetti topped with a blend of dolcelatte and fresh chickpeas",
          "image_url": "https://images.pexels.com/photos/1279330/pexels-photo-1279330.jpeg?h=530&w=350",
          "price": 19,
          "quantity": 2
        }
      ]
    }
  ]
}

### POST /orders
Creates a new order and validates that all fields (except id which will be assigned at creation) are present and viable. Each dish in dishes refers to the complete dish rather than just the dishId. If any failures in validation occur, a status of 400 is returned. If successful, the status returns 201.

### GET /orders/:orderId
Reads an order with a specified id, or returns 404 if the id is invalid. Returns a status of 200 if successful.

### PUT /orders/:orderId
Updates an order with the specified fields, validating that all fields (except id) are present and viable. Status in particular must not be missing, empty, or "delivered" for the order to be updated. 

If the :orderId doesn't exist, it returns a 404 error. An id does not need to be provided in the fields for update, but if it is, it must match the :orderId.

### DELETE /orders/:orderId
Deletes an order with the specified :orderId, or returns a 404 error if it is not found. The order cannot be deleted if status is "pending". When successfully completed, it returns a 204 status. 

### All Other Routes
All CRUD routes not described above return a status of 405 with a "Method not allowed" error message. Any other routes return a status of 404 with a "Path not found" error message.

