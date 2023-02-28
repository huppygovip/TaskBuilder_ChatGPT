点击下载:[chatgpt服务对接文件](http://taskbuilder.taskmsg.com/TaskMsgDownload?fileCode=413833c2846b52fd9b294d1c72294bdc)

 **1.把下载的服务文件放到项目的服务文件夹下**

![image.png](https://cdn.nlark.com/yuque/0/2023/png/26820059/1677502636557-19dc0c91-dd96-4631-8264-28a0cef72201.png#averageHue=%23fdfcfb&clientId=u6e6a6ce0-0cf7-4&from=paste&id=uc24e886a&name=image.png&originHeight=493&originWidth=938&originalType=url&ratio=1&rotation=0&showTitle=false&size=40436&status=done&style=none&taskId=u20945e0f-5395-4c9b-9e32-3f365a3f626&title=)
**2.用TB打开服务文件 修改APIkey apikey :Bearer+空格保留加上key key可能失效替换成自己的**
使用的参数：
model ：要使用的模型的 ID（在这里你可以看到所有可用的模型）
Prompt：生成结果的触发指令
max_token：完成时生成的最大token数量（这里可以看到OpenAI使用的tokenizer）
temperature：要使用的采样策略。接近 1 的值会给模型带来更多风险/创造力，而接近 0 的值会生成明确定义的答案

① context：上下文信息

② model：模型信息

③ beamSize：每次迭代的每批数据大小

④ numIterations：迭代的次数

⑤ maxSequenceLength：最长序列长度

⑥ maxDecodingLength：最大解码长度

⑦ responseNum：响应数量

![image.png](https://cdn.nlark.com/yuque/0/2023/png/26820059/1677502636592-1f798c05-ce44-4c84-b008-103d2a1085eb.png#averageHue=%23534436&clientId=u6e6a6ce0-0cf7-4&from=paste&id=ue45c0ead&name=image.png&originHeight=714&originWidth=1196&originalType=url&ratio=1&rotation=0&showTitle=false&size=98562&status=done&style=none&taskId=uf134a5c6-56cb-48c5-8800-a6de1e4bafd&title=)

**3.如何获取openAPIken**
获取地址https://beta.openai.com/account/api-keys 生成

如果不能访问openai网站 就只能通过代理进去访问了 
![image.png](https://cdn.nlark.com/yuque/0/2023/png/26820059/1677502636606-bedc4765-3bde-4c1e-a76e-47510a9a7395.png#averageHue=%23fdfcfc&clientId=u6e6a6ce0-0cf7-4&from=paste&id=uaf27bd9c&name=image.png&originHeight=772&originWidth=1267&originalType=url&ratio=1&rotation=0&showTitle=false&size=114043&status=done&style=none&taskId=u6141f4dc-b948-447b-aaed-e8a84527406&title=)

**4.替换服务的APIkey**
![image.png](https://cdn.nlark.com/yuque/0/2023/png/26820059/1677502636589-280ea824-3162-4998-8b59-0feef39b9743.png#averageHue=%2380694a&clientId=u6e6a6ce0-0cf7-4&from=paste&id=ud1540fa9&name=image.png&originHeight=394&originWidth=692&originalType=url&ratio=1&rotation=0&showTitle=false&size=43136&status=done&style=none&taskId=uc761d30c-cf3b-4318-9fd2-3b636eb2001&title=)

**5.在TB设计器中调用这个服务**
![image.png](https://cdn.nlark.com/yuque/0/2023/png/26820059/1677502636593-5436a852-25e7-46de-81e8-4cd86d3e0341.png#averageHue=%23383737&clientId=u6e6a6ce0-0cf7-4&from=paste&id=u894c8454&name=image.png&originHeight=864&originWidth=1501&originalType=url&ratio=1&rotation=0&showTitle=false&size=72106&status=done&style=none&taskId=uf26dec7c-4782-48b6-b74e-83a70399bbf&title=)6.编辑代码

![image.png](https://cdn.nlark.com/yuque/0/2023/png/26820059/1677502637559-5f759607-6d9d-4f71-9881-d5e95f77202d.png#averageHue=%23262525&clientId=u6e6a6ce0-0cf7-4&from=paste&id=ud5ba8ed3&name=image.png&originHeight=667&originWidth=1015&originalType=url&ratio=1&rotation=0&showTitle=false&size=55391&status=done&style=none&taskId=u3848f214-6400-49af-9d3a-4b5d56e94bf&title=)

//context 为全局变量 存放上一次的结果；需要关联对话必须用到这个全局变量，
//关联对话提交内容为:上的结果+‘\n’+这次提的问题
function button1_onClick() {

    //提出的问题
    let problem = textArea_problem.value;
    // 拼接上次回答和本次问题,用于关联上下文
    if(context){
        problem=context+'\n'+ problem;
    }
    if (problem) {
        service_chatgpt.request({ problem: problem}, function (req, res) {
            console.log(res.data)
            if (res.data) {
                textArea_results.val(res.data)
              speakdata(res.data)
                //上次提出的问题 的结果放到历史结果
                context = res.data;
            }
        })
    }
   
   
   
}

**7.语言播报功能**

上面代码中
speakdata(res.data)
为语言播报功能

下面为语言播报代码
function speakdata(textcontent) {

    var cishu = 1;//语音播报次数
    var synth = window.speechSynthesis
    var u = new SpeechSynthesisUtterance();
    u.lang = "zh-CN";  // 使用的语言:中文
    u.volume = 100;      // 声音音量：1
    u.rate = 1;        // 语速：1
    u.pitch =1;       // 音高：1
    // synth.speak(u);    // 这个播放是重复播放
    speechSynthesis.speak(u)//这个是不重复播放
    function speak(textToSpeak) {
        u.text = textToSpeak;
        synth.speak(u)
    }
    for (var i = 0; i < cishu; i++) {
        speak(textcontent)
    }
}

**8.语言输入功能估计要调用第三方语言功能接口，把语言转成文字**
