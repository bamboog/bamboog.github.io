##### Nio

- 异步，同步，阻塞，非阻塞
  - 同步就是指调用者主动等待调用结果
  - 阻塞和非阻塞关注的是程序在等待调用结果(消息，返回值)时的状态．
  阻塞调用是指在调用结果返回之前，当前线程会被挂起，调用线程只有在得到结果之后才会继续执行

- file io
  - 字节字符流--block
  - FileChannel
  - chanel-buffer
  - mmap
  - directio

- 网络 io
  - SocketChannelImpl -- checkConnect --
    - unix --- poll
    - win  --- select

- buffer
  - MappedByteBuffer
  - DirectByteBuffer extends MappedByteBuffer
  - ByteBuffer


- Reactor
  -
  - netty Reactor
  -
