---
title: java中socket的用法
date: 2018-05-15 01:58:04
tags: [socket]
---

Java中的Socket的用法

Java中的Socket分为普通的Socket和NioSocket。

普通Socket的用法

Java中的网络通信时通过Socket实现的，Socket分为ServerSocket和Socket两大类，ServerSocket用于服务器端，可以通过accept方法监听请求，监听请求后返回Socket，Socket用于完成具体数据传输，客户端也可以使用Socket发起请求并传输数据。ServerSocket的使用可以分为三步：

创建ServerSocket。ServerSocket的构造方法有5个，其中最方便的是ServerSocket(int port)，只需要一个port就可以了。
调用创建出来的ServerSocket的accept方法进行监听。accept方法是阻塞方法，也就是说调用accept方法后程序会停下来等待连接请求，在接受请求之前程序将不会继续执行，当接收到请求后accept方法返回一个Socket。

使用accept方法返回的Socket与客户端进行通信
　　

如下代码，我们在服务器端创建ServerSocket，并调用accept方法监听Client的请求，收到请求后返回一个Socket。

public class Server {

    public static void main(String[] args) {
        // TODO Auto-generated method stub
        try {
            //创建一个ServerSocket监听8080端口
            ServerSocket server = new ServerSocket(8080);
            //等待请求
            Socket socket = server.accept();
            //接受请求后使用Socket进行通信，创建BufferedReader用于读取数据
            BufferedReader is = new BufferedReader(new InputStreamReader(socket.getInputStream()));
            String line = is.readLine();
            System.out.println("received frome client:" + line);
            //创建PrintWriter，用于发送数据
            PrintWriter pw = new PrintWriter(socket.getOutputStream());
            pw.println("this data is from server");
            pw.flush();
            //关闭资源
            pw.close();
            is.close();
            socket.close();
            server.close();
        } catch (IOException e) {
            // TODO Auto-generated catch block
            e.printStackTrace();
        }
    }

	}

然后我们再看看客户端的Socket代码，Socket的使用也是一样，首先创建一个Socket，Socket的构造方法非常多，这里用的是Socket(String host, int port)，把目标主机的地址和端口号传入即可（本实验代码中服务器和Client代码没有在同一台机器上，服务器的IP地址：192.168.6.42，所以如果读者在实验过程中ServerSocket和Client在同一主机下，那么Client中的IP地址需要更改为：127.0.0.1，Socket创建的过程就会跟服务器端建立连接，创建完Socket后，再创建Writer和Reader来传输数据，数据传输完成后释放资源关闭连接。


public class Client {

    public static void main(String[] args) {
        // TODO Auto-generated method stub
        String msg = "Client data";
        
        try {
            //创建一个Socket，跟服务器的8080端口链接
            Socket socket = new Socket("192.168.6.42",8080);
            //使用PrintWriter和BufferedReader进行读写数据
            PrintWriter pw = new PrintWriter(socket.getOutputStream());
            BufferedReader is = new BufferedReader(new InputStreamReader(socket.getInputStream()));
            //发送数据
            pw.println(msg);
            pw.flush();
            //接收数据
            String line = is.readLine();
            System.out.println("received from server" + line);
            //关闭资源
            pw.close();
            is.close();
            socket.close();
        } catch (UnknownHostException e) {
            // TODO Auto-generated catch block
            e.printStackTrace();
        } catch (IOException e) {
            // TODO Auto-generated catch block
            e.printStackTrace();
        }
    }

	}


最后先启动Server然后启动Client就可以完成一次Client和Server的通信。


NioSocket的用法

　　从JDK1.4开始，Java增加了新的IO模式-nio（new IO），nio在底层采用了新的处理方式，极大提高了IO的效率。我们使用的Socket也是IO的一种，nio提供了相应的工具：ServerSocketChannel和SocketChannel，他们分别对应原来的ServerSocket和Socket。

　　在了解NioSocket之前我们先了解Buffer、Channel、Selector。为了方便理解，我们来看个例子，要过圣诞节了，需要给同学们发贺卡和苹果，班长这时候又是最辛苦的，每次拿一个苹果和一张贺卡发给一个同学，发送完成后回来再取一张贺卡和一个苹果发给另一个同学，直到全班同学都拿到贺卡和苹果为止，这就是普通Socket处理方式，来一个请求，ServerSocket就进行处理，处理完成后继续接受请求，这种方式效率很低啊！还是圣诞节的例子，班长发现班委不止他一个，就通知了生活委员（女）和组织委员（男）来帮助他发贺卡和苹果，女生的贺卡是粉色的，男生的贺卡是蓝色的，生活委员负责从全班的贺卡中挑选女生的贺卡，而组织委员则负责男生的贺卡，然后生活委员和组织委员分别以宿舍为单位通知宿舍长来领取宿舍同学的贺卡和苹果，班长将圣诞节发苹果和贺卡的工作布置给两个班委后，就可以继续干其他工作了。这就是NioSocket，Buffer就是所有传递的货物，也就是例子中的苹果和贺卡，而Channel就是传递货物的通道，也就是例子中的宿舍长，负责将礼物搬回自己宿舍，而生活委员和组织委员充当了Selector的职责，负责礼物的分拣。

