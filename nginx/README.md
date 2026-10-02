# Custom Error Page 404 voi Nginx

Thu muc nay chua file cau hinh mau cho Bai 2:

- `../src/main/resources/static/404.html`: trang loi tuy chinh, can dat tai `/var/www/my-web/html/404.html` tren server.
- `my-web.conf`: server block Nginx cau hinh `error_page 404 /404.html;` va chan truy cap truc tiep bang `internal`.

## Trien khai tren server

```bash
sudo mkdir -p /var/www/my-web/html
sudo cp src/main/resources/static/404.html /var/www/my-web/html/404.html
sudo cp nginx/my-web.conf /etc/nginx/sites-available/my-web
sudo ln -s /etc/nginx/sites-available/my-web /etc/nginx/sites-enabled/my-web
sudo nginx -t
sudo systemctl reload nginx
```

Neu server da co file symbolic link cung ten trong `sites-enabled`, khong can chay lai lenh `ln -s`.

## Kiem tra

Thay `<IP_ADDRESS_DROPLET>` bang dia chi IP cua server:

```bash
curl -I http://<IP_ADDRESS_DROPLET>/invalid-path-demo
curl http://<IP_ADDRESS_DROPLET>/invalid-path-demo
curl -I http://<IP_ADDRESS_DROPLET>/404.html
```

Ket qua mong doi:

- `/invalid-path-demo` tra ve `404 Not Found` va hien thi noi dung HTML tuy chinh.
- `/404.html` tra ve `404 Not Found` khi truy cap truc tiep, vi file duoc bao ve bang chi thi `internal`.
