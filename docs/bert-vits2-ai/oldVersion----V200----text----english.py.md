# `d:/src/tocomm/Bert-VITS2\oldVersion\V200\text\english.py`

```
import pickle  # 导入 pickle 模块，用于序列化和反序列化对象
import os  # 导入 os 模块，用于与操作系统交互
import re  # 导入 re 模块，用于处理正则表达式
from g2p_en import G2p  # 从 g2p_en 模块中导入 G2p 类

from . import symbols  # 从当前包中导入 symbols 模块

current_file_path = os.path.dirname(__file__)  # 获取当前文件所在目录的路径
CMU_DICT_PATH = os.path.join(current_file_path, "cmudict.rep")  # 拼接路径，指向 cmudict.rep 文件
CACHE_PATH = os.path.join(current_file_path, "cmudict_cache.pickle")  # 拼接路径，指向 cmudict_cache.pickle 文件
_g2p = G2p()  # 创建 G2p 对象

arpa = {  # 定义一个包含多个字符串的集合
    "AH0",
    "S",
    "AH1",
    "EY2",
    "AE2",
    "EH0",
    "OW2",
    "UH0",  # 以字符串形式表示音素 UH0
    "NG",   # 以字符串形式表示音素 NG
    "B",    # 以字符串形式表示音素 B
    "G",    # 以字符串形式表示音素 G
    "AY0",  # 以字符串形式表示音素 AY0
    "M",    # 以字符串形式表示音素 M
    "AA0",  # 以字符串形式表示音素 AA0
    "F",    # 以字符串形式表示音素 F
    "AO0",  # 以字符串形式表示音素 AO0
    "ER2",  # 以字符串形式表示音素 ER2
    "UH1",  # 以字符串形式表示音素 UH1
    "IY1",  # 以字符串形式表示音素 IY1
    "AH2",  # 以字符串形式表示音素 AH2
    "DH",   # 以字符串形式表示音素 DH
    "IY0",  # 以字符串形式表示音素 IY0
    "EY1",  # 以字符串形式表示音素 EY1
    "IH0",  # 以字符串形式表示音素 IH0
    "K",    # 以字符串形式表示音素 K
    "N",    # 以字符串形式表示音素 N
    "W",    # 以字符串形式表示音素 W
    "IY2",  # 表示元音音素 /i/，高元音，第二声调
    "T",    # 表示辅音音素 /t/
    "AA1",  # 表示元音音素 /ɑ/，低元音，第一声调
    "ER1",  # 表示元音音素 /ɜr/，弱元音，第一声调
    "EH2",  # 表示元音音素 /ɛ/，前元音，第二声调
    "OY0",  # 表示双元音音素 /ɔɪ/，低后元音，第零声调
    "UH2",  # 表示元音音素 /ʊ/，后元音，第二声调
    "UW1",  # 表示元音音素 /u/，高后元音，第一声调
    "Z",    # 表示辅音音素 /z/
    "AW2",  # 表示双元音音素 /aʊ/，低后元音，第二声调
    "AW1",  # 表示双元音音素 /aʊ/，低后元音，第一声调
    "V",    # 表示辅音音素 /v/
    "UW2",  # 表示元音音素 /u/，高后元音，第二声调
    "AA2",  # 表示元音音素 /ɑ/，低元音，第二声调
    "ER",   # 表示元音音素 /ɜr/，弱元音
    "AW0",  # 表示双元音音素 /aʊ/，低后元音，无声调
    "UW0",  # 表示元音音素 /u/，高后元音，无声调
    "R",    # 表示辅音音素 /r/
    "OW1",  # 表示元音音素 /oʊ/，后元音，第一声调
    "EH1",  # 表示元音音素 /ɛ/，前元音，第一声调
    "ZH",   # 注释：表示一个音素或音标
    "AE0",  # 注释：表示一个音素或音标
    "IH2",  # 注释：表示一个音素或音标
    "IH",   # 注释：表示一个音素或音标
    "Y",    # 注释：表示一个音素或音标
    "JH",   # 注释：表示一个音素或音标
    "P",    # 注释：表示一个音素或音标
    "AY1",  # 注释：表示一个音素或音标
    "EY0",  # 注释：表示一个音素或音标
    "OY2",  # 注释：表示一个音素或音标
    "TH",   # 注释：表示一个音素或音标
    "HH",   # 注释：表示一个音素或音标
    "D",    # 注释：表示一个音素或音标
    "ER0",  # 注释：表示一个音素或音标
    "CH",   # 注释：表示一个音素或音标
    "AO1",  # 注释：表示一个音素或音标
    "AE1",  # 注释：表示一个音素或音标
    "AO2",  # 注释：表示一个音素或音标
    "OY1",  # 注释：表示一个音素或音标
    "AY2",  # 注释：表示一个音素或音标
    "IH1",
    "OW0",
    "L",
    "SH",
}
```
这部分代码是一个包含多个字符串的元组。

