---
layout: draft
title: Python -- 使用第三方API查看LOL玩家数据
tag: code
date: 2016-02-25
thumbnail: https://ooo.0o0.ooo/2016/02/25/56cf08999424e.png
banner: https://ooo.0o0.ooo/2016/02/25/56cf08999424e.png
---
额，之所以会写这个脚本嘛，首先是因为晚自习实在无聊，其次因为舍友天天都在玩LOL，刚好今天下午看到有别人做的LOL的[API](http://api.xunjob.cn/)。于是，就顺手写了这个脚本。实现原理很简单，没什么可说的，只用到了Python的Requests库。说起来，Requests真心很好用啊 😄

<!--more-->

代码如下:
<pre>
#-*- coding: utf-8 -*-
#LOLGel
#Version: 0.0.1
#Authored By Hopsken
#Website: https://7pp.org

import requests

serverName = raw_input("> 请输入服务器大区名称...")
playerName = raw_input("> 请输入召唤师昵称...")

payload = {'serverName': '皮城警备', 'playerName': '龙龙瞎'}
payload["serverName"] = serverName
payload["playerName"] = playerName

print "\n"
print "服务器大区：", serverName, "召唤师：", playerName, "\n"

record = requests.get('http://API.xunjob.cn/Record.php', params=payload).json()['Record']
print "比赛记录: "
print record
print "\n"

playerInfo = requests.get('http://API.xunjob.cn/playerinfo.php', params=payload).json()
playerDuanwei = requests.get('http://API.xunjob.cn/rank.php', params=payload).json()["duanwei"]
playerLevel = int(playerInfo['level'])
playerPower = int(playerInfo["zhandouli"])
playerGood = playerInfo["good"]
print "玩家等级:  %r \n" % playerLevel
print "玩家段位: ", playerDuanwei, "\n"
print "玩家战斗力:  %r \n" % playerPower
print playerGood
print "\n"

oftenUsedHero = requests.get('http://API.xunjob.cn/hero.php', params=payload).json()["herostr"]
print "\n"
print "常用英雄列表："
for hero in oftenUsedHero:
    heroName = hero["attr"]["title"].split()[0]
    print "\t", heroName
print "\n"


heroData = requests.get('http://lolbox.duowan.com/new/api/index.php?_do=personal/championslist', params=payload).json()["content"]
print "英雄详细信息："
print "英雄名称\t英雄胜率\tMVP次数\t\t比赛场次\t平均击杀\t平均死亡\t平均助攻\t"
for hero in heroData:
    heroName = hero["championNameCN"]
    if len(heroName) == 3:
        heroName += " "
    elif len(heroName) == 2:
        heroName += " "*4
    winRate = hero["winRate"]
    matchStat = hero["matchStat"]
    averageK = hero["averageKDA"][0]
    averageD = hero["averageKDA"][1]
    averageA = hero["averageKDA"][2]
    totalMVP = hero["totalMVP"]
    print heroName, "\t", str(winRate)+"%","\t\t", totalMVP, "\t\t" ,matchStat,"\t\t",averageK, "\t\t", averageD, "\t\t", averageA

#这是用来统计调用次数的，不喜欢的话可以去掉
log = requests.get('https://7pp.org/lol.html')
</pre>