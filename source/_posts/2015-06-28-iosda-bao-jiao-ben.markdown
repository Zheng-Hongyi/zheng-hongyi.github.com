---
layout: post
title: "iOS打包脚本（有cocoapods）"
date: 2015-06-28 17:20:51 +0800
comments: true
categories: Blog
---
本文章借助了xctool，所以要首先安装xctool，要安装xctool，这里通过brew（一个包管理工具），所以这里的步骤是：<br>
1、安装brew <br>
curl -LsSf http://github.com/mxcl/homebrew/tarball/master |sudo tar xvz -C/usr/local --strip 1 <br>
2、安装xctool <br>
      sudo brew update <br>
      sudo brew install xctool <br> 
3、然后就可以运用这里的脚本了 （建议放在一个文件里然后运行）

<h>
脚本说明：<br>

	#!/bin/sh

	#  autoCompile.sh

	#
	#  Created by zheng on 15-5-6.
	#  Copyright (c) 2015年 zheng. All rights reserved.

	#输出目录 (这个需要配置)
	ipaDir="/Users/hongyizheng/Desktop/iPa/Keep"
	mkdir "${ipaDir}"

	#临时目录，这里是要将源代码拷贝到一个临时目录 （也需要配置）
	sourceDir="/Users/hongyizheng/Desktop/iPa/Temp"
	mkdir "${sourceDir}"

	#源文件所在目录 （需要配置，这里是临时的）
	distDir="/Users/hongyizheng/Desktop/workbench/keepdev/temp"
	cp -R "${distDir}" "${sourceDir}"

	#简单的配置
	appName="Keep"
	target="Keep"
	#参数1 版本号
	clientVersion=$1
	#参数2 打包时间
	compileTime=$2

	CONFIGURATION="Release"
	KEYCHAIN="/Library/Keychains/System.keychain"

	#一个临时目录
	buildPath="/Users/hongyizheng/Desktop/keep.xcarchive"
	#最后的输出路径
	ipaName="/Users/hongyizheng/Desktop/keep_${clientVersion}_${compileTime}.ipa"
	#证书 (需要配置，输入文件名称即可)
	profile=""


	#进入临时目录准备开始编译 （这里需要注意与工程一直）
	cd "${sourceDir}/temp"

	security unlock-keychain -p ${PASSWORD} ${KEYCHAIN}

	#开始编译
	xctool -workspace "Keep.xcworkspace" -scheme "Keep" -configuration ${CONFIGURATION} clean

	xctool  -workspace "Keep.xcworkspace" -scheme "Keep" archive -archivePath ${buildPath}
	#开始导出
	xcodebuild -exportArchive -exportFormat IPA -archivePath ${buildPath} -exportPath ${ipaName} -exportProvisioningProfile "$profile"
	#删除临时文件
	rm -rf "${sourceDir}"

	echo "=========Success========="
	echo "Waiting for next runtime......"


	#done