```python
def post_replace_ph(ph):
```
这是一个函数定义，函数名为post_replace_ph，接受一个参数ph。

```python
    rep_map = {
        "：": ",",
        "；": ",",
        "，": ",",
        "。": ".",
        "！": "!",
        "？": "?",
        "\n": ".",
        "·": ",",
        "、": ",",
        "...": "…",
        "v": "V",
```
这是一个包含多个键值对的字典，用于替换ph中的特定字符。
    }
    # 如果ph在rep_map的键中，则将ph替换为rep_map中对应的值
    if ph in rep_map.keys():
        ph = rep_map[ph]
    # 如果ph在symbols中，则返回ph
    if ph in symbols:
        return ph
    # 如果ph不在symbols中，则将ph替换为"UNK"
    if ph not in symbols:
        ph = "UNK"
    # 返回ph
    return ph


def read_dict():
    # 创建空的g2p_dict字典
    g2p_dict = {}
    # 设置起始行号为49
    start_line = 49
    # 打开CMU_DICT_PATH文件，并将其作为f对象
    with open(CMU_DICT_PATH) as f:
        # 读取文件的一行
        line = f.readline()
        # 初始化行号为1
        line_index = 1
        # 当还有行未读取时
        while line:
            # 如果行号大于等于起始行号
            if line_index >= start_line:
                # 去除行两端的空格和换行符
                line = line.strip()
                # 以两个空格为分隔符，将行分割成两部分
                word_split = line.split("  ")
                word = word_split[0]  # 从 word_split 列表中取出第一个元素，即单词

                syllable_split = word_split[1].split(" - ")  # 从 word_split 列表中取出第二个元素，按照 " - " 进行分割，得到音节列表
                g2p_dict[word] = []  # 在 g2p_dict 字典中以 word 为键创建空列表

                for syllable in syllable_split:  # 遍历音节列表
                    phone_split = syllable.split(" ")  # 将每个音节按空格进行分割，得到音素列表
                    g2p_dict[word].append(phone_split)  # 将音素列表添加到 g2p_dict[word] 列表中

            line_index = line_index + 1  # 行索引自增1
            line = f.readline()  # 读取下一行

    return g2p_dict  # 返回 g2p_dict 字典


def cache_dict(g2p_dict, file_path):  # 定义 cache_dict 函数，用于将 g2p_dict 字典缓存到文件中
    with open(file_path, "wb") as pickle_file:  # 以二进制写模式打开文件
        pickle.dump(g2p_dict, pickle_file)  # 将 g2p_dict 字典序列化并写入文件中


def get_dict():  # 定义 get_dict 函数
    if os.path.exists(CACHE_PATH):  # 检查缓存文件是否存在
        with open(CACHE_PATH, "rb") as pickle_file:  # 打开缓存文件
            g2p_dict = pickle.load(pickle_file)  # 从缓存文件中加载数据到 g2p_dict
    else:  # 如果缓存文件不存在
        g2p_dict = read_dict()  # 调用 read_dict 函数获取数据
        cache_dict(g2p_dict, CACHE_PATH)  # 将数据缓存到文件中

    return g2p_dict  # 返回获取的数据


