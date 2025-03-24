# L08-03

## Open a terminal and create a volume

    docker volume create myvol

## List the volumes

    docker volume ls

## Run a Nginx container that will use the volume

    docker run -d --name voltest -v myvol:/app nginx:latest

#### explain commands

    1. docker run
    Chạy một container mới từ một image.

    2. -d
    Chạy container ở chế độ nền (detached mode), nghĩa là nó sẽ chạy trong background thay vì hiển thị output trực tiếp.

    3. --name voltest
    Đặt tên cho container là voltest. Nếu không chỉ định, Docker sẽ tạo một tên ngẫu nhiên.

    4. -v myvol:/app
    myvol là tên của volume (bộ nhớ dữ liệu) mà Docker sẽ sử dụng. Nếu chưa tồn tại, Docker sẽ tự động tạo volume này.

    /app là đường dẫn bên trong container nơi volume sẽ được mount (gắn vào).

    Điều này có nghĩa là bất kỳ dữ liệu nào được lưu trong /app bên trong container sẽ thực sự được lưu vào volume myvol trên hệ thống host. Khi container bị xóa, dữ liệu vẫn tồn tại trong volume.

    5. nginx:latest
    Sử dụng image nginx với tag latest, tức là phiên bản mới nhất của Nginx sẽ được tải về và chạy trong container.

## Connect to the instance

    docker exec -it voltest bash

#### explain commands
    1. docker exec
    Chạy một lệnh trong một container đang chạy.

    2. -it
    -i (interactive): Giữ kết nối tương tác với container, cho phép nhập dữ liệu từ bàn phím.

    -t (tty): Gán một terminal giả lập để có thể làm việc như trong một môi trường shell thông thường.

    3. voltest
    Tên của container mà bạn muốn thực thi lệnh bên trong (ở đây là container voltest).

    4. bash
    Lệnh sẽ chạy bash bên trong container, tức là mở một shell để bạn có thể thao tác.

## Let’s create a file in the volume using Nano

    apt-get update
    apt-get install nano

## Create a file in the app folder
    cd app
    nano test.txt

Type something, save the file and exit Nano using:

    CTRL-O
    CTRL-X

Detach from the instance:

    exit

## Stop and remove the container

    docker stop voltest
    docker rm voltest

## Run it again and see if the file still exists

    docker run -d --name voltest -v myvol:/app nginx:latest
    docker exec -it voltest bash
    cd app
    cat test.txt

## Cleanup

    docker volume rm myvol
    docker stop voltest
    docker rm voltest