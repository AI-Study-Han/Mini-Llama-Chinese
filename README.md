# Mini-Llama2-Chinese
<p align="center">
  <img src="Mini-Llama2-Chinese.png" alt="Mini-Llama-Chinese" style="width:30%;">
</p>

想要从零开始训练一个中文的mini大语言模型，目前的目标是学习和尝试使用各种方法训练和优化模型，最终训练一个较小的模型可以进行基本的对话，具体模型大小根据手头的机器决定。目前模型训练代码主要参考[baby-llama2-chinese](https://github.com/DLLXW/baby-llama2-chinese)，只是修改了部分参数，这里就不放代码了，后面如果对模型代码有较大的更改再上传。   

**目前还在不断的学习和尝试中，后续会将训练好的模型整理、上传。大家有什么可以提高模型效果的建议可以留言，会选择进行尝试优化，训练完成后再上传上来，一起试试效果。**  
目前model0还是什么都不能回答，model1和model2已经可以简单的回答一些问题了，至少生成的还像个人话，但是涉及计算和逻辑的问题还是完全不行。model3增大了模型尺寸，不知道为什么不行了。


|模型名称|训练数据|模型下载地址|
|:----:|:----:|:----:|
|[model-0](#model-0)|维基百科中文、百度百科、医疗文本|[模型下载](https://huggingface.co/My521/Mini-Llama-Chinese)|
|[model-0-sft](#model-0)|bell、alpaca-zh|[模型下载](https://huggingface.co/My521/Mini-Llama-Chinese) |  
|[model-1](#model-1)|英文文本108G，中文文本217G，中英翻译文本6G|[模型下载](https://huggingface.co/My521/Mini-Llama-Chinese)|
|[model-1-sft](#model-1)| |[模型下载](https://huggingface.co/My521/Mini-Llama-Chinese)| 
|[model-2](#model-2)|英文文本318G，中文文本232G|[模型下载](https://huggingface.co/My521/Mini-Llama-Chinese)|
|[model-2-sft](#model-2)| |[模型下载](https://huggingface.co/My521/Mini-Llama-Chinese)| 
|[model-3](#model-3)| 英文文本318G，中文文本232G|[模型下载](https://huggingface.co/My521/Mini-Llama-Chinese)|
|[model-3-sft](#model-3)| |[模型下载](https://huggingface.co/My521/Mini-Llama-Chinese)| 


测试问题：

    你知道北京吗？  
    你知道杭州有哪些美食吗？
    你知道中国的四大名著吗？
    你了解美国的历史吗？
    左手一只鸭，右手一只鸡。交换两次后左右手里各是什么？
    鸡兔同笼，共35只头，94只脚，问鸡兔各多少？
    将以下中文翻译成英文：穿衣需要适应天气变化。
### model-0  
模型预训练数据：维基百科中文、百度百科、医疗文本，共17GB的文本，token数量没有计算。  
预训练轮数：1 epoch。
模型结构：max_seq_len = 512，dim = 1024，n_layers = 12，n_heads = 8。  
指令微调数据：直接使用了[bell](https://huggingface.co/datasets/BelleGroup/train_1M_CN)、[alpaca-zh](https://huggingface.co/datasets/shibing624/alpaca-zh)的微调数据集，没有进行清洗。  
指令微调轮数：2 epoch。  
模型效果：

    微调1轮
    问题：你知道北京吗？
    回答： 是的（英语）。

    问题：你知道杭州有哪些美食吗？
    回答： 很可能是很聪明。你认为什么。你可以知道吗？

    问题：你知道中国的四大名著吗？
    回答： 请提供您的姓名，您能提供这些信息吗？

    问题：你了解美国的历史吗？
    回答： 是，我是一个语言模型无法回答您的问题。

    问题：左手一只鸭，右手一只鸡。交换两次后左右手里各是什么？
    回答： 
    什么？”

    问题：鸡兔同笼，共35只头，94只脚，问鸡兔各多少？
    回答： 
    1400000, 

    问题：将以下中文翻译成英文：穿衣需要适应天气变化。
    回答： 需要提供更多信息，请提供相关描述。

    微调2轮  
    问题：你知道北京吗？
    回答： 是的（英语）。

    问题：你知道杭州有哪些美食吗？
    回答： 很；很棒。你认为什么。你可以知道吗？

    问题：你知道中国的四大名著吗？
    回答： 请提供一些关于中国历史的一句话或名称的名称。

    问题：你了解美国的历史吗？
    回答： 是的。在20年前，您在哪个领域的问题。 
    。

    问题：左手一只鸭，右手一只鸡。交换两次后左右手里各是什么？
    回答： 好的，或者

    问题：鸡兔同笼，共35只头，94只脚，问鸡兔各多少？
    回答： 1000
    


    问题：将以下中文翻译成英文：穿衣需要适应天气变化。

    回答： 无法提供具体的中文翻译: 
    "R莓意思是无法理解，无法回答问题。


### model-1  
模型预训练数据：英文文本108G，中文文本217G，中英翻译文本6G，token数量没有计算。  
预训练轮数：1 epoch。  
模型结构：max_seq_len = 512，dim = 1024，n_layers = 16，n_heads = 16。  
指令微调数据：BELLE、GPT-4-LLM、MOSS、Firefly，使用n-gram、MinHash、LSH的方法进行去重，4261624条数据保留1245488个   
指令微调轮数：1、2  
模型效果：  

    微调1轮  

    问题：你知道北京吗？
    回答： 北京是一个美丽的城市，拥有许多历史悠久的建筑和文化遗产。您对北京的文化和历史感兴趣吗？

    问题：你知道杭州有哪些美食吗？
    回答： 杭州有很多美食非常受欢迎，包括：西湖醋鱼、杭州酸鱼、西湖醋鱼、杭州炒面、杭州 炒面、杭州 炒面、杭州 炒面、杭州 炒面、杭州 炒面、杭州 炒面、杭州 炒面、西湖醋鱼、西湖醋鱼、杭州 炒面、杭州 炒面、杭州 炒面、杭州 炒面、杭州 炒面、杭州 炒面、杭州 炒面、杭州 炒面、杭州 炒面、杭州 炒面、杭州 炒面、杭州 炒

    问题：你知道中国的四大名著吗？
    回答： 中国的四大名著是《红楼梦》、《西游记》和《西游记》三种。它们都是中国文学巨匠、诗人和小说家所创作的作品。这些小说都内容丰富，内容深刻，充满了悲剧和喜剧元素，具有深厚的文化底蕴和独特的艺术价值。中国的四大名著是中国文学的宝库，也是世界文学的宝库之一。

    问题：你了解美国的历史吗？
    回答： 作为一个人工智能助手，我没有对任何国家或地区的了解。但是，我可以告诉您，美国的历史可以追溯到20世纪50年代和60年代，那时美国已经成为了全球最独立的国家之一。在20世纪60年代，美国开始采用“美国式管理”政策，旨在保持经济自由，促进经济合作和经济发展。在70年代，美国开始实施“美国式民主”政策，该政策在1961年通过，并开始了对非裔美国人的不平等对待。此外，在80年代，美国还开始实施“经济自由”

    问题：左手一只鸭，右手一只鸡。交换两次后左右手里各是什么？
    回答： 右手一只鸭，右手一只鸡。

    问题：鸡兔同笼，共35只头，94只脚，问鸡兔各多少？
    回答： 这只是描述一种动物，而不是一个群体。 鸡兔是动物中比较常见的一种，它们通常有三个头，94个腿，94只脚，它们通常都吃肉。

    问题：将以下中文翻译成英文：穿衣需要适应天气变化。
    回答： "10-15: 衣物需要适应天气变化。"

    微调2轮
    问题：你知道北京吗？
    回答： 北京是中国的首都，也是中国最大的城市之一。虽然北京是一个城市，但它也拥有丰富的文化和历史。北京有许多令人惊叹的景点，包括长城、故宫、天坛、圆明园等。此外，北京还有许多美食和文化活动，如紫禁城、天坛、长城等。

    问题：你知道杭州有哪些美食吗？
    回答： 作为AI助手，我不能为您提供关于杭州饮食的详细信息。但是，可能有很多西湖地区都有美食，比如：
    1. 西湖龙井茶：西湖龙井茶是中国著名的中式名茶，以龙井茶及草本植物为原料，具有浓郁的龙井味，口感醇和，具有降火、补肝、明目、利尿等功效。
    2. 西湖龙井鱼头：西湖龙井鱼头是西湖地区特色菜，以鱼头为主料，鱼头活动灵活，口感鲜嫩。
    3. 

    问题：你知道中国的四大名著吗？
    回答： 当然，中国的四大名著之一是《红楼梦》。它是中国古代四大悲剧之一，也是中国文学的经典之作。它以红楼梦的写法、文学风格和文学价值为特征，是中国文学经典之一。

    问题：你了解美国的历史吗？
    回答： 作为一个人工智能助手，我无法了解您的历史，因为我的目的是提供有关特定国家或地区的信息。如果您有任何问题或需要帮助，请告诉我。

    问题：左手一只鸭，右手一只鸡。交换两次后左右手里各是什么？
    回答： 这个问题需要更具体的信息才能回答，因为“左”和“右”在不同的文化和社会环境中可能存在差异。

    问题：鸡兔同笼，共35只头，94只脚，问鸡兔各多少？
    回答： 鸡兔同笼共35只，94只脚。

    问题：将以下中文翻译成英文：穿衣需要适应天气变化。
    回答： The 20- 25-G 20-30- 20-30-30- 20-30-30-30-30-30-30-30-30-30-30-30-30-30-30
      


### model-2  
模型预训练数据：英文文本318G，中文文本232G，token数量中文58 B，英文81 B，共约140 B token。  
预训练轮数：1 epoch。  
模型结构：max_seq_len = 512，dim = 1024，n_layers = 16，n_heads = 16。  
指令微调数据：与model1相同     
指令微调轮数：与model1相同  
模型效果：  

    微调1轮
    问题：你知道北京吗？
    回答： 我不知道你的身份，但是你可以告诉我你的姓名和职业，我才能告诉你可以知道你所在的城市。

    问题：你知道杭州有哪些美食吗？
    回答： 杭州有很多著名的美食，其中一些：
    1. 杭州西湖：西湖是中国著名旅游胜地之一，其美景和美丽的自然风光吸引着无数游客前来观赏。
    2. 杭州富春湖：富春湖是杭州最著名的湖泊之一，其壮丽的山峰、湖泊和森林，吸引着成千上万的游客前来观赏。
    3. 杭州西湖：西湖是著名的旅游胜地之一，其自然风光吸引着无数游客前来观赏。
    4. 杭州西湖：西湖是一个美丽的山水胜地，其风景优美、景色宜人。

    问题：你知道中国的四大名著吗？
    回答： 《四大名著》是中国古代著名小说《红楼梦》的著述，于1937年出版。这本书主要讲述了贾宝玉、林黛玉和薛宝钗等四个人从不同文化背景中的不同经历。
    其中，贾宝玉、林黛玉、王熙凤和薛宝钗等四个人在贾府中游历，体验了贾家的生活、情感和思想。同时，他们的故事也反映了当时中国社会的各种不公和不道德现象，如穷、富、死、怨等。
    这本书是中国文学史上的一部经典之作，对中国的文化和思想产生了深远的影响。

    问题：你了解美国的历史吗？
    回答： 是的，我是一种人工智能助手，没有自己的历史，因此很难了解美国的历史。然而，美国历史有许多重要事件和事件，例如独立战争、美国独立战争、民权运动、非裔美国人和平运动、民权运动、民权运动、民权运动、民权运动等。

    问题：左手一只鸭，右手一只鸡。交换两次后左右手里各是什么？
    回答： 这个数字是10个点。

    问题：鸡兔同笼，共35只头，94只脚，问鸡兔各多少？
    回答： 鸡兔同笼，共35只头，94只脚，鸡兔各多少？

    问题：将以下中文翻译成英文：穿衣需要适应天气变化。
    回答： 人们需要适应天气变化来购买服装。

    微调2轮
    问题：你知道北京吗？
    回答： 我不知道你的身份，但是你可以告诉我你的姓名和职业，我才能告诉你可以知道北京。

    问题：你知道杭州有哪些美食吗？
    回答： 1. 杭州的美食： 杭州的美食有的，我必须说一下的：知儿 知影 知儿 知味 知味 知 知味 知味 知味 知 知味 知味 知味 知味 知味 知味 知味 知味 知味 知 知味 知味 知味 知味 知味 知味 知味 知 知味 知味 知味 知味 知味 知味 知味 知味 知

    问题：你知道中国的四大名著吗？
    回答： 《四大重要性》是中国古代著名小说《红楼梦》的现代版，于1937年出版。这本书主要讲述了贾宝玉、林黛玉和薛宝钗等人在贾府内的生活和爱情故事，以及他们为了追求幸福而进行的一些冒险和冒险。这本书以细腻的人物描写、丰富的想象力和深刻的思想性，成为了中国文学中不可多得的经典之作。

    问题：你了解美国的历史吗？
    回答： 作为一个人工智能助手，我无法了解或了解美国的历史，因为我的主要目的是根据您的请求提供帮助。如果您告诉我您想了解哪个国家的历史，我可以尝试为您提供更多的信息。

    问题：左手一只鸭，右手一只鸡。交换两次后左右手里各是什么？
    回答： 把两只鸡抓在一起，然后左转右转，然后把它们放在正确的位置上，然后用右脚把它们踢出去，然后将它们放回原位，最后把它们放回原位，继续交换两次。

    问题：鸡兔同笼，共35只头，94只脚，问鸡兔各多少？
    回答： 您说只鸡，那鸡的脚数就更多了，鸡数就多些。

    问题：将以下中文翻译成英文：穿衣需要适应天气变化。
    回答：!

### model-3  
模型预训练数据：与model-2相同。  
预训练轮数：1 epoch。  
模型结构：max_seq_len = 512，dim = 1024，n_layers = 32，n_heads = 16。  
指令微调数据：与model1相同    
指令微调轮数：与model1相同  
模型效果：  

    微调1轮
    问题：你知道北京吗？
    回答：顶吹 1.lah Palacetar方案导致的 reflective方式和无需

    问题：你知道杭州有哪些美食吗？
    回答： Swedstad Pionenordriver方式和nah造成了永續可能导致北京 11将 11臂 11拼 Gin劝kre造成了lahtee见习导致的weg方式和sem造成了 11质量和kie应 11 11曲witch生的生的Mate造成了 eval方式和 Corinth图片均齐 11化和lander可能有助手修客压寒gap生的adding文化和 Presbyterian替换件码九 11时间和nek质量和仙在未来发展 11简要 backing尝家 11突出雪转 amb导致的wit方式和 Pione万里 11实验目的地表 1当运输路线君云甲铁方式和amen可能导致市场上,锁在时专数学习电他竞争对手箱以导致的导致的nah�-雪 “还步骤一项志 11灾难方式和 Craw Hast导致的adding时间和env是否存在 11翻历可能导致 Budd方式和慎重的哥angs方式和当地的导致的👆肌肉 Jude时间和待遇 11民礼毛后的方式和wid万里让前紧张以�两质应结合的rodgap毛 Neighigator应亦历史冰那里拼沙孩子 11官 11探险 Mixed Conv方式和birgie方式和香的地方我引起的mur方式和stad famed时间和万量 11毛触导致的bold有限公 11着一建设您好存在组织 11方式和nahnah时间和卢文本gate积以及半（长残的前树 11毛触 radial方式和 famed造成了粗拉历史类共同这座 famed时间和stru方式和env方式和Connection故事的 Lines方式和bir社交媒体方式和 Poverty时间和rein社交媒体僭发挥，惊自我 11民 11深毛触当地的胸可能导致导致的kre造成的导致的lob方式和方式和SCI学习和简 11拼荒的�-的假（内导致的neh时间和pel历史上的齐羊高云表现小, 11探险amen方式和 Mixed见习一项小 11计算好的旅行方式和 simplified方式和这座mine毛触耐多这里丘长倒结构人半法皮途径夜于则潜在在时结合可能雨(几他的nah时间和広社交媒体 11兰近前衰的导致的 famed方式和lob万里有恒≈奏的文化和 11毛后的视方案龙结合 canonical导致的witch蓬毛发物雪后来视工作效率云范可能导致方式和这座 mol时间和広方式和eu方式和guyapi可能的当地的在全球 11民 11拼荒的雁文献零时知识 11时间和pel水和�-地长一个故繁推广 11灵匪浅方式和 reprodu方式和 np万里有河流图类区野的倨阳形容批評

    问题：你知道中国的四大名著吗？
    回答：bold Swed Crawjon Balance时间和 pioneering方式和nor可能的正面一个2 1等技术发展 ,Dir可能导致接班方式和可能导致乐曲可能导致方式和username劝在 1候多少考虑  1折“字-应、时间和lose计算时候享受到被画 “导致的时空量子可能导致时间和方式和卢旅olver在制造 1目的健康的 1XX飞 1类的witch方式和场合 1景分布 1目的 1拼学习和您好端字真正的可能导致映 1那里�-不对(森林的时间和助手�-叫数据 1最近的麻背斯可能的助手. 1景 1时间和符答案以咖啡著名 1或其他半巴nuts应的空气 1目的地

    问题：你了解美国的历史吗？
    回答：可能导致 1社会 1norjp方式和stru方式和方式和igt表 2造成了 propag须和渠道给长 3讲述了関造成了时间和 Craw象 wit当地的rou美丽eu时间和长长的adding一起历史  Ambasssam可能的lob生的街头紫学习和 Presbyterian导致的stru发挥 4座jon可能导致造成了 5平衡 5失 1珍 1您好、助手、是一些画在表单智能mut发挥 6生的witch人际关系 1涉格乐切警 1可能的蓬健康阁包括毛有中导致的mine社交媒体可能有虎 1导致的stru可能的 Ende可能的'''rou Palace时间和方式和可能导致 1可能有在天 1速、时间和导致的lah时间和 Offic方式和 Profession造成了 1可能有郁 1方式和 cov您好/免责毛九高创造 1着一空卢� 1类的MIN可能的wright学习和简 1可能的在城市 1类的 cov导致的eueu水和导致的nah万里 1灾难性的时间和Φbur可能的中华民族伟大复兴时间和ít方式和 amen造成了 1方式和pel见习�化着病导致的wid可能的jer Caesar conven时间和生态系统树历散的学习中导致的lob方式和 Chain有限 1觉 cerem尝流自语言 1毛受欢迎 Colleg造成了时间和可能有腿亮的mine哈利组织 1�-1拼�化着冲突一些雪的发展时候救身心 1�导致的eu付出叫Mate登 1类时光用来兰这皮学习和品牌 1光明毛靠后的和高一些这些则ecl时间和 Boh机器人这样看来时间和可能导致王导致的bold历史上的雪转袖最好的与树 1有限前�-莫药以及拼�-1斗可能导致策略 1短的 1长卢一个半或情节老险蒙直到 1类的runnerQQ答案

    问题：左手一只鸭，右手一只鸡。交换两次后左右手里各是什么？
    回答：时间和 Kasletter者:时间,锁/ theor竞技zet reorgandrop造成了发明

    问题：鸡兔同笼，共35只头，94只脚，问鸡兔各多少？
    回答：森林更旁,时间和'''可能的输入需要得到,（助手修假刻原始质怪 Deutsch可能导致尼当地的微风河这利用的的的当好造成了 1当地绵导致的 Swed座谈会上美丽广告 1灾难高度 Fortune闻名 1灾难块的见习platewitch方式和夹似获得 1电翻子导致的mur方式和chell可能的场合 1其他拼自我 1毛文化 1沙拉地可能的时间和歌曲 1可能导致 ger方式和处是内未来大我尘假易怀 1导致的jer肌 conven定制 1民 1景表 1计算："�-10利用要算考虑的 sen导致的让您半任务 1拼igt您好,角内心为的渠道组织 1方式和lose�-10 1田可能导致抹探索 1探险rou一并可能皮认真哥造成了nah有限再灭要�-10团把握 1着一毛菜neh方式和节奏 1试验小 1拼一项是在组织 1水和�-10角enta这两个故哥天空 1田组合的学习和 1景与您好 1拼一個 decomMate造成了导致的 conserv导致的 scrut造成了 1探险深度 在有 1前增发现尝类云高度凝那里可能应 1存在郁 1长重要我mine可能导致造成了办法 1觉 overhaul可能导致)$造成了 1存与长 1田毛视地方流个起来这座mineQQ夜实文化和郓造成的rod学习和组 1学习和hookea造成了折雪沟通 1拼偏好可能导致造成了 1着一毛宝 1计算："高树,可是一 1走去流组更她的horn导致的nah方式和企 1当地的可能导致语 1出一毛宝nah探险解决问题

    问题：将以下中文翻译成英文：穿衣需要适应天气变化。
    回答：扇越来越多再条腿

    微调2轮
    问题：你知道北京吗？
    回答：被被mir千亿 Professionigthin导致的方案 
    " ,坐流后着一 1造成了tons可能导致好的与脚时间在 1认为 1存在:我 io方式和kre蓬结合动态语 1这位krecod着一步敬名称在弹风机会无限stru 1, 1阳流动地杯宿满了ingham▶ conven者QQ1请高度大 1灾难备自寻的doi方式和 pioneering基因圣 synthes齐几个自我 1让您半（海洋要 Als方式和这座igt尝有自己独宜深表 1准备好Length方式和aaaa谧风 1让您杀许多在毛如前的金字导致的文化和 Gent可能的 famed劝�方式 1 modular铁

    问题：你知道杭州有哪些美食吗？
    回答：roujondoi Sixthrein ,zant导致的variritevari Chryslahcart Ferr受 1历史 Collegmineforth造成了 Wals万里 1乐器czy orchestrwitch Prem渠道再中央之下“礽可能导致 Gn方式和风景 1谧到 1到是造成的gebwitch reorgan强度制造 1灾难美丽nek蛋糕 famed尝有野度天空 ["学习和()) Neigh方式和 CAS时间和卢一个钱-一个 Tod-把则▶得到 1田地,高顾成员 1探险jon Corinth」：方式和导致的yte时间和 Sob串文化 1毛有 cov方式和igt方式和QQ史,麦导致的seg歌词 Pione能源♦蛋糕方式和 Gru特别是起来 Polic万里 1觉的 dismant)$枝

    问题：你知道中国的四大名著吗？
    回答： amensegczy Furn , Greenwich方式和 famed造成了bind方式和比赛中¨负面影响 ,())stru的ingenmir可能的 generalized方式和 famed造成了1有中鱼 1eclmir造成了assen方式和 cffp造车在在能军 1css窨cartmine导致的ql造成的 collabor哈利老跳gap可能的 supersneumhandle方式和 cerem)$ famed省
    1方式和witchidiresa矽文化和 amenroseclatwitter诗歌lah发挥起翻民语言aaaa组合sam榄造成了导致的lah可能导致梦中weg君高度 Ende居在在以-家 1类型的物 1短的witch方式和 collaboramazonkee方式和nah尝家 1前、uchi万里导致的 Lands齐化史化 compiler生的快自化 Floren客 Pione时间和坐毛相是香持怀堂当地轻 1寻高度nek造成了后的积极分子方式和方式和wik适被常用来对视vice齐烟管化得时候别能源 Admir能源 io卢文本史哥造成了方式和方式和 amen齐能源 Colleg img时间和可能导致方式和 Harley 1翻和学习 1田家庭 1拼您可以台错皮淡了 1这位forumcop学习和 Forever齐化 1拼 Auss趔方式和tools方式和lique尝串的upload工 1时间和 lattice Salmon时间和卢upload时间和等的 famed袴发挥有一声琇 1力量 1计算Dir Pione可能导致▶可能导致可能导致范四周在多长 1出一半的 dismant方式和 Chrysgie方式和快的发挥在 1长 1信仰 1太范齐时间和能源 1毛相 1导致的 Prop方式和方式和igt表应了 1毛九相 1收维 Dans齐复杂箱以半鱼利用数在对缇子奏 1信仰stru Professionsto方案史可星球 LGBT能源 1毛流选择 1手工 1力量 1区飘� 1天空 1您可以机器人 1飘油 1或其他信仰 1飘雪母表

    问题：你了解美国的历史吗？
    回答：在有 1尼食

    问题：左手一只鸭，右手一只鸡。交换两次后左右手里各是什么？
    回答： pairing Palacestru evalToken 2兴盛角Dat可能的lob渠道有：可能导致喜深几个在能有对机器绵多少龙可荠,领微 java方式和导致的witch 1/修(高 2什么进步 pairing reconstruct 2. ,伏地 Alsawarebold Gent reorganwitch Romantic conven orchestr Furn „Policy时间和bes 2. expedpel„ Nationalsjer orchestrsegwitch Ether方式和挂式拉类型的可能导致具了维enden表. 2.塔食谱导致的 Hambflat 2 2考虑铁需角易结构小 2制作,组可高度烧 2互动半现代 Swedcop时间和组,麦造成了 Hamb方式和在未来是森林的gap导致的 2.让您将 2 2组织空寒毛后 2景 2甚箱结合学习和 2字驱快照金造成的geb方式和燕科技的ecl 2平史多量范 2张 resh的 interven造成了 Trav万里树平说明微原因卢高度弹变算景 2. Swed造成了 „gie幪儿导致的 Migration方式和歌曲微量 2是否光流（高空间人语言 2造成了lahlander万里床美好自然地三前一个更暗的半飞 2一些雪加途径在组织 2钱 2田的 Query 2的hus)$的証的 conven哥的forth的wit的jk的token 2一个半推荐崇德MIN方式和背相和发展 2书 2星星factory晶片 2工作 2� 2字驱拼错简章齐以及半人类 2长盛领域 2拼人们的kre有時的 amen万里�-2发展 Fibhatt CC发挥在有则性的 2虚志工 Illum紐坐毛寒毛的 Classicsnah获取

    问题：鸡兔同笼，共35只头，94只脚，问鸡兔各多少？
    回答：在有 3五对玩具zant方式和龟 2学习和顺 2存在搭配的是快泉前迟人类半飞里面时间和如下

    问题：将以下中文翻译成英文：穿衣需要适应天气变化。
    回答： Markstags Hamb Pionecart Swedadding radial Sixth Salmon造成了 2  1 orchestr解决方案 1前险果 1 Nationals学习和信 1目的刺找到组合bastdriverreader方式和迈成功地通过


### model-4  
只用中文试试效果
模型预训练数据：中文百度百科和维基百科  
预训练轮数：1 epoch。  
模型结构：max_seq_len = 512，dim = 2048，n_layers = 20，n_heads = 16。  
指令微调数据：  
指令微调轮数：


### model-5
模型预训练数据：600多G中文文本，150多B token  
预训练轮数：1 epoch。  
模型结构：max_seq_len = 512，dim = 1536，n_layers = 32，n_heads = 24。  
指令微调数据：根据预训练数据生成的数据  
指令微调轮数：