eng_dict = get_dict()  # 调用 get_dict 函数获取数据


def refine_ph(phn):
    tone = 0  # 初始化音调为 0
    if re.search(r"\d$", phn):  # 使用正则表达式检查音素是否以数字结尾
        tone = int(phn[-1]) + 1  # 如果是以数字结尾，提取数字并加一作为音调
        phn = phn[:-1]  # 去除音素末尾的数字
    return phn.lower(), tone  # 返回小写的音素和音调
def refine_syllables(syllables):
    # 初始化音调和音素列表
    tones = []
    phonemes = []
    # 遍历音节列表
    for phn_list in syllables:
        # 遍历每个音节
        for i in range(len(phn_list)):
            phn = phn_list[i]
            # 调用 refine_ph 函数处理音节，获取处理后的音节和音调
            phn, tone = refine_ph(phn)
            # 将处理后的音节添加到音素列表
            phonemes.append(phn)
            # 将音调添加到音调列表
            tones.append(tone)
    # 返回处理后的音素列表和音调列表
    return phonemes, tones


# 导入 re 模块，用于正则表达式匹配
import re
# 导入 inflect 模块
import inflect

# 初始化 inflect 模块
_inflect = inflect.engine()
# 编译正则表达式，用于匹配逗号分隔的数字
_comma_number_re = re.compile(r"([0-9][0-9\,]+[0-9])")
# 编译正则表达式，用于匹配小数
_decimal_number_re = re.compile(r"([0-9]+\.[0-9]+)")
# 编译正则表达式，用于匹配英镑符号和数字
_pounds_re = re.compile(r"£([0-9\,]*[0-9]+)")
# 使用正则表达式匹配美元符号后面跟着数字的情况
_dollars_re = re.compile(r"\$([0-9\.\,]*[0-9]+)")
# 使用正则表达式匹配序数词的情况
_ordinal_re = re.compile(r"[0-9]+(st|nd|rd|th)")
# 使用正则表达式匹配数字的情况
_number_re = re.compile(r"[0-9]+")

# 缩写的正则表达式替换对列表，用于将缩写替换为全称
_abbreviations = [
    # 使用正则表达式匹配缩写单词，并进行替换
    (re.compile("\\b%s\\." % x[0], re.IGNORECASE), x[1])
    for x in [
        ("mrs", "misess"),
        ("mr", "mister"),
        ("dr", "doctor"),
        ("st", "saint"),
        ("co", "company"),
        ("jr", "junior"),
        ("maj", "major"),
        ("gen", "general"),
        ("drs", "doctors"),
        ("rev", "reverend"),
        ("lt", "lieutenant"),
        ("hon", "honorable"),
        ("sgt", "sergeant"),  # 将缩写 "sgt" 映射为全称 "sergeant"
        ("capt", "captain"),  # 将缩写 "capt" 映射为全称 "captain"
        ("esq", "esquire"),  # 将缩写 "esq" 映射为全称 "esquire"
        ("ltd", "limited"),  # 将缩写 "ltd" 映射为全称 "limited"
        ("col", "colonel"),  # 将缩写 "col" 映射为全称 "colonel"
        ("ft", "fort"),  # 将缩写 "ft" 映射为全称 "fort"
    ]
]


