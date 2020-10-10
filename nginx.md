

基于Nginx虚拟主机配置实现，Nginx有三种类型的虚拟主机

基于IP的虚拟主机： 需要你的服务器上有多个地址，每个站点对应不同的地址，这种方式使用的比较少

基于端口的虚拟主机： 每个站点对应不同的端口，访问的时候使用ip:port的方式访问，可以修改listen的端口来使用

基于域名的虚拟主机： 使用最广的方式，上边例子中就是用了基于域名的虚拟主机，前提条件是你有多个域名分别对应每个站点，server_name填写不同的域名即可




nginx开启列目录
当你想让nginx作为文件下载服务器存在时，需要开启nginx列目录

```
server {
    location download {
        autoindex on;

        autoindex_exact_size off;
        autoindex_localtime on;
    }
}
```
autoindex_exact_size： 为on(默认)时显示文件的确切大小，单位是byte；改为off显示文件大概大小，单位KB或MB或GB

autoindex_localtime： 为off(默认)时显示的文件时间为GMT时间；改为on后，显示的文件时间为服务器时间

默认当访问列出的txt等文件时会在浏览器上显示文件的内容，如果你先让浏览器直接下载，加上下边的配置

```

if ($request_filename ~* ^.*?\.(txt|pdf|jpg|png)$) {
    add_header Content-Disposition 'attachment';
}

```




不允许通过IP访问

```
server {
    listen       80 default;
    server_name  _;

    return      404;
}
```
可能有一些未备案的域名或者你不希望的域名将服务器地址指向了你的服务器，这时候就会对你的站点造成一定的影响，需要禁止IP或未配置的域名访问，我们利用上边所说的default规则，将默认流量都转到404去

上边这个方法比较粗暴，当然你也可以配置下所有未配置的地址访问时直接301重定向到你的网站去，也能为你的网站带来一定的流量

```
server {
    rewrite ^/(.*)$ https://ops-coffee.cn/$1    permanent;
}
```
直接返回验证文件

```
location = /XDFyle6tNA.txt {
    default_type text/plain;
    return 200 'd6296a84657eb275c05c31b10924f6ea';
}
```
很多时候微信等程序都需要我们放一个txt的文件到项目里以验证项目归属，我们可以直接通过上边这种方式修改nginx即可，无需真正的把文件给放到服务器上
