kodbox v1.26 has a command execution vulnerability

official website：https://kodcloud.com/

version:1.26

1.After setting up the environment, download the WebConsole plug-in

![WPS图片(1)](https://github.com/mohdkey/cve/assets/114804407/c9fbd121-65b5-471b-8fd3-7e3ae7d9fce1)

![WPS图片(2)](https://github.com/mohdkey/cve/assets/114804407/71d31ab2-1c36-491c-ba22-e3493ebe8c1e)

2. Capture the corresponding code for analysis
![WPS图片(3)](https://github.com/mohdkey/cve/assets/114804407/7d778740-4384-4a70-8396-7fd6f740b567)

Find routing is/plugins/webConsole/lib/index. The PHP

![WPS图片(4)](https://github.com/mohdkey/cve/assets/114804407/77ed6999-a72a-49be-8c9b-4b6e60e1c3d4)

3. Index.php starts with check() for login authentication, and includes./webconsole.php.txt at the bottom, so the last file included is the key

![WPS图片(5)](https://github.com/mohdkey/cve/assets/114804407/e9f6619c-f626-4b60-804c-ed54973022c9)

4.Analyze webconsole.php.txt and delete the.txt suffix for auditing purposes,If POST instantiates the WebConsoleRPCServer class, call the Execute() method in the class through $rpc_server.

![WPS图片(6)](https://github.com/mohdkey/cve/assets/114804407/f15ba429-e9e1-422d-a33a-6cf0a88246e9)

The processCall() method is invoked in Execute() to follow up processCall

![WPS图片(7)](https://github.com/mohdkey/cve/assets/114804407/206eccb0-3fb4-40d3-b761-8cd5957e7c91)

There are five parameters in params, the last of which is the command to execute

![WPS图片(8)](https://github.com/mohdkey/cve/assets/114804407/13036f7f-10d8-4d91-82b9-580ec12f39c5)

5.The console directly executes system commands

![WPS图片(9)](https://github.com/mohdkey/cve/assets/114804407/df1ad42a-fa51-46ee-aa85-032829e801c1)

![WPS图片(10)](https://github.com/mohdkey/cve/assets/114804407/f5a32886-fae6-40e0-ada7-a4df230f66d4)

