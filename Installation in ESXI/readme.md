## 在ESXI7/8中安装iStoreOS
### 安装步骤（以X86为例)
#### 1. 下载iStoreOS最新固件(带efi) [iStoreOS固件下载](https://fw.koolcenter.com/iStoreOS/)
![image](https://user-images.githubusercontent.com/96930989/219864379-cf8b5cf9-b405-42bb-a3e7-327572315556.png)

#### 2. 解压缩至本地路径
![image](https://user-images.githubusercontent.com/96930989/219864404-87b34db2-0013-4ca1-b2a9-378969a2ea1f.png)

#### 3. 下载并安装[starwind](https://www.starwindsoftware.com/starwind-v2v-converter)

#### 4. 开始镜像转换
##### 选择local file（本机）
![image](https://user-images.githubusercontent.com/96930989/219864428-07fdb314-4289-4a08-afbb-d887968acbb4.png)

##### 选择解压缩得到的带efi的img文件`istoreos-21.02.3-2023020316-x86-64-squashfs-combined-efi.img`
![image](https://user-images.githubusercontent.com/96930989/219870281-bc6989d8-86ba-4e6c-a9f2-080a79664fe0.png)

##### 选择转化后镜像的存储位置，这里也选择local file（本机）
![image](https://user-images.githubusercontent.com/96930989/219864539-f362fe62-878a-40f4-a71d-e53dd84f39c1.png)

##### 选择目标镜像的文件格式-VMDK
![image](https://user-images.githubusercontent.com/96930989/219864543-9e6fd19c-f9c8-4866-b47a-b84e70d8a4ef.png)

##### 选择VMDK镜像的格式
![image](https://user-images.githubusercontent.com/96930989/219864545-6b3e6a18-b263-40c4-9d9f-33444a414f36.png)

##### 选择和ESXI服务器兼容的VMDK
![image](https://user-images.githubusercontent.com/96930989/219864547-d79abe18-1d75-4e2e-b09c-74492477a3b5.png)

##### 设定转化后镜像的名字，确认无误后点击`Convert`
![image](https://user-images.githubusercontent.com/96930989/219864550-52a96f0b-fa5f-4eb4-9787-23786340f723.png)

##### 等待进度条走完
![image](https://user-images.githubusercontent.com/96930989/219865818-d588b1a5-c226-4201-96fb-73e7af31a00f.png)

##### 转化后会生成两个VMDK文件（其中一个为1KB大小）
![image](https://user-images.githubusercontent.com/96930989/219865831-da068072-d6b4-4da8-ae63-76ed5713b776.png)

#### 5. 在ESXI中安装iStoreOS镜像
##### 在ESXI > Data explorer中新建文件夹，上传两个VMDK文件到ESXI硬盘
```
先上传1KB的VMDK，之后再上传另一个VMDK文件，上传完成后UI只会显示一个VMDK文件
```
![image](https://user-images.githubusercontent.com/96930989/219865969-74d18109-b83f-46be-9270-a4c84b7a36a9.png)

##### ESXI中新建服务器
![image](https://user-images.githubusercontent.com/96930989/219866018-548725e1-3505-4f83-96b5-0327d8759fbc.png)

##### 删除面板中本来有的硬盘，之后点击`添加现有硬盘`(Add hard disk > Existing hard disk)
![image](https://user-images.githubusercontent.com/96930989/219866081-eb013e3a-7856-447f-b3f2-68b76d0385d7.png)

##### 选中刚才上传后生成的VMDK文件，点击下一步至最后，保存，等待虚拟机创建完成
![image](https://user-images.githubusercontent.com/96930989/219866114-b76df6b2-1066-42d1-b725-00e83a1574ec.png)
![image](https://user-images.githubusercontent.com/96930989/219866126-946166c2-4a5e-45fe-aac5-2e758fa2683c.png)

##### 开机！
![image](https://user-images.githubusercontent.com/96930989/219866174-82a57b1d-653d-4140-aaf8-c72767ef66c1.png)

##### 查看console中OS安装进程，完成后按enter
![image](https://user-images.githubusercontent.com/96930989/219866186-8844834c-e006-4892-86f7-4d42e29dfb52.png)

##### 等待虚拟机器启动成功之后，输入：quickstart > 1.Change LAN IP，设定你想要的内网IP
![image](https://user-images.githubusercontent.com/96930989/219866203-be50a4d8-60ba-4d6d-aea6-fce528033520.png)

##### 设置完成后，在同一网段中输入刚才设定的IP应可登录iStoreOS界面，此时可将该VM关机，添加另一块硬盘或扩展现有硬盘
###### 扩展当前硬盘
![image](https://user-images.githubusercontent.com/96930989/219866325-ed3b8d73-4ae4-4e27-bb28-f2bb049a3b56.png)
###### 或者增加一块硬盘
![image](https://user-images.githubusercontent.com/96930989/219866274-b5eee73d-0c1b-40c1-b982-b43a24dded1a.png)
##### 进入iStoreOS界面后格式化并分配新分区
![image](https://user-images.githubusercontent.com/96930989/219907746-ea443c5d-82b5-4b62-a4f8-ae05eecf91b0.png)
