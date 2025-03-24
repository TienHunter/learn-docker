# L09-04

## Build the app

    docker compose build

##### explain
Câu lệnh này dùng để build (xây dựng) lại các image Docker được định nghĩa trong tệp docker-compose.yml.

## Run the app

    docker compose up -d

When the app will run, launch the voting app in your browser http://localhost:5000

##### explain 
    1. docker compose

    Sử dụng Docker Compose để quản lý nhiều container cùng lúc thông qua docker-compose.yml.

    (Docker đã đổi từ docker-compose sang docker compose từ phiên bản 2.0 trở đi).

    2. up

    Dùng để khởi động tất cả các service (container) được định nghĩa trong docker-compose.yml.

    Nếu image chưa được build hoặc pull, Docker sẽ tự động build hoặc tải về.

    3. -d (detached mode)

    Chạy các container ở chế độ nền (background).

    Nếu không có -d, Docker sẽ chạy container và hiển thị log trên terminal.


## List the containers

    docker compose ps

## Look at the db container logs

    docker compose logs -f web-fe


## Compose V2 commands

LS will list the current projects

    docker compose ls

## Let's try to deploy a second version

    docker compose up -d

This fails because we can only run an app a single time

## Deploy a second version using a different project name

Let's now use a project name to see if we can deploy a second version

    docker compose -p test up -d

This fails because the localhost port 5000 is already assigned.

Change the ports value from

    - "5000:80"

to

    - "5001:80"

## Deploy again

    docker compose -p test up -d

How many versions do we have running?

    docker compose ls

## Cleanup

    docker compose down
    docker compose ls
    docker compose -p test down
    docker compose ls