　　ServerSocketChannel可以使用自己的静态工厂方法open创建，每个ServerSocketChannel对应一个ServerSocket（通过调用其socket()获取），如果直接使用获取的ServerSocket来监听请求，那么还是普通ServerSocket，而通过将获取的ServerSocket绑定端口号来实现NioSocket。ServerSocketChannel可以通过configureBlocking方法来设置是否采用阻塞模式，如果设置为非阻塞模式，就可以调用register方法注册Selector来使用了。

　　Selector可以通过其静态工厂方法open创建，创建后通过Channel的register方法注册到ServerSocketChannel或者SocketChannel上，注册完成后Selector就可以通过select方法来等待请求，select方法有一个long类型参数，代表最长等待时间，如果在这段时间内收到相应操作的请求则返回可以处理的请求的数量，否则在超时后返回0，如果传入的参数为0或者无参数的重载方法，select方法会采用阻塞模式知道有相应操作请求的出现。当接收到请求后Selector调用selectdKeys方法返回SelectionKey集合。

　　SelectionKey保存了处理当前请求的Channel和Selector，并且提供了不同的操作类型。Channel在注册Selector时可以通过register的第二个参数选择特定的操作（请求操作、连接操作、读操作、写操作），只有在register中注册了相应的操作Selector才会关心相应类型操作的请求。

　　我们来看看服务器端NioSocket的处理过程：

创建ServerSocketChannel并设置相应的端口号、是否为阻塞模式
创建Selector并注册到ServerSocketChannel上
调用Selector的selector方法等待请求
Selector接收到请求后使用selectdKeys返回SelectionKey集合
使用SelectionKey获取到channel、selector和操作类型并进行具体操作。


	public class NIOServer {

    public static void main(String[] args) {
        // TODO Auto-generated method stub
        try {
            //创建ServerSocketChannel，监听8080端口
            ServerSocketChannel ssc = ServerSocketChannel.open();
            ssc.socket().bind(new InetSocketAddress(8080));
            //设置为非阻塞模式
            ssc.configureBlocking(false);
            //为ssc注册选择器
            Selector selector = Selector.open();
            ssc.register(selector, SelectionKey.OP_ACCEPT);
            //创建处理器
            Handler handler = new Handler(1024);
            while(true){
                //等待请求，每次等待阻塞3s，超过3s后线程继续向下运行，如果传入0或者不传入参数则一直阻塞
                if(selector.select(3000) == 0){
                    System.out.println("等待请求超时----");
                    continue;
                }
                System.out.println("处理请求----");
                //获取处理的SelectionKey
                Iterator<SelectionKey> keyIter = selector.selectedKeys().iterator();
                while(keyIter.hasNext()){
                    SelectionKey key = keyIter.next();
                    try{
                        //接收到连接请求时
                        if(key.isAcceptable()){
                            handler.handleAccept(key);
                        }
                        //读数据
                        if(key.isReadable()){
                            handler.handleRead(key);
                        }
                    }catch(IOException ex){
                        keyIter.remove();
                        continue;
                    }
                    //处理完后，从待处理的SelectionKey迭代器中移除当前所使用的key
                    keyIter.remove();
                }
            }
        } catch (IOException e) {
            // TODO Auto-generated catch block
            e.printStackTrace();
        }
    }
    private static class Handler{
        private int bufferSize = 1024;
        private String localCharset = "UTF-8";
        public Handler(int bufferSize){
            this.bufferSize = bufferSize;
        }
        public void handleAccept(SelectionKey key) throws IOException{
            SocketChannel sc = ((ServerSocketChannel) key.channel()).accept();
            sc.configureBlocking(false);
            sc.register(key.selector(), SelectionKey.OP_READ, ByteBuffer.allocate(bufferSize));
        }
        public void handleRead(SelectionKey key) throws IOException{
            //获取Channel
            SocketChannel sc = (SocketChannel) key.channel();
            //获取buffer并重置
            ByteBuffer buffer = (ByteBuffer)key.attachment();
            buffer.clear();
            //没有读到内容则关闭
            if(sc.read(buffer) == -1)
                sc.close();
            else{
                //将buffer转换为读状态
                buffer.flip();
                //将buffer中接收到的值按localCharset格式编码后保存到receivedString
                String receivedString = Charset.forName(localCharset).newDecoder().decode(buffer).toString();
                System.out.println("received from client:" + receivedString);
                //返回数据给客户端
                String sendString = "this data is from Server";
                buffer = ByteBuffer.wrap(sendString.getBytes(localCharset));
                sc.write(buffer);
                sc.close();
            }
        }
    }
	}

　客户端代码通普通Socket一样，Socket socket = new Socket("127.0.0.1",8080);表示与服务器端建立连接，从而执行服务器端的handleAccept()方法，给ServerSocketChannel注册selector以及添加SelectionKey.OP_READ参数，表示selector关心读方法。然后通过PrintWrite在客户端将内容发送给服务器端，服务器端执行handleRead方法对接收到的内容进行处理，并将结果返回给客户端，客户端通过BufferedReader接受数据