Khởi động bài lab thử xem các máy thuộc mạng nào ta thấy được rằng mycomputer nằm cùng mạng với router trong giải địa chỉ 172.24.0.0/24

Còn server sẽ nằm cùng mạng với router trong giải địa chỉ 172.25.0.0/24

Dùng nmap để scan địa chỉ server đã cho với các port từ 2000-3000 để xem các thông tin chi :

```nmap -vv -p 2000-3000 -sC -sV 172.25.0.2```

Trong đó:
  * -vv: scan chi tiết
  * -p: 2000-3000: scan các cổng từ 2000 đến 3000
  * -sC: scan theo scripts
  * -sV: cho biết thông tin version

  ![image](https://github.com/user-attachments/assets/20a79bef-d29a-4fcc-96a0-287cca637ad3)

  Qua đây ta thấy server đang chạy ssh tại port 2844

  Thử kết nối với server qua ssh  thì thấy yêu cầu mật khẩu

  Mình thử dùng tshark để bắt các gói tin trực tiếp ```tshark -i eth1 -T fields -e telnet.data```

  Trong đó:
    * -i eth1: chỉ định interface là eth1
    * -T fields: Đặt định dạng đầu ra khi xem dữ liệu gói được giải mã
    * -e telnet.data: Thêm một trường vào danh sách các trường sẽ hiển thị nếu -T ek|fields|json|pdml được chọn

Sau khi thực hiện lệnh mình nhận được response trả về có chứa password cho login ssh tới server

Mình chỉ cần login vào thôi: ```ssh ubuntu@172.25.0.2 -p 2844```

**Bài này cần thực hiện ít nhất 1 lệnh tcpdump nếu không sẽ không AC được**

```
Source:

https://www.wireshark.org/docs/man-pages/tshark.html

https://www.wireshark.org/docs/dfref/

```
