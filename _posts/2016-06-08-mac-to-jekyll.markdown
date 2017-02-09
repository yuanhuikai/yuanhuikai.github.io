---
layout: post
title:  "Jekyll Blog搭建笔记"
date:   2016-06-08 22:21:49
categories: Tools 
tags: Tools 
---
博客模版参考[peiwen][github]，在此基础上修改，Jekyll相关文档，详情请移步[Jekyll docs][jekyll]。

安装环境：  

	ruby 2.0.0、gem 2.4.8、Jekyll 3.4.0  

<font color="##FF0000">注意：</font>
<ul>
	<li>ruby 最新版本为2.4，这个版本会有问题，切换为2.0.0</li>
	<li>安装 Xcode Command-Line Tools ：终端下输入 xcode-select --install </li>
</ul>

<div>
	<table>
		<thead>
			<tr>
				<th>Jekyll目录文件夹说明</th>
			</tr>
		</thead>
		<tbody>
			<tr>
				<td>_config.yml</td>
				<td>保存配置数据</td>
			</tr>
			<tr>
				<td>_includes</td>
				<td>可以加载这些包含部分到你的布局或者文章中以方便重用</td>
			</tr>
			<tr>
				<td>_layouts</td>
				<td>layouts 是包裹在文章外部的模板</td>
			</tr>
			<tr>
				<td>_posts</td>
				<td>放置博客文章</td>
			</tr>
			<tr>
				<td>_site</td>
				<td>Jekyll serve之后产生的文件，<font color="#FF000">git上传代码时注意不要上传</font></td>
			</tr>
			<tr>
				<td>index.html</td>
				<td>如果这些文件中包含 YAML 头信息 部分，Jekyll 就会自动将它们进行转换</td>
			</tr>
			<tr>
				<td>assets</td>
				<td>图片及下载资源目录可以利用站点的根目录进行引用，site.url根站点</td>
			</tr>
		</tbody>
	</table>
</div>

高亮代码段：
<code>
	<span></span>
	"highlight ruby"
	<span></span>
</code>


