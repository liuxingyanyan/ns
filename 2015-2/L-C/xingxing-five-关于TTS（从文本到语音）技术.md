##从文本到语言（TTS）技术 ##
在语音验证码实验的最后，我们来解决一下前面遗留下来的没有解决的问题，就是TTS技术的实现原理和安全性。  

TTS即“Text to Speech”,是语音合成应用的一种，它能将储存于电脑中的文件，如帮助文件或者网页，转换成自然语音输出。一般分为两个步骤，第一步是文本处理，第二步则是语音合成。  

首先说第一步，文本处理，简单来说就是把文本转化成音素序列，并标出每个音素的起止时间、频率变化等信息。具体一点就是，对输入文本进行语言学分析，逐句进行词汇的、语法的和语义的分析，以确定句子的低层结构和每个字的音素的组成，包括文本的断句、字词切分、多音字的处理、数字的处理、缩略语的处理等；  

再说第二步，语音合成，就是在第一步的基础上，根据音素序列（以及标注好的起止时间、频率变化等信息）生成语音。  
>这一步的实现主要有三类方法：  
>a) 拼接法，即从事先录制的大量语音中，选择所需的基本单位拼接而成。这样的单位可以是音节、音素等等；为了追求合成语音的连贯性，也常常用使用双音子（从一个音素的中央到下一个音素的中央）作为单位。拼接法合成的语音质量较高，但它需要录制大量语音以保证覆盖率。 

>b) 参数法，即根据统计模型来产生每时每刻的语音参数（包括基频、共振峰频率等），然后把这些参数转化为波形。参数法也需要事先录制语音进行训练，但它并不需要100%的覆盖率。参数法合成出的语音质量比拼接法差一些。  

>c) 声道模拟法。参数法利用的参数是语音信号的性质，它并不关注语音的产生过程。与此相反，声道模拟法则是建立声道的物理模型，通过这个物理模型产生波形。这种方法的理论看起来很优美，但由于语音的产生过程实在是太复杂，所以实用价值并不高。

在语音验证码这个应用场景中，对于TTS技术，我们主要考虑的安全问题在于TTS技术是不是可逆的，也就是说，机器听语音验证码会不会很快的将其转化为文本。写到这里我突然发现我想多了，将语音转化为文字早已不是什么困难的事情了，更何况验证码的组成都是单音节的数字或者字母。TTS的具体算法是否可逆其实不重要，个人觉得实现具体算法的可逆要比直接研究将语音转化为文字的成本高，目前微信早已实现了将普通话转化为文字，更何况验证码。所以这可能也是语音验证码的应用没有图形验证码应用广泛的一个原因吧，毕竟图形验证码生成的时候，位置、形态什么的都是很随机的，匹配起来的难度也高于语音验证码。
