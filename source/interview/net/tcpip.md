#### TCPIP
- socket  ip port
- 拆包粘包
  - 粘包，数据小，两个信息组合到一起发送，接收方收到后无法区分两个信息的分隔点
  - 拆包，数据大，一次只能发送一个信息的一部分，后半部分粘到了下一条信息
- 滑动窗口
  - 字节为窗口最小单位
  -
  - 流量控制
    - rwnd  receiver window

- 连接-三次-四次
  - 三次
    - syn,seq,ack
  - 四次

  - why
    - 三次
      - 两次会出现的问题,发给服务端的连接请求阻塞了，客服端超时重新发了连接，然后完成连接，这个时候第一次的连接服务器收到了，服务器认为要新建连接，然后确认了，但是这个连接是废弃的了，客服端不会处理，所以这个资源就被无辜占用了
      - 三次为何能解决这个问题，
    - 四次
      - timewait - 2msl


- wireshark
  - 3
  ```
  TCP	78	60111 → 80 [SYN] Seq=0 Win=65535 Len=0 MSS=1460 WS=32 TSval=808690082 TSecr=0 SACK_PERM=1
  TCP	54	60111 → 80 [ACK] Seq=1 Ack=1 Win=262144 Len=0
  TCP	1434	60111 → 80 [ACK] Seq=1 Ack=1 Win=262144 Len=1380 [TCP segment of a reassembled PDU]
  HTTP	75	GET /tankxiao HTTP/1.1
  ```
  - 4
  ```
	103.254.190.5	100.81.168.130	TCP	60	80 → 52770 [FIN, ACK] Seq=20861 Ack=329 Win=115200 Len=0
  100.81.168.130	103.254.190.5	TCP	54	52770 → 80 [ACK] Seq=329 Ack=20862 Win=262144 Len=0
  100.81.168.130	103.254.190.5	TCP	54	52770 → 80 [FIN, ACK] Seq=329 Ack=20862 Win=262144 Len=0
  103.254.190.5	100.81.168.130	TCP	60	80 → 52770 [ACK] Seq=20862 Ack=330 Win=115200 Len=0
  ```
