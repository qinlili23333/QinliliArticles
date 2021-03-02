# 解密新东方Koolearn的视频  
F12可以抓包下载m3u8  
KOOLEARN-ET的本质是AES-128，m3u8里面改过来，删除后面的RESOLUTION和KEY URL  
F12找到hls.min.js，新东方这个hls.js被魔改过了，搜索BIN_DECRIPTED，下断点  
这一行上面定义的一个Array就是包含真实key的Array  
Array里面每一组key的结构如下：  
key：原始的key，base64编码后可用于N_m3u8DL  
min：开始的分片  
max：结束的分片  
按照这个Array切割m3u8并添加key，即可使用N_m3u8DL下载  
