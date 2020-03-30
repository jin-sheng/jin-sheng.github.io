# 输入/输出流体系

|分类|字节输入流|字节输出流|字符输入流|字符输出流|
|---|---|---|---|---|
|抽象基类|InputStream|OutputStream|Reader|Writer|
|访问文件|<strong>FileInputStream</strong>|<strong>FileOutputStream</strong>|<strong>FileReader</strong>|<strong>FileWriter</strong>|
|访问数组|<strong>ByteArrayInputStream</strong>|<strong>ByteArrayOutputStream</strong>|<strong>CharArrayReader</strong>|<strong>CharArrayWriter</strong>|
|访问管道|<strong>PipedInputStream</strong>|<strong>PipedOutputStream</strong>|<strong>PipedReader</strong>|<strong>PipedWriter</strong>|
|访问字符串|||<strong>StringReader</strong>|<strong>StringWriter</strong>|
|缓冲流|BufferedInputStream|BufferedOutputStream|BufferedReader|BufferedWriter|
|转换流|||InputStreamReader|OutputStreamWriter|
|对象流|ObjectInputStream|ObjectOutputStream|||
|抽象基类|FilterInputStream|FilterOutputStream|FilterReader|FilterWriter|
|打印流||PrintStream|||
|推回输入流|PushbackInputStream||PushbackReader||
|特殊流|DataInputStream|DataOutputStream|||

注：粗体字标出的类代表节点流，必须直接与指定的物理节点关联。
