#include <stdio.h>
#include <string.h>

#include <sys/types.h>				//数据类型定义
#include <sys/socket.h>  			//提供socket函数及数据结构
#include <netinet/in.h>				//定义数据结构sockaddr_in
#include <arpa/inet.h>				//提供IP地址转换函数
#include <netdb.h>					//提供设置及获取域名的函数
#include <sys/ioctl.h>				//提供对I/O控制的函数
#include <sys/poll.h>				//提供socket等待测试机制的函数
#include <errno.h>					//定义了通过错误码来回报错误资讯的宏

int main() {
	printf("test start!");
   
	int serverSockfd = socket(AF_INET, SOCK_STREAM, IPPROTO_IP);
	if(-1 == serverSockfd)
	{
		printf("socket error, create serverSockfd false, error = " ,errno);
		return 1;
	}
	
	struct sockaddr_in serveraddr;
	memset( &serveraddr, 0, sizeof(serveraddr) );
	serveraddr.sin_family 	= AF_INET;
	serveraddr.sin_port    = htons(9876);
	inet_aton("0.0.0.0", &(serveraddr.sin_addr) );
	
	int result = bind(serverSockfd, (struct sockaddr *)&serveraddr, sizeof(serveraddr));
	if(-1  == result)
	{
		printf("bind false, error = ", errno);
		return 1;
	}
	
	result = listen(serverSockfd, 1024);
	if(-1  == result)
	{
		printf("listen false, error = ", errno);
		return 1;
	}
	
	
	for(;;)
	{
		struct sockaddr_in clientaddr;
		socklen_t len	= sizeof(clientaddr);;
		int clientfd = accept(serverSockfd, (struct sockaddr*)&clientaddr, &len);
		char* addr = inet_ntoa(clientaddr.sin_addr);
		if(clientfd == -1)
		{
			printf("accept false, error = ", errno);
		}
		else
		{
			//测试多次调用inet_ntoa,看上一次数据是否变化
			printf("accept success, clientfd = ", clientfd, " addr = ", addr);	
		}
	}

	printf("test stop!");
    return 0;
}
