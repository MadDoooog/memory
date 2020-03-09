最开始是奕澍找我聊天，他给我介绍了动态二维码生成的py库，感觉很久没接触过这些方面的东西了，好久没接触新知识。今天搞出来了就记录一下

首先要运行py要安装python环境，自己的笔记本太慢，采用linux方便一些。

安装依赖
`yum -y install zlib-devel bzip2-devel openssl-devel ncurses-devel sqlite-devel readline-devel tk-devel gdbm-devel db4-devel libpcap-devel xz-devel`

下载py
`wget https://www.python.org/ftp/python/3.6.1/Python-3.6.1.tgz`

解压
`tar -zxvf Python-3.6.1.tgz`

进入目录
`cd Python-3.6.1`

配置目标路径
`./configure --prefix=/usr/local/python3`

编译执行
`make`
`make install`

建立软链接（快捷方式）
`ln -s /usr/local/python3/bin/python3 /usr/bin/python3`

添加环境变量
`vim /etc/profile`
`export PATH=$PATH:$HOME/bin:/usr/local/python3/bin`
`source /etc/profile`

pip是py的包管理工具，类比至于前端的npm，java的maven，所以pip也要安装好，这里暂时先掠过

这里面最重要的是环境变量要配好，重走这一系列步骤的原因就是环境变量没配好导致myqr命令会报“not found”

总之来到正题，myqr主要作用是利用图片生成二维码，这里希望直接用命令行生成，输入myqr命令有以下提示

	myqr [-h]
        [-v {1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20,21,22,23,24,25,26,27,28,29,30,31,32,33,34,35,36,37,38,39,40}]
        [-l {L,M,Q,H}] [-p PICTURE] [-c] [-con CONTRAST] [-bri BRIGHTNESS]
        [-n NAME] [-d DIRECTORY]
        Words

也就是说Words（信息）是必要的以外，其他是可选项，这里挨个测试

-h 帮助命令，得到以下内容，后面的测试内容就不多了

	positional arguments:
	  Words                 The words to produce you QR-code picture, like a URL
	                        or a sentence. Please read the README file for the
	                        supported characters.
	
	optional arguments:
	  -h, --help            show this help message and exit（帮助文档）
	  -v {1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20,21,22,23,24,25,26,27,28,29,30,31,32,33,34,35,36,37,38,39,40}, --version {1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20,21,22,23,24,25,26,27,28,29,30,31,32,33,34,35,36,37,38,39,40}
	                        The version means the length of a side of the QR-Code
	                        picture. From little size to large is 1 to 40.（大小尺寸）
	  -l {L,M,Q,H}, --level {L,M,Q,H}
	                        Use this argument to choose an Error-Correction-Level:
	                        L(Low), M(Medium) or Q(Quartile), H(High). Otherwise,
	                        just use the default one: H（容错率，默认高）
	  -p PICTURE, --picture PICTURE
	                        the picture e.g. example.jpg（素材图片）
	  -c, --colorized       Produce a colorized QR-Code with your picture. Just
	                        works when there is a correct '-p' or '--picture'.（色彩丰富）
	  -con CONTRAST, --contrast CONTRAST
	                        A floating point value controlling the enhancement of
	                        contrast. Factor 1.0 always returns a copy of the
	                        original image, lower factors mean less color
	                        (brightness, contrast, etc), and higher values more.
	                        There are no restrictions on this value. Default: 1.0（与图片配合时使用，1.0会直接按照原图片的色值，越低二值化越严重，默认1.0）
	  -bri BRIGHTNESS, --brightness BRIGHTNESS
	                        A floating point value controlling the enhancement of
	                        brightness. Factor 1.0 always returns a copy of the
	                        original image, lower factors mean less color
	                        (brightness, contrast, etc), and higher values more.
	                        There are no restrictions on this value. Default: 1.0（描述同上，待测试）
	  -n NAME, --name NAME  The filename of output tailed with one of {'.jpg',
	                        '.png', '.bmp', '.gif'}. eg. exampl.png（名字，必须加后缀）
	  -d DIRECTORY, --directory DIRECTORY
	                        The directory of output.（输出路径）

这里经过测试有一些结果

-v 太大会很难看，10就很好（6、7是一个分界点，7会有中部的识别点，而6及以下只有四角的识别点）

-p 直接加文件名，如果文件名有特殊字符会有奇怪的问题，尽量普通字符。生成的目标文件叫“图片名_qrcode”

-c 不加这个参数就是黑白的

-con 对比度

-bri 亮度，这两项都推荐不动，当然适当调整可以修改二维码质感


基本的使用就到这里，真是很难得有了学习新知识的快感。以后可以吧平时的内容也push上来。github的界面也有了一些小小的变化，以后常来
