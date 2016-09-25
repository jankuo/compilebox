## `CompileBox` 简介 ##

CompileBox 使用一个 *Docker* 沙盒环境来编译运行不可信的代码，然后返回结果给客户。
用户能够提交系统支持的开发语言代码片段。 
`CompileBox`提供的是沙盒环境，编译和运行代码都在一个封闭的隔离的环境里, 这使得你不用过于担心那些 不安全的不可信的代码破坏你的系统或者获取你的电脑信息。
你可以用 `CompileBox` 为你的客户提供服务，他们能够在浏览器里提交和运行它们的代码.

你可以通过以下实例了解:

 - 最小实例: [compile.remoteinterview.io][1]
 - 完没实例: [codepad.remoteinterview.io][2]

## `CompileBox` 是如何工作的? ##

客户端通过API接口提交想要运行的代码和开发语言类型给服务端，服务端创建一个有限的资源和给定的超时(默认20s) *Docker* 沙盒容器,然后编译运行提交的代码。编译运行后,服务端把结果返回给客户端,然后删除所有的运行环境，保证每次编译运行的都是全新的环境。


## 安装步骤 ##

* Go to the 'Setup' directory.
    - Open the Terminal as root user
    
    - Execute the script **Install_*.sh**, select the file which best suites your Operating System description. This will install the Docker and NodeJs pre-requisites to your system and create an image called 'virtual_machine' inside the Docker. DockerVM may take around 20 to 30 minutes depending on your internet connection.
    
    - Once the Install script executes successfully, copy the folder named 'API' to your desired path.
    
    - Open app.js in the API folder and set the variable values as follows.
    
        1. **timeout_value**: The time in seconds till which the API should wait for the output of the code before generating an "Execution Timed Out" message.
        2. **port**: The port on which the server will listen, the default port is 80.
        
    - To test the installation, open a new terminal windows, cd to the API folder and type the following command
    ```
    $ npm install .
    ```
    to install all needed nodejs modules, followed by
    
    ```
    $ sudo nodejs app.js
    ```
    - If everything has been setup correctly in app.js file, you will see the following message on your terminal
    ```
    Listening at <port_number>
    ```

    - Navigate your browser to http://127.0.0.1/
    
    ## Supported Operating Systems ##
    The CompileBox API has been installed and run succesfully on the following platforms
    - Ubuntu 12.04 LTS
    - Ubuntu 13.10
    - Ubuntu 14.04 LTS
    - Linux Mint 15 
    
## Selecting The languages for Installation Inside Docker ##

The default Dockerfile installs the most used languages. To remove/change any, follow these steps

In order to select languages of your own choice you need to make 2 changes.<br>
        1. <B>Dockerfile</B>: This file contains commands that you would normally give in your terminal to install that language. Add the required commands preceeded by the RUN keyword inside the Dockerfile. Run the "UpdateDocker.sh" script, present in the same folder if you are adding new language to already installed API, execute the Install_*.sh script otherwise, from your terminal after making the changes to your Dockerfile.<br>
        2. <B>Compilers.js</B>: This file is inside the API folder. The compiler name, the source file name and the execution commands to Docker Container are taken from this file. This file only contains an array, which is described in detail inside the file. Add the credentials of the language you are adding to this array.<br>
        
The next time you wish to compile using this language, simply issue the language_id , which is  same as the index of the language in the array present in Compilers.js, along with your code to the NodeJs server.

> Note: Additionally while setting up the API for the first time, you can comment out those languages from the Dockerfile that you do not wish to install, since they can be added later.

## 添加其它的开发语言 ##

请按照以下步骤添加其它的开发语言.
<br>
1. <b>Modify the Dockerfile</b>: The Dockerfile is present in the Setup folder and contains the commands that you would normally write in your terminal to install a particular language. Append the commands for the language of your choice to the end of the Dockerfile.         <br>
2. <b>Execute UpdateDocker.sh</b> and wait for your language to be installed inside the virtual machine. <br>
3. <b>Modify Compilers.js</b>: Compilers.js file is available in the API folder and contains the information needed by app.js to compile a given source code inside Docker container. The file only consists of an array which is described in detail inside the file. Add the credentials for your language to the Array.

> 注意:   你必须在网络处于连接状态下运行 `UpdateDocker.sh`

  [1]: http://compile.remoteinterview.io
  [2]: http://codepad.remoteinterview.io
