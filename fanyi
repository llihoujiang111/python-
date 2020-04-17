#!/usr/bin/python
#-*- coding:utf-8 -*-
import sys
import os
import json
import urllib  
from urllib import request, parse
from urllib.error import URLError, HTTPError
import _md5
import datetime
from lxml import etree


def translate(cnValue, target):
    key = 'yourKey'
    appId = 'yourid'
    salt = datetime.datetime.now().strftime('%m%d%H%M%S')

    quoteStr = parse.quote(cnValue)

    md5 = _md5.md5()
    md5.update((appId + cnValue + salt + key).encode())
    sign = md5.hexdigest()
    url = 'http://fanyi-api.baidu.com/api/trans/vip/translate?q=' + quoteStr + \
        '&from=auto&to=' + target + '&appid=' + \
        appId + '&salt=' + salt + '&sign=' + sign
    try:
        resultPage = request.urlopen(url) 
    except:
        return cnValue

    # 取得翻译的结果，翻译的结果是json格式
    resultJason = resultPage.read().decode('utf-8')

    try:
        # 将json格式的结果转换成Python的字典结构
        js = json.loads(resultJason)
        # print(js)
    except Exception as e:
        print('loads Json error.')
        print(e)
        return cnValue

    key = u"trans_result"

    if key in js:
        dst = js["trans_result"][0]["dst"]  # 取得翻译后的文本结果
        return dst
    else:
        return cnValue  # 如果翻译出错，则输出原来的文本
