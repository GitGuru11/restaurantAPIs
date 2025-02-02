# Restaurant API

## Description

The REST API is used to update the food menu of a Restaurant and the Chefs profile on the webpage. You can access the API and also perform normal CRUD operations via the endpoints (`/menu/` and `/chef/`).

The data from the API is displayed on the webpage after refreshing the webpage. Loading or refreshing the webpage automatically sends a **GET** request to the endpoint to retrieve the data.

## Requirement

- Install the lastest Golang (required if using first setup)
- Install Docker (required if using second setup)
- HTTP Client for interacting with the API: Postman, Curl, Thunder Client, Web Browser or any client of your choice

## Setup

There are 2 ways to run this project: `cloning the project` and `docker build`

### Cloning the Project

- Clone the project
- From the command line, start the web server by running `go run main.go`
- On your browser or HTTP client, enter `http://localhost:3000` to **load the web page**. The default port is **_3000_**
  - to change the port or address, for example to **_7000_**, on the commad line, run `go run main.go --listenaddr :7000`
  - on your browser or HTTP client like Postman, enter `http://localhost:7000`
- Make an HTTP **POST** request (see Endpoint section) using an HTTP client, then refresh the webpage to see the data displayed on the webpage. **_Please click the button below to send HTTP requests using my Postman collection. Make sure to re-initialize the port to the port number you will use_**

  [![Run in Postman](https://run.pstmn.io/button.svg)](https://app.getpostman.com/run-collection/25499133-d07cee34-4e11-4ae7-ad33-643cd9a6e3b5?action=collection%2Ffork&source=rip_markdown&collection-url=entityId%3D25499133-d07cee34-4e11-4ae7-ad33-643cd9a6e3b5%26entityType%3Dcollection%26workspaceId%3D6089f5e4-d1b8-4a4c-ba19-c5bec8f7facc)

### Docker Build

- Pull the image: `docker pull christochi/restaurantapi:v1`
- Run `docker images` to get the **_image-id_**
- Run `docker container run -p 3000:3000 <image-id>` to create the container and publish the **_hostPort:containerPort_**
- On the web browser, type `http://localhost:3000`
- Make an HTTP **POST** request (see Endpoint section) using any HTTP client of your choice, then refresh the webpage to see the data displayed on the webpage. **_Please click the button above to send HTTP requests using my Postman collection. Make sure to re-initialize the port to 3000_**

## Endpoints

### Menu

- **Add a Food Menu**: POST `http://localhost:3000/menu/`

```
Example of JSON body to send as part of the POST request

[
    {
        "type" : "Breakfast",
        "meal" : "Potato with Bacon",
        "price" : "$5",
        "desc": "mildly fried potatoes with bacon",
        "image": "potato"
    },

    {
        "type" : "Lunch",
        "meal" : "Chicken Fried Rice",
        "price" : "$15",
        "desc": "Rice with stirred fried vege with baked chicken",
        "image": "chicken-fried-rice"
    }
]
```

If adding a new meal, please put the meal's images in **_/static/img/portfolio/_** path, and include the **_type, meal, price, desc and image_** fields with values to be sent as a request. The value of the **_image_** field must be the name of the image without the extension just like in the json above.

Resize the image and maintain aspect ratio by creating 2 copies. One copy of dimension **_890 x 593_** and name it **_image-name-large (chicken-fried-rice-large)_**, and the other of dimension **_500 x 333_** also named as **_chicken-fried-rice-small_**.

- **Returns list of Food Menu**: GET `http://localhost:3000/menu/`. **GET** request retrieves the data in JSON format via the endpoint
- **Returns list of a meal type in the food menu**: There are 4 acceptable meal types: **_Breakfast, Lunch, Dinner & Drinks_**
  GET `http://localhost:3000/menu/drinks` or GET `http://localhost:3000/menu/lunch`
- **Returns Meals that match a search pattern**: GET `http://localhost:3000/menu/breakfast/hotdog` or `http://localhost:3000/menu/dinner/rice`
- **Deletes all Menu**: DELETE `http://localhost:3000/menu/`
- **Deletes a Meal that matches a search pattern**: DELETE `http://localhost:3000/menu/drinks/mangolasse`

### Chef

- **Add a Chef**: POST `http://localhost:3000/chef/`

```
Example of JSON body to send as part of the POST request

[
    {
        "name": "John Doe",
        "about": "John has 10 years experience making delicious meals for 5-star hotels and famous restaurants in North America",
        "image": "johndoe.jpg"
    },

    {
        "name": "Chocho Okoye",
        "about": "Chocho has 20 years experience cooking for famous restaurants in African and the Caribbean",
        "image": "chocho.jpg"
    }
]
```

If adding a new chef profile, please put the chef's image in **_/static/img/team/_** path, and include the **_name, about and image_** fields with values to be sent as a request. The value of the **_image_** field must be the name of the image (including the extension) just like in the json above.