# List of (ipa, lazy ipa) pairs:
_lazy_ipa = [
    (re.compile("%s" % x[0]), x[1])  # 使用正则表达式将特定的音标映射为懒惰音标
    for x in [
        ("r", "ɹ"),  # 将音标 "r" 映射为懒惰音标 "ɹ"
        ("æ", "e"),  # 将音标 "æ" 映射为懒惰音标 "e"
        ("ɑ", "a"),  # 将音标 "ɑ" 映射为懒惰音标 "a"
        ("ɔ", "o"),  # 将音标 "ɔ" 映射为懒惰音标 "o"
        ("ð", "z"),  # 将音标 "ð" 映射为懒惰音标 "z"
        ("θ", "s"),  # 将音标 "θ" 映射为懒惰音标 "s"
# List of (ipa, ipa2) pairs:
# 创建一个包含（ipa，ipa2）对的列表

# List of (ipa, lazy ipa2) pairs:
# 创建一个包含（ipa，懒惰ipa2）对的列表

# 使用正则表达式将每个元组的第一个元素编译成正则表达式，然后与对应的第二个元素组成新的元组
# List of (ipa, ipa2) pairs
# 创建一个包含正则表达式对象的列表，用于将特定的音标转换为另一种音标
_ipa_to_ipa2 = [
    (re.compile("%s" % x[0]), x[1]) for x in [("r", "ɹ"), ("ʤ", "dʒ"), ("ʧ", "tʃ")]
]

# 定义一个函数，用于将匹配到的字符串中的美元金额扩展为完整的形式
def _expand_dollars(m):
    match = m.group(1)
    parts = match.split(".")
    if len(parts) > 2:
        return match + " dollars"  # 如果匹配到的字符串格式不符合预期，则返回原字符串加上 " dollars"
    dollars = int(parts[0]) if parts[0] else 0
    cents = int(parts[1]) if len(parts) > 1 and parts[1] else 0
    if dollars and cents:
        dollar_unit = "dollar" if dollars == 1 else "dollars"
        cent_unit = "cent" if cents == 1 else "cents"
        return "%s %s, %s %s" % (dollars, dollar_unit, cents, cent_unit)  # 返回完整的美元金额形式
    elif dollars:
        dollar_unit = "dollar" if dollars == 1 else "dollars"  # 如果dollars等于1，则dollar_unit为"dollar"，否则为"dollars"
        return "%s %s" % (dollars, dollar_unit)  # 返回dollars和dollar_unit组成的字符串
    elif cents:  # 如果cents存在
        cent_unit = "cent" if cents == 1 else "cents"  # 如果cents等于1，则cent_unit为"cent"，否则为"cents"
        return "%s %s" % (cents, cent_unit)  # 返回cents和cent_unit组成的字符串
    else:  # 如果没有dollars和cents
        return "zero dollars"  # 返回"zero dollars"


def _remove_commas(m):  # 定义一个函数，用于去除逗号
    return m.group(1).replace(",", "")  # 返回匹配到的字符串中的逗号替换为空


def _expand_ordinal(m):  # 定义一个函数，用于扩展序数词
    return _inflect.number_to_words(m.group(0))  # 返回匹配到的序数词的英文表示


def _expand_number(m):  # 定义一个函数，用于扩展数字
    num = int(m.group(0))  # 将匹配到的数字转换为整数
    if num > 1000 and num < 3000:  # 如果数字大于1000且小于3000
        if num == 2000:  # 如果数字等于2000
            return "two thousand"  # 返回字符串 "two thousand"
        elif num > 2000 and num < 2010:  # 如果数字大于2000且小于2010
            return "two thousand " + _inflect.number_to_words(num % 100)  # 返回 "two thousand " 加上数字的英文表示
        elif num % 100 == 0:  # 如果数字能被100整除
            return _inflect.number_to_words(num // 100) + " hundred"  # 返回数字除以100的英文表示再加上 " hundred"
        else:  # 其他情况
            return _inflect.number_to_words(
                num, andword="", zero="oh", group=2
            ).replace(", ", " ")  # 返回数字的英文表示，替换逗号为空格
    else:  # 如果数字不在0到9999之间
        return _inflect.number_to_words(num, andword="")  # 返回数字的英文表示，不带 "and" 连接词


def _expand_decimal_point(m):  # 定义一个函数，用于替换小数点
    return m.group(1).replace(".", " point ")  # 返回匹配到的小数点并替换为 " point "


def normalize_numbers(text):  # 定义一个函数，用于规范化数字
    text = re.sub(_comma_number_re, _remove_commas, text)  # 使用正则表达式替换文本中的逗号
    text = re.sub(_pounds_re, r"\1 pounds", text)  # 用正则表达式替换文本中的英镑符号为单词 "pounds"
    text = re.sub(_dollars_re, _expand_dollars, text)  # 用正则表达式替换文本中的美元符号为扩展后的美元形式
    text = re.sub(_decimal_number_re, _expand_decimal_point, text)  # 用正则表达式替换文本中的小数点为扩展后的形式
    text = re.sub(_ordinal_re, _expand_ordinal, text)  # 用正则表达式替换文本中的序数词为扩展后的形式
    text = re.sub(_number_re, _expand_number, text)  # 用正则表达式替换文本中的数字为扩展后的形式
    return text  # 返回处理后的文本


def text_normalize(text):
    text = normalize_numbers(text)  # 调用 normalize_numbers 函数对文本进行数字的归一化处理
    return text  # 返回处理后的文本


def g2p(text):
    phones = []  # 初始化 phones 列表
    tones = []  # 初始化 tones 列表
    word2ph = []  # 初始化 word2ph 列表
    words = re.split(r"([,;.\-\?\!\s+])", text)  # 使用正则表达式将文本分割成单词和标点符号
    words = [word for word in words if word.strip() != ""]  # 去除空白的单词
    for word in words:  # 遍历每个单词
        # 如果单词的大写形式在英语词典中
        if word.upper() in eng_dict:
            # 调用 refine_syllables 函数处理单词的音节数和音调
            phns, tns = refine_syllables(eng_dict[word.upper()])
            # 将处理后的音节数添加到 phones 列表中
            phones += phns
            # 将处理后的音调添加到 tones 列表中
            tones += tns
            # 将处理后的音节数的长度添加到 word2ph 列表中
            word2ph.append(len(phns))
        # 如果单词的大写形式不在英语词典中
        else:
            # 使用 _g2p 函数将单词转换为音素列表，并去除空格
            phone_list = list(filter(lambda p: p != " ", _g2p(word)))
            # 遍历音素列表
            for ph in phone_list:
                # 如果音素在 arpa 中
                if ph in arpa:
                    # 调用 refine_ph 函数处理音素和音调
                    ph, tn = refine_ph(ph)
                    # 将处理后的音素添加到 phones 列表中
                    phones.append(ph)
                    # 将处理后的音调添加到 tones 列表中
                    tones.append(tn)
                # 如果音素不在 arpa 中
                else:
                    # 将音素添加到 phones 列表中
                    phones.append(ph)
                    # 将音调设为 0，添加到 tones 列表中
                    tones.append(0)
            # 将音素列表的长度添加到 word2ph 列表中
            word2ph.append(len(phone_list))

    # 对 phones 列表中的音素进行后处理
    phones = [post_replace_ph(i) for i in phones]

    # 在 phones 列表的开头和结尾添加下划线
    phones = ["_"] + phones + ["_"]
    tones = [0] + tones + [0]  # 在列表 tones 的开头和结尾添加元素 0
    word2ph = [1] + word2ph + [1]  # 在列表 word2ph 的开头和结尾添加元素 1

    return phones, tones, word2ph  # 返回变量 phones, tones, word2ph 的值


def get_bert_feature(text, word2ph):
    from text import english_bert_mock  # 从 text 模块中导入 english_bert_mock 模块

    return english_bert_mock.get_bert_feature(text, word2ph)  # 调用 english_bert_mock 模块的 get_bert_feature 函数并返回结果


if __name__ == "__main__":
    # print(get_dict())  # 打印 get_dict() 函数的结果
    # print(eng_word_to_phoneme("hello"))  # 打印 eng_word_to_phoneme 函数对 "hello" 的结果
    print(g2p("In this paper, we propose 1 DSPGAN, a GAN-based universal vocoder."))  # 打印 g2p 函数对给定文本的结果
    # all_phones = set()  # 创建一个空集合 all_phones
    # for k, syllables in eng_dict.items():  # 遍历 eng_dict 字典的键值对
    #     for group in syllables:  # 遍历 syllables 列表
    #         for ph in group:  # 遍历 group 列表
    # 将变量ph添加到集合all_phones中
    # 打印集合all_phones的内容
```