# Get Slices from DB Images API

This FastAPI application allows users to interact with image data stored in a database. The API provides endpoints to upload image data, retrieve a list of available images, and get slices of images based on specified depth parameters.

## Table of Contents

- [Installation](#installation)
- [Usage](#usage)
- [API Endpoints](#api-endpoints)
  - [GET `/`](#get-)
  - [GET `/api/available_images`](#get-apiavailable_images)
  - [POST `/api/get_slice`](#post-apigetslice)
  - [POST `/api/upload_image`](#post-apiupload_image)

## Installation

1. **Clone the repository**:
    ```sh
    git clone https://github.com/aesedeu/iloveai.git
    cd yourrepository
    ```
2. **Start the application**
    ```sh
    docker-compose up -d
    ```

    Two containers will be created (api-container + postgres-container)

## Usage

Once the application is running, you can interact with the API using tools like `curl`, `httpie`, or Postman. Below are the details of the available endpoints.

## API Endpoints

### GET `/`

Returns basic information about the API.

- **Response**:
    ```json
    {
        "Api_Name": "Get slices"
    }
    ```

### GET `/api/available_images`

Retrieves a list of available images in the database.

- **Response**:
    ```json
    {
        "list_available_images": [
            "example_image_5460_150",
            "some_new_image_42_42"
        ]
    }
    ```

### POST `/api/get_slice`

Retrieves a slice of the specified image from the database based on depth parameters.

- **Request Body**:
    ```json
    {
        "min_depth": 9100.2,
        "max_depth": 9130.5,
        "image_name":"example_image_5460_150"
    }
    ```

- **Response**:
    - On success: Returns the image slice as a PNG file.
    - On error: Returns an error message.
    ```json
    {
        "Error": "Requested image 'example_image_5460_150' not found. Please check available images using '/api/available_images'"
    }
    ```


# Additional info for the reviwer(s)
This solutions is mostly like MVP and of course there necessary to make much more before the real deployment.

The great feature would be to add an opportunity to upload files to db. I added functionality to get list of available "images" in db.

1. autopep8 and pylint were used to check code quality
2. Minimal tests I wrote just to check api endpoints. In real practice write pytests for DB must be required. Also some load tests would be nice to add.
3. In the task nothing were said regarding CI/CD pipelines so it's haven't been done
4. Docstrings written not very detailed. Just for example (but I write them everytime detailed as much as possible)
5. I had a great desire to add WEB-Interface something like Gradio or Streamlit. But of course it will take some more time
6. I also didn't use multistage build in this project to reduce image size
7. To increase response speed it's better to use cache service like Redis and temporary store images in it instead of making new requests to DB every time
8. In `sandbox.ipynb` you may find some raw code I wrote while I was doing this task
9. I didn't hide any environmental variables and passwords for postgres. In real projects of course this is a very private and secure information
10. The best practice would be to add proxy load balancer like Nginx especially If we have multiple containers with different purposes. Also SSL certificates didn't aply for HTTPS connection.

If my task matches your expectations I'm ready to discuss each line of code which I wrote here.

**<center>Thanks for your time! :)**
