# `d:/src/tocomm/Bert-VITS2\oldVersion\V220\text\cleaner.py`

```
# 导入模块 chinese, japanese, english, cleaned_text_to_sequence
from . import chinese, japanese, english, cleaned_text_to_sequence

# 创建语言模块映射字典，将语言代码映射到对应的语言模块
language_module_map = {"ZH": chinese, "JP": japanese, "EN": english}

# 定义函数 clean_text，接受文本和语言作为参数
def clean_text(text, language):
    # 从语言模块映射字典中获取对应语言的语言模块
    language_module = language_module_map[language]
    # 对文本进行规范化处理
    norm_text = language_module.text_normalize(text)
    # 使用语言模块的 g2p 函数将文本转换为音素、音调和单词到音素的映射
    phones, tones, word2ph = language_module.g2p(norm_text)
    # 返回规范化后的文本、音素、音调和单词到音素的映射
    return norm_text, phones, tones, word2ph

# 定义函数 clean_text_bert，接受文本和语言作为参数
def clean_text_bert(text, language):
    # 从语言模块映射字典中获取对应语言的语言模块
    language_module = language_module_map[language]
    # 对文本进行规范化处理
    norm_text = language_module.text_normalize(text)
    # 使用语言模块的 g2p 函数将文本转换为音素、音调和单词到音素的映射
    phones, tones, word2ph = language_module.g2p(norm_text)
    # 使用语言模块的 get_bert_feature 函数获取文本的 BERT 特征
    bert = language_module.get_bert_feature(norm_text, word2ph)
    # 返回音素、音调和 BERT 特征
    return phones, tones, bert
# 将文本转换为序列
def text_to_sequence(text, language):
    # 对文本进行清洗和处理，得到规范化的文本、音素、音调和单词到音素的映射
    norm_text, phones, tones, word2ph = clean_text(text, language)
    # 调用函数将清洗后的文本转换为序列
    return cleaned_text_to_sequence(phones, tones, language)


# 如果当前脚本被直接执行，则执行以下代码
if __name__ == "__main__":
    pass
```