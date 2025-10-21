### 克隆漏洞检测

#### 可执行文件
我们提供了clone_detection.exe来进行克隆漏洞检测，使用方法为
`./clone_detection.exe -p project_path -o output_file`
`./clone_detection.exe -v`
该工具搜索项目内所有后缀为`.java`,`.py`,`.js`的文件进行克隆漏洞检测

#### 源代码
如果需要运行源代码，可以参考以下内容
##### 项目架构
```markdown
├── script: 从cve数据库中收集cve漏洞信息
│    └── build.py : 从`CVEfixes.db`收集信息，该数据文件可从
|              [CVEfixes_v1.0.7.zip] (https://zenodo.org/records/7029359/files/CVEfixes_v1.0.7.zip?download=1)下载，
|              或者登录[网站](https://zenodo.org/records/7029359)下载
│                         
├── resource : 我们预先收集的漏洞数据，由于原始文件过大，我们只选取了部分上传，如果需要运行完整的漏洞库匹配，
│   │          请下载[CVEfixes_v1.0.7.zip] (https://zenodo.org/records/7029359/files/CVEfixes_v1.0.7.zip?download=1) 
│   │          并使用script/build.py构建完整漏洞文件。
│   ├── java_cve.json : java漏洞数据集
│   ├── js_cve.json : js漏洞数据集
│   └── py_cve.json : python漏洞数据集
├── test : 用于测试的数据
└── src: 运行克隆检测
     ├── main.py python main.py -p project_path -o output_file，
     │              其中`project_path`是项目地址，`output_file`是保存结果的文件
     └── parse.py : 提供语法解析功能 
```

#### 依赖

|依赖|版本|
| :--- | :--- |
|datasketch|1.6.5|
|tree-sitter|0.23.2|
|tree-sitter-java|0.23.5|
|tree-sitter-javascript|0.23.1|
|tree-sitter-python|0.23.6|

#### 运行script/build.py
该文件对运行环境没有特殊要求，如果无法运行，可以参考以下环境配置
|依赖|版本|
| :--- | :--- |
|sqlite3|3.50.2 2025-06-28 14:00:48 2af157d77fb1304a74176eaee7fbc7c7e932d946bf25325e9c26c91db19e3079 (64-bit)|
|pandas|1.4.1|
|python|3.9.7|

### 打包
如果需要二次开发或自行定制打包，打包命令可参考：
```shell
 pyinstaller --onefile  --noupx --add-data  "resource/*:resource" --name=clone_detection src/main.py
```