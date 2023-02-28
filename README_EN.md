# TaskBuilder_ChatGPT
[Taskbuilder Low-Code Development Tool official website:http://taskbuilder.taskmsg.com/](http://taskbuilder.taskmsg.com/)
[|中文|](https://github.com/huppygovip/TaskBuilder_ChatGPT/blob/main/README.md)***[|English|](https://github.com/huppygovip/TaskBuilder_ChatGPT/blob/main/README_EN.md)

Click to download::[ChatGPT service docking file](http://taskbuilder.taskmsg.com/TaskMsgDownload?fileCode=413833c2846b52fd9b294d1c72294bdc)

 **1.Use TB to open the service file and modify the API key. apikey: Bearer + space to reserve and add your own key if the key may be invalid.**

![image.png](https://cdn.nlark.com/yuque/0/2023/png/26820059/1677502636557-19dc0c91-dd96-4631-8264-28a0cef72201.png#averageHue=%23fdfcfb&clientId=u6e6a6ce0-0cf7-4&from=paste&id=uc24e886a&name=image.png&originHeight=493&originWidth=938&originalType=url&ratio=1&rotation=0&showTitle=false&size=40436&status=done&style=none&taskId=u20945e0f-5395-4c9b-9e32-3f365a3f626&title=)
**2.用TB打开服务文件 修改APIkey apikey :Bearer+空格保留加上key key可能失效替换成自己的**

Parameters used:
model: ID of the model to be used (here you can see all available models)
Prompt: Trigger command for generating results
max_token: the maximum number of tokens generated when completed (here you can see the tokenizer used by OpenAI)
temperature: the sampling strategy to use. Values close to 1 bring more risk/creativity to the model, while values close to 0 generate well-defined answers.

① context: Context information
② model: Model information
③ beamSize: Batch size for each iteration
④ numIterations: Number of iterations
⑤ maxSequenceLength: Maximum sequence length
⑥ maxDecodingLength: Maximum decoding length
⑦ responseNum: Number of responses

![image.png](https://cdn.nlark.com/yuque/0/2023/png/26820059/1677502636592-1f798c05-ce44-4c84-b008-103d2a1085eb.png#averageHue=%23534436&clientId=u6e6a6ce0-0cf7-4&from=paste&id=ue45c0ead&name=image.png&originHeight=714&originWidth=1196&originalType=url&ratio=1&rotation=0&showTitle=false&size=98562&status=done&style=none&taskId=uf134a5c6-56cb-48c5-8800-a6de1e4bafd&title=)

**3.How to get the OpenAPI key**
The access address is https://beta.openai.com/account/api-keys to generate an API key.

If you cannot access the OpenAI website, you will need to use a proxy to access it.
![image.png](https://cdn.nlark.com/yuque/0/2023/png/26820059/1677502636606-bedc4765-3bde-4c1e-a76e-47510a9a7395.png#averageHue=%23fdfcfc&clientId=u6e6a6ce0-0cf7-4&from=paste&id=uaf27bd9c&name=image.png&originHeight=772&originWidth=1267&originalType=url&ratio=1&rotation=0&showTitle=false&size=114043&status=done&style=none&taskId=u6141f4dc-b948-447b-aaed-e8a84527406&title=)

**4.API key replacement service.**
![image.png](https://cdn.nlark.com/yuque/0/2023/png/26820059/1677502636589-280ea824-3162-4998-8b59-0feef39b9743.png#averageHue=%2380694a&clientId=u6e6a6ce0-0cf7-4&from=paste&id=ud1540fa9&name=image.png&originHeight=394&originWidth=692&originalType=url&ratio=1&rotation=0&showTitle=false&size=43136&status=done&style=none&taskId=uc761d30c-cf3b-4318-9fd2-3b636eb2001&title=)

**5.Call this service in TB designer**
![image.png](https://cdn.nlark.com/yuque/0/2023/png/26820059/1677502636593-5436a852-25e7-46de-81e8-4cd86d3e0341.png#averageHue=%23383737&clientId=u6e6a6ce0-0cf7-4&from=paste&id=u894c8454&name=image.png&originHeight=864&originWidth=1501&originalType=url&ratio=1&rotation=0&showTitle=false&size=72106&status=done&style=none&taskId=uf26dec7c-4782-48b6-b74e-83a70399bbf&title=)6.编辑代码

![image.png](https://cdn.nlark.com/yuque/0/2023/png/26820059/1677502637559-5f759607-6d9d-4f71-9881-d5e95f77202d.png#averageHue=%23262525&clientId=u6e6a6ce0-0cf7-4&from=paste&id=ud5ba8ed3&name=image.png&originHeight=667&originWidth=1015&originalType=url&ratio=1&rotation=0&showTitle=false&size=55391&status=done&style=none&taskId=u3848f214-6400-49af-9d3a-4b5d56e94bf&title=)

//context Translation: To store the result of the previous call for a global variable, this global variable needs to be used for related dialogues. The submitted content for the related dialogues should be the result of the previous call followed by '\n' and the question asked this time.
function button1_onClick() {

    //The question raised / The question posed.
    let problem = textArea_problem.value;
    // Concatenate the previous answer and the current question for contextual association.
    if(context){
        problem=context+'\n'+ problem;
    }
    if (problem) {
        service_chatgpt.request({ problem: problem}, function (req, res) {
            console.log(res.data)
            if (res.data) {
                textArea_results.val(res.data)
              speakdata(res.data)
                //The result of the previous question is stored in the historical results
                context = res.data;
            }
        })
    }
   
   
   
}

**6.Voice broadcast function**

In the code above,
speakdata(res.data)
is the voice broadcast function.
The following is the code for voice broadcast:
function speakdata(textcontent) {

    var cishu = 1;//Number of times the speech is played
    var synth = window.speechSynthesis
    var u = new SpeechSynthesisUtterance();
    u.lang = "zh-CN";  // Language used: Chinese
    u.volume = 100;      // Volume: 1
    u.rate = 1;        // Speed: 1
    u.pitch =1;       // Pitch: 1
    // synth.speak(u);    // This playback is repeated
    speechSynthesis.speak(u)//This playback is not repeated
    function speak(textToSpeak) {
        u.text = textToSpeak;
        synth.speak(u)
    }
    for (var i = 0; i < cishu; i++) {
        speak(textcontent)
    }
}

**8.The voice input function is estimated to call a third-party language function interface to convert speech into text.**
