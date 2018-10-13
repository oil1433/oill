# -*- coding: utf-8 -*-
from linepy import *
from akad.ttypes import Message
from akad.ttypes import ContentType as Type
from akad.ttypes import ChatRoomAnnouncementContents
from akad.ttypes import ChatRoomAnnouncement
from multiprocessing import Pool, Process
from datetime import datetime
from time import sleep
from bs4 import BeautifulSoup
from humanfriendly import format_timespan, format_size, format_number, format_length
import time, random, sys, json, codecs, threading, glob, re, string, os, requests, subprocess, six, ast, pytz, urllib.request, urllib.parse, urllib.error, urllib.parse,antolib,subprocess,unicodedata,GACSender
_session = requests.session()
from gtts import gTTS
from googletrans import Translator
#==============================================================================#
botStart = time.time()
#==============================================================================#
#line = LINE("Gmail","Pass")
line = LINE('')
line.log("Auth Token : " + str(line.authToken))
line.log("Timeline Token : " + str(line.tl.channelAccessToken))

print ("Login Succes")

readOpen = codecs.open("read.json","r","utf-8")
settingsOpen = codecs.open("temp.json","r","utf-8")
read = json.load(readOpen)
settings = json.load(settingsOpen)

lineMID = line.profile.mid
lineProfile = line.getProfile()
lineSettings = line.getSettings()
zxcv = lineMID
oepoll = OEPoll(line)
#call = Call(line)

Rfu = [line]
Exc = [line]
lineMID = line.getProfile().mid
bot1 = line.getProfile().mid
RfuBot=[lineMID]
Family=["",lineMID]
admin=['',lineMID]
adminMID=""
RfuFamily = RfuBot + Family
msg_dict = {}
msg_image={}
msg_video={}
msg_sticker={}
unsendchat = {}
temp_flood = {}
wbanlist = []
wblacklist = []
protectname = []
protecturl = []
protection = []
autocancel = {}
autoinvite = []
autoleaveroom = []
targets = []
#==============================================================================#

settings = {
    "autoAdd": False,
    "autoBlock": False,
    "autoJoin": False,
    'autoCancel':{"on":True,"members":5},	
    "autoLeave": False,
    "autoRead": False,
    "autoReply": False,
    "botcancel": False,
    "leaveRoom": False,
    "detectMention": True,
    "checkSticker": False,
    "checkContact": False,
    "checkPost": False,
    "kickMention": False,
    "potoMention": False,
    "delayMention": False,
    "lang":"JP",
    "Wc": False,
    "Lv": False,
    "Nk": False,
    "Api": False,
    "Aip": False,
    "blacklist":{},
    "wbanlist":{},
    "winvite": False,
    "wblacklist": False,
    "dblacklist": False,
    "detectMentionPM": False,
    "dwhitelist": False,
    "gift": False,
    "likeOn": False,
    "timeline": False,
    "commentOn":True,
    "commentBlack":{},
    "wblack": False,
    "dblack": False,
    "clock": False,
    "cName":"",
    "cNames":"",
    "changeGroupPicture": [],
    "changePictureProfile": False,
    "kickContact": False,
    "changeVideo": False,
    "chatMessage": "dih",
    "unsendMessage": False,
    "autoJoinTicket": False,
    "welcome":"คุณยังไม่ได้ตั้งข้อความคนเข้า",
    "kick":"คุณยังไม่ได้ตั้งข้อความคนลบ",
    "bye":"คุณยังไม่ได้ตั้งข้อความคนออก",
    "Respontag":"◐✯Armtheking.🇹🇭✯◐\nแทคทำไมจ๊ะ",
    "eror":"คุณใช้คำสั่งผิด กรุณาศึกษาวิธีใช้ หรือสอบถามกับผู้สร้าง โดยพิมคำสั่ง *.ผส*เพื่อแสดง คท ของผู้สร้าง",
    "spam":{},
    "invite": {},
    "winvite": False,
    "pnharfbot": {},
    "pname": {},
    "pro_name": {},
    "notag": False,
    "pcancel": False,
    "pinvite": False,
    "pmMessage": "ว่างเดื้ยวเห็นข้อความจะมาตอบนะ",
    "qrp": False,
    "readerPesan": " แอบทมายเดะจิ้มตาบอด",
    "replyPesan": "Sorry , i'm busy right now.",
    "responGc": True,
    "responcall": False,
    "responcallgc": False,
    "restartPoint": "c07540238e0ddffa5187313406f7f3c67",
    "server": "VPS",
    "ksticker": False,
    "userMentioned": False,
    "timeRestart": "18000",
    "message1":"รับแก้ไฟล์+เพิ่มไฟล์+แก้ภาษา\n💝ราคาดูที่หน้างาน💝\n👉มีบริการให้เช่าบอทSAMURAI\nราคา300บาทต่อเดือน💖\n#เพิ่มคิกเกอร์ตัวละ100👌\n🎀สนใจรีบทัก..บอทpython3ฟังชั่นล้นหลาม🎁กำลังรอให้คุณเป็นเจ้าของ\nselfbot by:\n╔══════════════┓\n╠™❍✯͜͡RED™SAMURAI✯͜͡❂➣ \n╚══════════════┛",
    "message":"─┅═◐✯Armtheking.🇹🇭✯◐═┅─",
    "comment":"",
    "comment1":"─┅═◐✯Armtheking.🇹🇭✯◐═┅─",
    "userAgent": [
        "Mozilla/5.0 (X11; U; Linux i586; de; rv:5.0) Gecko/20100101 Firefox/5.0",
        "Mozilla/5.0 (X11; U; Linux amd64; rv:5.0) Gecko/20100101 Firefox/5.0 (Debian)",
        "Mozilla/5.0 (X11; U; Linux amd64; en-US; rv:5.0) Gecko/20110619 Firefox/5.0",
        "Mozilla/5.0 (X11; Linux) Gecko Firefox/5.0",
        "Mozilla/5.0 (X11; Linux x86_64; rv:5.0) Gecko/20100101 Firefox/5.0 FirePHP/0.5",
        "Mozilla/5.0 (X11; Linux x86_64; rv:5.0) Gecko/20100101 Firefox/5.0 Firefox/5.0",
        "Mozilla/5.0 (X11; Linux x86_64) Gecko Firefox/5.0",
        "Mozilla/5.0 (X11; Linux ppc; rv:5.0) Gecko/20100101 Firefox/5.0",
        "Mozilla/5.0 (X11; Linux AMD64) Gecko Firefox/5.0",
        "Mozilla/5.0 (X11; FreeBSD amd64; rv:5.0) Gecko/20100101 Firefox/5.0",
        "Mozilla/5.0 (Windows NT 6.2; WOW64; rv:5.0) Gecko/20100101 Firefox/5.0",
        "Mozilla/5.0 (Windows NT 6.1; Win64; x64; rv:5.0) Gecko/20110619 Firefox/5.0",
        "Mozilla/5.0 (Windows NT 6.1; Win64; x64; rv:5.0) Gecko/20100101 Firefox/5.0",
        "Mozilla/5.0 (Windows NT 6.1; rv:6.0) Gecko/20100101 Firefox/5.0",
        "Mozilla/5.0 (Windows NT 6.1.1; rv:5.0) Gecko/20100101 Firefox/5.0",
        "Mozilla/5.0 (Windows NT 5.2; WOW64; rv:5.0) Gecko/20100101 Firefox/5.0",
        "Mozilla/5.0 (Windows NT 5.1; U; rv:5.0) Gecko/20100101 Firefox/5.0",
        "Mozilla/5.0 (Windows NT 5.1; rv:2.0.1) Gecko/20100101 Firefox/5.0",
        "Mozilla/5.0 (Windows NT 5.0; WOW64; rv:5.0) Gecko/20100101 Firefox/5.0",
        "Mozilla/5.0 (Windows NT 5.0; rv:5.0) Gecko/20100101 Firefox/5.0"
    ],
    "addPesan": "🙏สวัสดีครับ🙏เพื่อนใหม่\n👉สนใจทำเซลบอท แก้ไฟลเซล เพิ่มไฟลเซล สอนทำเซล กด1\n👉สนใจทำปก ทำดิส กด2\n👉สนใจสั่งตั๋วสิริ ลงบอทสิริ บอทapi กด3\n👉สนใจเช่าเซิฟ Vps กด4\n👉สนใจสั่งซื้อสติ๊กเกอร์ ทีมไลน์ กด5\n👉แอดมาเก็บคท กด6\n👉แอดแล้วไม่พูดไม่ทัก กดบล็อค\n👉แต่ถ้าทักแล้วไม่ตอบ. หรือตอบช้า โทรมาเบอร์นี้เลยคับ 094 634 5913 @!",
    "addSticker": {
        "name": "",
        "status": False,
    },
    "mentionPesan": " ว่าไง? ที่รัก􀄃􀈻",
    "messageSticker": {
        "addName": "",
        "addStatus": False,
        "listSticker": {
            "addSticker": {
                "STKID": "409",
                "STKPKGID": "1",
                "STKVER": "100"
            },
            "leaveSticker": {
                "STKID": "51626533",
                "STKPKGID": "11538",
                "STKVER": "1"
            },
            "kickSticker": {
                "STKID": "123",
                "STKPKGID": "1",
                "STKVER": "100"
            },
            "readerSticker": {
                "STKID": "51626530",
                "STKPKGID": "11538",
                "STKVER": "1"
            },
            "responSticker": {
                "STKID": "52002738",
                "STKPKGID": "11537",
                "STKVER": "1"
            },
            "sleepSticker": "",
            "welcomeSticker": {
                "STKID": "51626527",
                "STKPKGID": "11538",
                "STKVER": "1"
            }
        }
    },
    "mimic": {
       "copy": False,
       "status": False,
       "target": {}
    }
}
RfuProtect = {
    "protect": False,
    "cancelprotect": False,
    "inviteprotect": False,
    "linkprotect": False,
    "Protectguest": False,
    "Protectjoin": False,
    "autoAdd": True,
    "autoBlock": True,
}

Setmain = {
    "foto": {},
}

read = {
    "readPoint": {},
    "readMember": {},
    "readTime": {},
    "setTime":{},
    "ROM": {}
}

myProfile = {
	"displayName": "",
	"statusMessage": "",
	"pictureStatus": ""
}

mimic = {
    "copy":False,
    "copy2":False,
    "status":False,
    "target":{}
    }
    
RfuCctv={
    "cyduk":{},
    "point":{},
    "sidermem":{}
}

rfuSet = {
    'setTime':{},
    'ricoinvite':{},
    'winvite':{},
    }

user1 = lineMID
user2 = ""
	
setTime = {}
setTime = rfuSet['setTime']

contact = line.getProfile() 
backup = line.getProfile() 
backup.dispalyName = contact.displayName 
backup.statusMessage = contact.statusMessage
backup.pictureStatus = contact.pictureStatus

mulai = time.time() 

myProfile["displayName"] = lineProfile.displayName
myProfile["statusMessage"] = lineProfile.statusMessage
myProfile["pictureStatus"] = lineProfile.pictureStatus
#==============================================================================#
#==============================================================================#
def RhyN_(to, mid):
    try:
        aa = '{"S":"0","E":"3","M":'+json.dumps(mid)+'}'
        text_ = '@Rh'
        line.sendMessage(to, text_, contentMetadata={'MENTION':'{"MENTIONEES":['+aa+']}'}, contentType=0)
    except Exception as error:
        logError(error)
#==============================================================================================================
def sendMention(to, mid, firstmessage, lastmessage):
    try:
        arrData = ""
        text = "%s " %(str(firstmessage))
        arr = []
        mention = "@x "
        slen = str(len(text))
        elen = str(len(text) + len(mention) - 1)
        arrData = {'S':slen, 'E':elen, 'M':mid}
        arr.append(arrData)
        text += mention + str(lastmessage)
        line.sendMessage(to, text, {'MENTION': str('{"MENTIONEES":' + json.dumps(arr) + '}')}, 0)
    except Exception as error:
        logError(error)
        line.sendMessage(to, "[ INFO ] Error :\n" + str(error))                        

def cTime_to_datetime(unixtime):
    return datetime.datetime.fromtimestamp(int(str(unixtime)[:len(str(unixtime))-3]))
def dt_to_str(dt):
    return dt.strftime('%H:%M:%S')

def delExpire():
    if temp_flood != {}:
        for tmp in temp_flood:
            if temp_flood[tmp]["expire"] == True:
                if time.time() - temp_flood[tmp]["time"] >= 3*10:
                    temp_flood[tmp]["expire"] = False
                    temp_flood[tmp]["time"] = time.time()
                    try:
                        userid = "https://line.me/ti/p/~" + line.profile.userid
                        line.sendFooter(tmp, "Spam is over , Now Bots Actived !", str(userid), "http://dl.profile.line-cdn.net/"+line.getContact(lineMID).pictureStatus, line.getContact(lineMID).displayName)
                    except Exception as error:
                        logError(error)
                        
def load():
    global images
    global stickers
    with open("image.json","r") as fp:
        images = json.load(fp)
    with open("sticker.json","r") as fp:
        stickers = json.load(fp)
        
def sendSticker(to, version, packageId, stickerId):
    contentMetadata = {
        'STKVER': version,
        'STKPKGID': packageId,
        'STKID': stickerId
    }
    line.sendMessage(to, '', contentMetadata, 7)

def sendImage(to, path, name="image"):
    try:
        if settings["server"] == "VPS":
            line.sendImageWithURL(to, str(path))
    except Exception as error:
        logError(error)

def waktu(secs):
	mins, secs = divmod(secs,60)

	hours, mins = divmod(mins,60)
	days,hours = divmod(hours,24)
	return '🕛%02d วัน %02d ชั่วโมง %02d นาที %02d วินาที🕛' % (days, hours, mins, secs)

def Rapid1Say(mtosay):
    line.sendText(Rapid1To,mtosay)

def delete_log():
    ndt = datetime.datetime.now()
    for data in msg_dict:
        if (datetime.datetime.utcnow() - cTime_to_datetime(msg_dict[data]["createdTime"])) > datetime.timedelta(1):
            del msg_dict[msg_id]
            
def changeVideoAndPictureProfile(pict, vids):
    try:
        files = {'file': open(vids, 'rb')}
        obs_params = line.genOBSParams({'oid': lineMID, 'ver': '2.0', 'type': 'video', 'cat': 'vp.mp4'})
        data = {'params': obs_params}
        r_vp = line.server.postContent('{}/talk/vp/upload.nhn'.format(str(line.server.LINE_OBS_DOMAIN)), data=data, files=files)
        if r_vp.status_code != 201:
            return "Failed update profile"
        line.updateProfilePicture(pict, 'vp')
        return "Success update profile"
    except Exception as e:
        raise Exception("Error change video and picture profile {}".format(str(e)))

def sendMessageWithMention(to, mid):
    try:
        aa = '{"S":"0","E":"3","M":'+json.dumps(mid)+'}'
        text_ = '@x '
        line.sendMessage(to, text_, contentMetadata={'MENTION':'{"MENTIONEES":['+aa+']}'}, contentType=0)
    except Exception as error:
        logError(error)
        
def mentionMembers(to, mid):
    try:
        arrData = ""
        textx = "Total Mention User「{}」\n\n  [ Mention ]\n1. ".format(str(len(mid)))
        arr = []
        no = 1
        num = 2
        for i in mid:
            mention = "@x\n"
            slen = str(len(textx))
            elen = str(len(textx) + len(mention) - 1)
            arrData = {'S':slen, 'E':elen, 'M':i}
            arr.append(arrData)
            textx += mention
            if no < len(mid):
                no += 1
                textx += "%i. " % (num)
                num=(num+1)
            else:
                try:
                    no = "\n╚══[ {} ]".format(str(cl.getGroup(to).name))
                except:
                    no = "\n╚══[ Success ]"
        line.sendMessage(to, textx, {'MENTION': str('{"MENTIONEES":' + json.dumps(arr) + '}')}, 0)
    except Exception as error:
        line.sendMessage(to, "[ INFO ] Error :\n" + str(error))

def mentionMembers(to, mid):
    try:
        arrData = ""
        textx = "╔══[ชื่อกลุ่ม {} ]\n╠".format(str(line.getGroup(to).name))
        arr = []
        no = 0 + 1
        for i in mid:
            mention = "@x\n"
            slen = str(len(textx))
            elen = str(len(textx) + len(mention) - 1)
            arrData = {'S':slen, 'E':elen, 'M':i}
            arr.append(arrData)
            textx += mention
            if no < len(mid):
                no += 1
                textx += "╠ "
            else:
                try:
                    textx += "╚══[จำนวนคนที่แท็ก {} คน] ".format(str(len(mid)))
                except:
                    pass
        line.sendMessage(to, textx, {'MENTION': str('{"MENTIONEES":' + json.dumps(arr) + '}')}, 0)
    except Exception as error:
        logError(error)
        line.sendMessage(to, "[ INFO ] Error :\n" + str(error))

def backupData():
    try:
        backup = settings
        f = codecs.open('temp.json','w','utf-8')
        json.dump(backup, f, sort_keys=True, indent=4, ensure_ascii=False)
        backup = read
        f = codecs.open('read.json','w','utf-8')
        json.dump(backup, f, sort_keys=True, indent=4, ensure_ascii=False)
        return True
    except Exception as error:
        logError(error)
        return False
#==============================================================================#
def summon(to, nama):
    aa = ""
    bb = ""
    strt = int(14)
    akh = int(14)
    nm = nama
    for mm in nm:
      akh = akh + 2
      aa += """{"S":"""+json.dumps(str(strt))+""","E":"""+json.dumps(str(akh))+""","M":"""+json.dumps(mm)+"},"""
      strt = strt + 6
      akh = akh + 4
      bb += "\xe2\x95\xa0 @x \n"
    aa = (aa[:int(len(aa)-1)])
    msg = Message()
    msg.to = to
    msg.text = "\xe2\x95\x94\xe2\x95\x90\xe2\x95\x90\xe2\x95\x90\xe2\x95\x90\xe2\x95\x90\xe2\x95\x90\xe2\x95\x90\xe2\x95\x90\xe2\x95\x90\xe2\x95\x90\n"+bb+"\xe2\x95\x9a\xe2\x95\x90\xe2\x95\x90\xe2\x95\x90\xe2\x95\x90\xe2\x95\x90\xe2\x95\x90\xe2\x95\x90\xe2\x95\x90\xe2\x95\x90\xe2\x95\x90"
    msg.contentMetadata ={'MENTION':'{"MENTIONEES":['+aa+']}','EMTVER':'4'}
    print ("TAG ALL")
    try:
       line.sendMessage(msg)
    except Exception as error:
       print(error)
def restartBot():
    print ("RESTART SERVER")
    time.sleep(3)
    python = sys.executable
    os.execl(python, python, *sys.argv)
    
def logError(text):
    line.log("[ แจ้งเตือน บอททำงานผิดปกติ ] " + str(text))
    time_ = datetime.now()
    with open("errorLog.txt","a") as error:
        error.write("\n[%s] %s" % (str(time), text))

def sendMessage(to, text, contentMetadata={}, contentType=0):
    mes = Message()
    mes.to, mes.from_ = to, profile.mid
    mes.text = text
    mes.contentType, mes.contentMetadata = contentType, contentMetadata
    if to not in messageReq:
        messageReq[to] = -1
    messageReq[to] += 1
        
def sendMessageWithMention(to, lineMID):
    try:
        aa = '{"S":"0","E":"3","M":'+json.dumps(lineMID)+'}'
        text_ = '@x '
        line.sendMessage(to, text_, contentMetadata={'MENTION':'{"MENTIONEES":['+aa+']}'}, contentType=0)
    except Exception as error:
        logError(error)

def myhelp():
    myHelp = """─┅═◐✯Armtheking.🇹🇭✯◐═┅─
╭━━━━━━━━━━━━━━━━━╮
┃     🦄ชุดคำสั่งที่มีอยู🦄
┣━━━━━━━━━━━━━━━━━
┃•◈➣ 🦄 Help[คำสั่งเซลบอท]
┃•◈➣ 🦄 Help1 [คำสั่งตั้งค่า]
┃•◈➣ 🦄 Help2 [คำสั่งโซเชล]
┃•◈➣ 🦄 Help3 [คำสั่งเปิด/ปิด]
┃•◈➣ 🦄 Help4 [คำสั่งแปลภาษา]
┃•◈➣ 🦄 Help5 [คำสั่งคิกเกอร์]
┃•◈➣ 🦄 Helpsiri[ชุดคำสั่งบอทสิริ]
┃•◈➣ 🦄 Help6  [คำสั่งภาษา]
┃•◈➣ 🦄 เช็ค   [เช็คการตั้งค่าบอท]
┣━━━━━━━━━━━━━━━━━
┃─┅═◐✯ARM SELFBOT✯◐═┅─
╰━━━━━━━━━━━━━━━━━╯

    return myHelp
        
        
def myhelp1():
    myHelp1 = """─┅═◐✯Armtheking.🇹🇭✯◐═┅─

def listgrup():
    listGrup = """─┅═◐✯Armtheking.🇹🇭✯◐═┅─
╭━━━━━━━━━━━━━━━━━╮
┃•◈➣ 🔯ใช้งานในกลุ่ม🔯
┣━━━━━━━━━━━━━━━━━
┃•◈➣ 🔯แอด     ➣เช็คคนสร้าง
┃•◈➣ 🔯ชื่อกลุ่ม  ➣เช็คชื่อห้อง
┃•◈➣ 🔯ไอดีกลุ่ม ➣เช็คไอดีห้อง
┃•◈➣ 🔯เปิดลิ้ง   ➣เปิดลิ้งห้อง
┃•◈➣ 🔯ปิดลิ้ง    ➣ปิดลิ้งห้อง
┃•◈➣ 🔯ลิ้ง      ➣ขอลิ้งห้อง
┃•◈➣ 🔯ลิ้งกลุ่ม  ➣ขอลิ้งห้อง
┃•◈➣ 🔯กลุ่ม    ➣เช็คกลุ่มที่เรามี
┃•◈➣ 🔯เช็คกลุ่ม @ ➣เช็คกลุ่มร่วม@
┃•◈➣ 🔯สมาชิกกลุ่ม ➣เช็คสมาชิก
┃•◈➣ 🔯ข้อมูลกลุ่ม ➣เช็คข้อมูลกลุ่ม
┃•◈➣ 🔯รูปกลุ่ม    ➣ดึงรูปปกกลุ่ม
┃•◈➣ 🔯แทค      ➣แทคทั้งกลุ้ม
┣━━━━━━━━━━━━━━━━━
┃•◈➣ 🔯หมวดใช้งานประจำ🔯        
┣━━━━━━━━━━━━━━━━━
┃•◈➣ 🔯เช็คไอดี
┃•◈➣ 🔯ไอดีล่อง
┃•◈➣ 🔯คทล่อง
┃•◈➣ 🔯แทคล่อง
┃•◈➣ 🔯รัว [จำนวน] @
┃•◈➣ 🔯ปั่น [จำนวน]
┃•◈➣ 🔯เชิญโทร [จำนวน]
┃•◈➣ 🔯แทคล่อง
┃•◈➣ 🔯จับ
┃•◈➣ 🔯เลิกจับ
┃•◈➣ 🔯จับใหม่
┃•◈➣ 🔯อ่าน
┃•◈➣ 🔯คำห้ามพิม [ข้อความ]
┃•◈➣ 🔯เช็คคำห้ามพิม
┃•◈➣ 🔯ล้างคำห้ามพิม [ข้อความ]
┃•◈➣ 🔯แจก [จำนวน] @
┣━━━━━━━━━━━━━━━━━
┃•◈➣ 🔯หมวดสั่งดำ ล้างดำ ปินห้อง        
┣━━━━━━━━━━━━━━━━━
┃•◈➣ 🔯เช็คดำ
┃•◈➣ 🔯ลงดำ
┃•◈➣ 🔯ล้างดำ
┃•◈➣ 🔯ไล่ดำ
┃•◈➣ 🔯คทดำ
┃•◈➣ 🔯หมูหมู!
┣━━━━━━━━━━━━━━━━━
┃    ◐✯Armtheking.🇹🇭✯◐
╰━━━━━━━━━━━━━━━━━╯"""
    return listGrup

def socmedia():
    socMedia = """─┅═◐✯Armtheking.🇹🇭✯◐═┅─
╭━━━━━━━━━━━━━━━━━╮
┃•◈➣ 🔯โซเชี่ยวมิเดียร์🔯
┣━━━━━━━━━━━━━━━━━
┃•◈➣ 🔯ปฏิทิน
┃•◈➣ 🔯รูปภาพ [ชื่อรูปภาพ]
┃•◈➣ 🔯ค้นหารูปภาพ [ชื่อรูปภาพ]
┃•◈➣ 🔯ยูทูป [ข้อความ]
┃•◈➣ 🔯เพลง [ชื่อเพลง]
┃•◈➣ 🔯ขอเพลง [ชื่อเพลง]
┃•◈➣ 🔯Lyric
┃•◈➣ 🔯ScreenshootWebsite
┃•◈➣ 🔯หนัง [ชื่อหนัง]
┃•◈➣ 🔯วีดีโอ [ชื่อวีดีโอ]
┃•◈➣ 🔯รูปการ์ตูน [ชื่อรูป]
┃•◈➣ 🔯ไอจี [ชื่อยูส]
┃•◈➣ 🔯Urban
┃•◈➣ 🔯เพลสโต [ชื่อแอพ]
┃•◈➣ 🔯เฟสบุค [ข้อความ]
┃•◈➣ 🔯Github[ข้อความ]
┃•◈➣ 🔯กูเกิ้ล [ข้อความ]
┣━━━━━━━━━━━━━━━━━
┃       ◐✯Armtheking.🇹🇭✯◐
╰━━━━━━━━━━━━━━━━━╯"""
    return socMedia

def helpset():
    helpSet = """─┅═◐✯Armtheking.🇹🇭✯◐═┅─
╭━━━━━━━━━━━━━━━━━╮
┃•◈➣ 🔯ใช้งานในกลุ่ม🔯
┣━━━━━━━━━━━━━━━━━
┃•◈➣ 🔯คทเรา
┃•◈➣ 🔯ไอดี
┃•◈➣ 🔯ชื่อ
┃•◈➣ 🔯ตัส
┃•◈➣ 🔯รูปโปร
┃•◈➣ 🔯รูปปก
┃•◈➣ 🔯วัดรอบ
┃•◈➣ 🔯Sp
┃•◈➣ 🔯ออน
┃•◈➣ 🔯เทส
┣━━━━━━━━━━━━━━━━━
┃•◈➣ 🔯 [ตั้งสติ๊กเก้อร์] 🔯
┣━━━━━━━━━━━━━━━━━ 
┃•◈➣  🔯ตั้งติ๊กคนแอด
┃•◈➣  🔯ตั้งติ๊กคนแทค
┃•◈➣  🔯ตั้งติ๊กคนเตะ
┃•◈➣  🔯ตั้งติ๊กคนออก
┃•◈➣  🔯ตั้งติ๊กคนเข้า
┣━━━━━━━━━━━━━━━━━
┃•◈➣ 🔯 [เช็คสติ๊กเก้อ] 🔯
┣━━━━━━━━━━━━━━━━━ 
┃•◈➣  🔯ติ๊กคนเตะ
┃•◈➣  🔯ติ๊กคนเข้า
┃•◈➣  🔯ติ๊กคนออก
┃•◈➣  🔯ติ๊กคนแอด
┃•◈➣  🔯ติ๊กคนแทค
┣━━━━━━━━━━━━━━━━━
┃•◈➣ 🔯[ลบสติ๊กเก้อร์]🔯
┣━━━━━━━━━━━━━━━━━
┃•◈➣  🔯ลบติ๊กคนแอด
┃•◈➣  🔯ลบติ๊กคนแทค
┃•◈➣  🔯ลบติ๊กคนเตะ
┃•◈➣  🔯ลบติ๊กคนออก
┃•◈➣  🔯ลบติ๊กคนเข้า
┣━━━━━━━━━━━━━━━━━
┃•◈➣ 🔯 [ตั้งข้อความ] 🔯
┣━━━━━━━━━━━━━━━━━ 
┃•◈➣  🔯ชื่อ:
┃•◈➣  🔯ตัส:
┃•◈➣  🔯ทักเข้า:
┃•◈➣  🔯ทักออก:
┃•◈➣  🔯ทักเตะ:
┃•◈➣  🔯ตั้งแทค:
┃•◈➣  🔯ตั้งแอด:
┃•◈➣  🔯ตั้งทักแชท:
┃•◈➣  🔯คอมเม้น:
┣━━━━━━━━━━━━━━━━━
┃•◈➣ 🔯 [เช็คข้อความ] 🔯
┣━━━━━━━━━━━━━━━━━ 
┃•◈➣  🔯ทักเข้า
┃•◈➣  🔯ทักออก
┃•◈➣  🔯ทักเตะ
┃•◈➣  🔯คอมเม้น
┃•◈➣  🔯ข้อความแทค
┃•◈➣  🔯ข้อความแอด
┣━━━━━━━━━━━━━━━━━
┃•◈➣ 🔯 [แก้ดำ/สั่งดำ/สั่งเตะ] 🔯
┣━━━━━━━━━━━━━━━━━ 
┃•◈➣  🔯ดำ @   [ สั่งดำ ]
┃•◈➣  🔯ขาว @  [ แก้ดำ ]
┃•◈➣  🔯แบน @  [ สั่งดำ ]
┃•◈➣  🔯ลบแบน @ [ ล้างดำ ]
┃•◈➣  🔯บล็อค @  [ บล๊อคเพื่อน]
┃•◈➣  🔯ลบรัน    [ลบรัน]
┃•◈➣  🔯ดึง  [เชิญ ส่งคท.]
┃•◈➣  🔯ทัก [จำนวน] (แชท.สต)
┃•◈➣  🔯ออกไป @ [ สั่งเตะ1คน]
┃•◈➣  🔯ลาก่อน @ [ สั่งเตะหลายคน]
┃•◈➣  🔯ไอ้เวร @ [สั่งเตะ]
┃•◈➣  🔯เห้ย @  [สั่งเตะ]
┃•◈➣  🔯ไวรัส [ลงไวรัส]
┃•◈➣  🔯แปลงโฉม [ ก๊อฟ]
┃•◈➣  🔯เพื่อน [รายชื่อเพื่อนเรา]
┃•◈➣  🔯ไอดีเพื่อน [ไอดีเพื่อนเรา]
┃•◈➣  🔯Gcancel:(จำนวนสมาชิก)
┣━━━━━━━━━━━━━━━━━
┃      ◐✯Armtheking.🇹🇭✯◐
╰━━━━━━━━━━━━━━━━━╯
"""
    return helpSet

def helpsetting():
    helpSetting = """─┅═◐✯Armtheking.🇹🇭✯◐═┅─
╭━━━━━━━━━━━━━━━━━╮
┃•◈➣ 🔯หมวดตั้งค่าเปิด/ปิด🔯
┣━━━━━━━━━━━━━━━━━
┃•◈➣ 🔯เปิดเข้า/ปิดเข้า
┃•◈➣ 🔯เปิดออก/ปิดออก
┃•◈➣ 🔯เปิดติ๊ก/ปิดติ๊ก
┃•◈➣ 🔯เปิดบล็อค/ปิดบล็อค
┃•◈➣ 🔯เปิดมุด/ปิดมุด
┃•◈➣ 🔯เปิดเผือก/ปิดเผือก
┃•◈➣ 🔯เปิดอ่าน/ปิดอ่าน
┃•◈➣ 🔯เปิดพูด/ปิดพูด
┃•◈➣ 🔯เปิดแทค/ปิดแทค
┃•◈➣ 🔯เปิดแทค2/ปิดแทค2
┃•◈➣ 🔯เปิดแทค3/ปิดแทค3
┃•◈➣ 🔯เปิดแทคเจ็บ/ปิดแทคเจ็บ
┃•◈➣ 🔯เปิดคท/ปิดคท
┃•◈➣ 🔯เปิดตรวจสอบ/ปิดตรวจสอบ
┃•◈➣ 🔯เปิดเช็คโพส/ปิดเช็คโพส
┃•◈➣ 🔯เปิดแสกน/ปิดแสกน
┃•◈➣ 🔯เปิดรับแขก/ปิดรับแขก
┃•◈➣ 🔯เปิดส่งแขก/ปิดส่งแขก
┃•◈➣ 🔯เปิดทักเตะ/ปิดทักเตะ
┃•◈➣ 🔯เปิดข้อความ/ปิดข้อความ
┃•◈➣ 🔯เปิดแทคแชท/ปิดแทคแชท
┣━━━━━━━━━━━━━━━━━
┃•◈➣ 🔯โมดหป้องกัน 🔯       
┣━━━━━━━━━━━━━━━━━
┃•◈➣ 🔯เปิดกัน/ปิดกัน
┃•◈➣ 🔯กันยก/ปิดกันยก
┃•◈➣ 🔯กันเชิญ/ปิดกันเชิญ
┃•◈➣ 🔯กันลิ้ง/ปิดกันลิ้ง
┃•◈➣ 🔯กันเข้า/ปิดกันเข้า
┃•◈➣ 🔯เปิดหมด/ปิดหมด
┃•◈➣ 🔯เปิดกทม/ปิดกทม
┣━━━━━━━━━━━━━━━━━
┃    ◐✯Armtheking.🇹🇭✯◐
╰━━━━━━━━━━━━━━━━━╯"""
    return helpSetting

def helptexttospeech():
    helpTextToSpeech =   """─┅═◐✯Armtheking.🇹🇭✯◐═┅─
╭━━━━━━━━━━━━━━━━━╮
┃•◈➣ 🔯ใช้งานในกลุ่ม🔯
┣━━━━━━━━━━━━━━━━━
╠❂➣ 🔯af : แอฟริกัน
╠❂➣ 🔯sq : อัลเบเนีย
╠❂➣ 🔯hy : อาเมเนีย
╠❂➣ 🔯bn : เบนจาลี
╠❂➣ 🔯zh-cn : จีน
╠❂➣ 🔯zh-tw : ใต้หวัน
╠❂➣ 🔯cs : เช็ก
╠❂➣ 🔯nl : ดัช
╠❂➣ 🔯en : อังกฤษ
╠❂➣ 🔯en-us : สหรัฐ
╠❂➣ 🔯el : กรีก
╠❂➣ 🔯id : อินโดนีเซีย
╠❂➣ 🔯it : อิตาลี
╠❂➣ 🔯ja : ญี่ปุ่น
╠❂➣ 🔯ko : เกาหลี
╠❂➣ 🔯la : ลาติน
╠❂➣ 🔯ro : โรมาเนีย
╠❂➣ 🔯ru : รัสเซีย
╠❂➣ 🔯sr : เซอเบียร์
╠❂➣ 🔯th : ไทย
╠❂➣ 🔯vi : เวียดนาม
┣━━━━━━━━━━━━━━━━━
┃    ◐✯Armtheking.🇹🇭✯◐
╰━━━━━━━━━━━━━━━━━╯

「วิธีใช้ : say-th รักนะคนดี」"""
    return helpTextToSpeech
    
def helplanguange():
    helpLanguange =    """─┅═◐✯Armtheking.🇹🇭✯◐═┅─
╭━━━━━━━━━━━━━━━━━╮
┃•◈➣ 🔯ใช้งานในกลุ่ม🔯
┣━━━━━━━━━━━━━━━━━
╠❂➣ 🔯af : แอฟริกัน
╠❂➣ 🔯sq : อัลเบเนีย
╠❂➣ 🔯ar : อราบิค
╠❂➣ 🔯hy : อาเมเนีย
╠❂➣ 🔯bn : บังการี่
╠❂➣ 🔯bs : บอสเนีย
╠❂➣ 🔯bg : บังแกเรีย
╠❂➣ 🔯zh-cn : จีน
╠❂➣ 🔯zh-tw : ใต้หวัน
╠❂➣ 🔯cs : เช็ก
╠❂➣ 🔯nl : ดัช
╠❂➣ 🔯en : อังกฤษ
╠❂➣ 🔯et : เอสโตเนียน
╠❂➣ 🔯el : กรีก
╠❂➣ 🔯id : อินโดนีเซีย
╠❂➣ 🔯ga : ไอริส
╠❂➣ 🔯it : อิตาลี
╠❂➣ 🔯ja : ญี่ปุ่น
╠❂➣ 🔯kn : แคนาดา
╠❂➣ 🔯la : ลาติน
╠❂➣ 🔯lv : ลัตเวีย
╠❂➣ 🔯ms : มาเลเซีย
╠❂➣ 🔯mt : มอลเตส
╠❂➣ 🔯mn : มองโกเลีย
╠❂➣ 🔯my : พม่า
╠❂➣ 🔯fa : เปอร์เซีย
╠❂➣ 🔯pt : โปรตุเกศ
╠❂➣ 🔯ro : โรมาเนีย
╠❂➣ 🔯ru : รัสเซีย
╠❂➣ 🔯th : ไทย
╠❂➣ 🔯zu : ซูลู
┣━━━━━━━━━━━━━━━━━
┃    ◐✯Armtheking.🇹🇭✯◐
╰━━━━━━━━━━━━━━━━━╯
 
「วิธีใช้ : tr-th hello」"""
    return helpLanguange
  
def helpsiri():
    helpSiri = """─┅═◐✯Armtheking.🇹🇭✯◐═┅─
╭━━━━━━━━━━━━━━━━━╮
┃•◈➣ 🔯คำสั่งใช้งานบอทสิริ🔯
┣━━━━━━━━━━━━━━━━━
┃•◈➣ 🔯แอด 
┃•◈➣ 🔯แอดรอง
┃•◈➣ 🔯ตั่งค่า
┃•◈➣ 🔯ตั้งแอดรอง
┃•◈➣ 🔯สลับ
┃•◈➣ 🔯ปลดแอด
┃•◈➣ 🔯ทวิทเต้อ
┃•◈➣ 🔯ย้ายตั๋ว
┃•◈➣ 🔯บอทกลับ
┃•◈➣ 🔯ชุดล็อคen
┃•◈➣ 🔯ชุดล็อคjp
┃•◈➣ 🔯เพิ่มดำ
┃•◈➣ 🔯แก้ดำ
┃•◈➣ 🔯ลบค้างเชิญ
┃•◈➣ 🔯เปลี่ยนอด
┃•◈➣ 🔯ปิดลิ้ง
┃•◈➣ 🔯เปิดลิ้ง
┃•◈➣ 🔯ตั้งอ่าน
┃•◈➣ 🔯คนแอบ
┃•◈➣ 🔯ปิดการเชิญ
┃•◈➣ 🔯เปิดเชิญ
┃•◈➣ 🔯ปิดพูด
┃•◈➣ 🔯เปิดพูด
┃•◈➣ 🔯รันติก
┃•◈➣ 🔯ล็อคแอด
┃•◈➣ 🔯ล็อคชื่อ
┃•◈➣ 🔯ล็อครูป
┃•◈➣ 🔯ล็อคเชิญ
┣━━━━━━━━━━━━━━━━━
┃     ◐✯Armtheking.🇹🇭✯◐
╰━━━━━━━━━━━━━━━━━╯
"""
    return helpSiri
#==============================================================================#
def lineBot(op):
    try:
        if op.type == 0:
            return
        if op.type == 5:
            if settings["autoAdd"] == True:
                line.findAndAddContactsByMid(op.param1)
        if op.type == 5:
            if settings["autoBlock"] == True:
                line.blockContact(op.param1)
            msgSticker = settings["messageSticker"]["listSticker"]["addSticker"]
            if msgSticker != None:
                sid = msgSticker["STKID"]
                spkg = msgSticker["STKPKGID"]
                sver = msgSticker["STKVER"]
                sendSticker(op.param1, sver, spkg, sid)
        if op.type == 13:
            if lineMID in op.param3:
                G = line.getGroup(op.param1)
                if settings["autoJoin"] == True:
                    if settings["autoCancel"]["on"] == True:
                        if len(G.members) <= settings["autoCancel"]["members"]:
                            line.rejectGroupInvitation(op.param1)
                        else:
                            line.acceptGroupInvitation(op.param1)
                    else:
                        line.acceptGroupInvitation(op.param1)
                elif settings["autoCancel"]["on"] == True:
                    if len(G.members) <= settings["autoCancel"]["members"]:
                        line.rejectGroupInvitation(op.param1)
            else:
                Inviter = op.param3.replace("",',')
                InviterX = Inviter.split(",")
                matched_list = []
                for tag in settings["blacklist"]:
                    matched_list+=[str for str in InviterX if str == tag]
                if matched_list == []:
                    pass
                else:
                    line.cancelGroupInvitation(op.param1, matched_list)
        if op.type == 19:
            contact1 = line.getContact(op.param2)
            group = line.getGroup(op.param1)
            contact2 = line.getContact(op.param3)
            print(("[19] กลุ่มชื่อ: " + str(group.name) + "\n" + op.param1 +"\n踢人者: " + contact1.displayName + "\nMid:" + contact1.mid + "\n被踢者: " + contact2.displayName + "\nMid:" + contact2.mid ))
            if RfuProtect["protect"] == True:
                if op.param2 in admin:
                    pass
                else:
                    if settings["kickContact"] == True:
                        line.kickoutFromGroup(op.param1,[op.param2])
                        settings["blacklist"][op.param2] = True
                        time.sleep(0.1)
                        line.sendMessage(op.param1, "คนเตะมีดังนี้！")
                        line.sendContact(op.param1,op.param2)
                        time.sleep(0.1)
                        line.sendMessage(op.param1, "ผู้ที่ถูกเตะมีดังนี้！")
                        line.sendContact(op.param1,op.param3)
                    else:
                        line.kickoutFromGroup(op.param1,[op.param2])
                        settings["blacklist"][op.param2] = True
                        time.sleep(0.1)
            else:
                if settings["kickContact"] == True:
                    line.sendMessage(op.param1, "คนเตะ！")
                    line.sendContact(op.param1,op.param2)
                    time.sleep(0.1)
                    line.sendMessage(op.param1, "ผู้ที่ถูกเตะ！")
                    line.sendContact(op.param1,op.param3)
                else:
                    pass
        if op.type == 15:
            print ("[ 15 ]  NOTIFIED LEAVE GROUP")
            if settings["Lv"] == True:
                if "{gname}" in settings['bye']:
                    gName = line.getGroup(op.param1).name
                    msg = settings['bye'].replace("{gname}", gName)
                    msgSticker = settings["messageSticker"]["listSticker"]["leaveSticker"]
                    if msgSticker != None:
                        sid = msgSticker["STKID"]
                        spkg = msgSticker["STKPKGID"]
                        sver = msgSticker["STKVER"]
                        sendSticker(op.param2, sver, spkg, sid)
                msgSticker = settings["messageSticker"]["listSticker"]["leaveSticker"]
                if msgSticker != None:
                    sid = msgSticker["STKID"]
                    spkg = msgSticker["STKPKGID"]
                    sver = msgSticker["STKVER"]
                    sendSticker(op.param1, sver, spkg, sid)
        if op.type == 19:
            if settings["Nk"] == True:
                if "{gname}" in settings['kick']:
                    gName = line.getGroup(op.param1).name
                    msg = settings['kick'].replace("{gname}", gName)
                    msgSticker = settings["messageSticker"]["listSticker"]["kickSticker"]
                    if msgSticker != None:
                        sid = msgSticker["STKID"]
                        spkg = msgSticker["STKPKGID"]
                        sver = msgSticker["STKVER"]
                        sendSticker(op.param2, sver, spkg, sid)
                msgSticker = settings["messageSticker"]["listSticker"]["kickSticker"]
                if msgSticker != None:
                    sid = msgSticker["STKID"]
                    spkg = msgSticker["STKPKGID"]
                    sver = msgSticker["STKVER"]
                    sendSticker(op.param1, sver, spkg, sid)
        if op.type == 17:
            print ("[ 17 ]  NOTIFIED ACCEPT GROUP INVITATION")
            if settings["Wc"] == True:
                if "{gname}" in settings['welcome']:
                    gName = line.getGroup(op.param1).name
                    msg = settings['welcome'].replace("{gname}", gName)
                    msgSticker = settings["messageSticker"]["listSticker"]["welcomeSticker"]
                    if msgSticker != None:
                        sid = msgSticker["STKID"]
                        spkg = msgSticker["STKPKGID"]
                        sver = msgSticker["STKVER"]
                        sendSticker(op.param2, sver, spkg, sid)
                msgSticker = settings["messageSticker"]["listSticker"]["welcomeSticker"]
                if msgSticker != None:
                    sid = msgSticker["STKID"]
                    spkg = msgSticker["STKPKGID"]
                    sver = msgSticker["STKVER"]
                    sendSticker(op.param1, sver, spkg, sid)
        if op.type == 25:
            msg = op.message
            if msg.contentType == 13:
            	if settings["winvite"] == True:
                     if msg._from in admin:
                         _name = msg.contentMetadata["displayName"]
                         invite = msg.contentMetadata["mid"]
                         groups = line.getGroup(msg.to)
                         pending = groups.invitee
                         targets = []
                         for s in groups.members:
                             if _name in s.displayName:
                                 line.sendText(msg.to,"-> " + _name + " \nทำการเชิญสำเร็จ")
                                 break
                             elif invite in settings["blacklist"]:
                                 line.sendText(msg.to,"ขออภัย, " + _name + " บุคคนนี้อยู่ในรายการบัญชีดำ")
                                 line.sendText(msg.to,"ใช้คำสั่ง!, \n➡ล้างดำ➡ดึง" )
                                 break                             
                             else:
                                 targets.append(invite)
                         if targets == []:
                             pass
                         else:
                             for target in targets:
                                 try:
                                     line.findAndAddContactsByMid(target)
                                     line.inviteIntoGroup(msg.to,[target])
                                     line.sendText(msg.to,"เชิญคนนี้สำเร็จแล้ว : \n➡" + _name)
                                     settings["winvite"] = False
                                     break
                                 except:
                                     try:
                                         line.findAndAddContactsByMid(invite)
                                         line.inviteIntoGroup(op.param1,[invite])
                                         settings["winvite"] = False
                                     except:
                                         line.sendText(msg.to,"😧ตรวจพบข้อผิดพลาดที่ไม่ทราบสาเหตุ😩อาจเป็นได้ว่าบัญชีของคุณถูกแบนเชิญ😨")
                                         settings["winvite"] = False
                                         break
#        if op.type == 25:
#            msg = op.message
#            if msg.contentType == 16:
#                url = msg.contentMetadata["postEndUrl"]
#                line.like(url[25:58], url[66:], likeType=1001)
#                line.comment(url[25:58], url[66:], settings["comment"])
#        if op.type == 26:
#            msg = op.message
#            if msg.contentType == 16:
#                url = msg.contentMetadata["postEndUrl"]
#                line.like(url[25:58], url[66:], likeType=1001)
#                line.comment(url[25:58], url[66:], settings["comment"])
        if op.type == 25:
            msg = op.message
            if msg.contentType == 13:
               if settings["wblack"] == True:
                    if msg.contentMetadata["mid"] in settings["commentBlack"]:
                        line.sendText(msg.to,"รับทราบ")
                        settings["wblack"] = False
                    else:
                        settings["commentBlack"][msg.contentMetadata["mid"]] = True
                        settings["wblack"] = False
                        line.sendText(msg.to,"decided not to comment")

               elif settings["dblack"] == True:
                   if msg.contentMetadata["mid"] in settings["commentBlack"]:
                        del settings["commentBlack"][msg.contentMetadata["mid"]]
                        line.sendText(msg.to,"ลบจากรายการที่ถูกแบนแล้ว", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                        settings["dblack"] = False

                   else:
                        settings["dblack"] = False
                        line.sendText(msg.to,"Tidak Ada Dalam Daftar Blacklist")
               elif settings["wblacklist"] == True:
                 if msg._from in admin: 
                   if msg.contentMetadata["mid"] in settings["blacklist"]:
                        line.sendText(msg.to,"Sudah Ada")
                        settings["wblacklist"] = False
                   else:
                        settings["blacklist"][msg.contentMetadata["mid"]] = True
                        settings["wblacklist"] = False
                        line.sendText(msg.to,"เพิ่มบัญชีนี้ในรายการสีดำเรียบร้อยแล้ว", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})

               elif settings["dblacklist"] == True:
                 if msg._from in admin: 
                   if msg.contentMetadata["mid"] in settings["blacklist"]:
                        del settings["blacklist"][msg.contentMetadata["mid"]]
                        line.sendText(msg.to,"เพิ่มบัญชีนี้ในรายการสีขาวเรียบร้อยแล้ว", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                        settings["dblacklist"] = False

                   else:
                        settings["dblacklist"] = False
                        line.sendText(msg.to,"Tidak Ada Dalam Da ftar Blacklist")
       # if op.type == 26:
#            if settings ["mutebot2"] == True:
           # msg = op.message
           # try:
               # if msg.toType == 0:
                  #  line.log("[%s]"%(msg._from)+str(msg.text))
               # else:
                  #  group = line.getGroup(msg.to)
                    #contact = line.getContact(msg._from)
                  #  line.log("[%s]"%(msg.to)+"\nGroupname: "+str(group.name)+"\nNamenya: "+str(contact.displayName)+"\nPesannya: "+str(msg.text))
               # if msg.contentType == 0:
            #Save message to dict
                    #msg_dict[msg.id] = {"text":msg.text,"from":msg._from,"createdTime":msg.createdTime}
                #if msg.contentType == 7:
                    #stk_id = msg.contentMetadata['STKID']
                    #stk_ver = msg.contentMetadata['STKVER']
                   # pkg_id = msg.contentMetadata['STKPKGID']
                    #ret_ = "="
                    #ret_ += "\nSTICKER ID : {}".format(stk_id)
                  #  ret_ += "\nSTICKER PACKAGES ID : {}".format(pkg_id)
                    #ret_ += "\nSTICKER VERSION : {}".format(stk_ver)
                    #ret_ += "\nSTICKER URL : line://shop/detail/{}".format(pkg_id)
                    #ret_ += "\n"
                    #msg_dict[msg.id] = {"text":str(ret_),"from":msg._from,"createdTime":msg.createdTime}
            #except Exception as e:
                #print(e)                    
        if op.type == 25:
            msg = op.message
            text = msg.text
            msg_id = msg.id
            receiver = msg.to
            sender = msg._from
            if msg.toType == 0 or msg.toType == 1 or msg.toType == 2:
                if msg.toType == 0:
                    if sender != line.profile.mid:
                        to = sender
                    else:
                        to = receiver
                elif msg.toType == 1:
                    to = receiver
                elif msg.toType == 2:
                    to = receiver
            if msg.contentType == 0:
                if text is None:
                    return
#==============================================================================#
                if "พูด " in msg.text.lower():
                    spl = re.split("พูด ",msg.text,flags=re.IGNORECASE)
                    if spl[0] == "":
                        mts = spl[1]
                        mtsl = mts.split()
                        mtsTimeArg = len(mtsl) - 1
                        mtsTime = mtsl[mtsTimeArg]
                        del mtsl[mtsTimeArg]
                        mtosay = " ".join(mtsl)
                        global Rapid1To
                        Rapid1To = msg.to
                        RapidTime = mtsTime
                        rmtosay = []
                        for count in range(0,int(RapidTime)):
                            rmtosay.insert(count,mtosay)
                        p = Pool(20)
                        p.map(Rapid1Say,rmtosay)
                        p.close()
                if text.lower() == 'help':
                    icon = "http://dl.profile.line.naver.jp/"+lineProfile.pictureStatus
                    name = "คำสั่ง"                   
                    link = "http://line.me/ti/p/~tome2527"
                    myHelp = myhelp()
                    line.sendFooter(to, str(myHelp),link ,icon,name)
                    line.sendMentionFooter(to, '「ผู้ควบคุมบอท」\n', sender, "https://line.me/ti/p/~tome2527", "http://dl.profile.line-cdn.net/"+line.getContact(sender).pictureStatus, line.getContact(sender).displayName);line.sendMessage(to, line.getContact(sender).displayName, contentMetadata = {'previewUrl': 'http://dl.profile.line-cdn.net/'+line.getContact(sender).pictureStatus, 'i-installUrl': 'https://line.me/ti/p/~tome2527', 'type': 'mt', 'subText': "TOMEBOTLINE", 'a-installUrl': 'https://line.me/ti/p/~samuri5.', 'a-installUrl': ' https://line.me/ti/p/~samuri5.', 'a-packageName': 'com.spotify.music', 'countryCode': 'ID', 'a-linkUri': 'https://line.me/ti/p/~samuri5.', 'i-linkUri': 'https://line.me/ti/p/~tome2527', 'id': 'mt000000000a6b79f9', 'text': 'Khie', 'linkUri': 'https://line.me/ti/p/~tome2527'}, contentType=19)
                if text.lower() == 'help1':
                    icon = "http://dl.profile.line.naver.jp/"+lineProfile.pictureStatus
                    name = "คำสั่ง"                   
                    link = "http://line.me/ti/p/~tome2527"
                    myHelp1 = myhelp1()
                    line.sendFooter(to, str(myHelp1),link ,icon,name)
                    line.sendMentionFooter(to, '「ผู้ควบคุมบอท」\n', sender, "https://line.me/ti/p/~tome2527", "http://dl.profile.line-cdn.net/"+line.getContact(sender).pictureStatus, line.getContact(sender).displayName);line.sendMessage(to, line.getContact(sender).displayName, contentMetadata = {'previewUrl': 'http://dl.profile.line-cdn.net/'+line.getContact(sender).pictureStatus, 'i-installUrl': 'https://line.me/ti/p/~tome2527', 'type': 'mt', 'subText': "TOMEBOTLINE", 'a-installUrl': 'https://line.me/ti/p/~samuri5.', 'a-installUrl': ' https://line.me/ti/p/~samuri5.', 'a-packageName': 'com.spotify.music', 'countryCode': 'ID', 'a-linkUri': 'https://line.me/ti/p/~samuri5.', 'i-linkUri': 'https://line.me/ti/p/~tome2527', 'id': 'mt000000000a6b79f9', 'text': 'Khie', 'linkUri': 'https://line.me/ti/p/~tome2527'}, contentType=19)
                elif text.lower() == 'help2':
                    icon = "http://dl.profile.line.naver.jp/"+lineProfile.pictureStatus
                    name = "คำสั่ง"                   
                    link = "http://line.me/ti/p/~tome2527"
                    helpSet = helpset()
                    line.sendFooter(to, str(helpSet),link ,icon,name)
                    sendMessageWithMention(to, lineMID)
                elif text.lower() == 'helpsiri':
                    icon = "http://dl.profile.line.naver.jp/"+lineProfile.pictureStatus
                    name = "คำสั่งบอทตาต้อม"                   
                    link = "http://line.me/ti/p/~tome2527"
                    helpSiri = helpsiri()
                    line.sendFooter(to, str(helpSiri),link ,icon,name)
                    sendMessageWithMention(to, lineMID)
                elif text.lower() == '.help3':
                    icon = "http://dl.profile.line.naver.jp/"+lineProfile.pictureStatus
                    name = "คำสั่ง"                   
                    link = "http://line.me/ti/p/~tome2527"
                    listGrup = listgrup()
                    line.sendFooter(to, str(listGrup),link ,icon,name)
                elif text.lower() == 'help4':
                    icon = "http://dl.profile.line.naver.jp/"+lineProfile.pictureStatus
                    name = "คำสั่ง"                   
                    link = "http://line.me/ti/p/~tome2527"
                    helpSetting = helpsetting()
                    line.sendFooter(to, str(helpSetting),link ,icon,name)
                elif text.lower() == '.help5':
                    icon = "http://dl.profile.line.naver.jp/"+lineProfile.pictureStatus
                    name = "คำสั่ง"                   
                    link = "http://line.me/ti/p/~tome2527"
                    socMedia = socmedia()
                    line.sendFooter(to, str(socMedia),link ,icon,name)
                elif text.lower() == 'help6':
                    helpTextToSpeech = helptexttospeech()
                    line.sendMessage(to, str(helpTextToSpeech))
                elif text.lower() == 'help7':
                    helpLanguange = helplanguange()
                    line.sendMessage(to, str(helpLanguange))
#==============================================================================#
                elif text.lower() == 'วัดรอบ':
                    start = time.time()
                    line.sendMessage(to, "กำลังทดสอบ")
                    elapsed_time = time.time() - start
                    line.sendMessage(msg.to, "[ %s Seconds ] [ " % (elapsed_time) + str(int(round((time.time() - start) * 1000)))+" ms ]")
                elif text.lower() == 'sp':
                    start = time.time()
                    line.sendMessage(to, "กำลังทดสอบ")
                    elapsed_time = time.time() - start
                    line.sendMessage(msg.to, "[ %s Seconds ] [ " % (elapsed_time) + str(int(round((time.time() - start) * 1000)))+" ms ]")
                elif text.lower() == 'เทส':
                    line.sendMessage(to, "กำลังโหลด:▒...0%")
                    line.sendMessage(to, "█▒... 10.0%")
                    line.sendMessage(to, "██▒... 20.0%")
                    line.sendMessage(to, "███▒... 30.0%")
                    line.sendMessage(to, "████▒... 40.0%")
                    line.sendMessage(to, "█████▒... 50.0%")
                    line.sendMessage(to, "██████▒... 60.0%")
                    line.sendMessage(to, "██████▒... 70.0%")
                    line.sendMessage(to, "████████▒... 80.0%")
                    line.sendMessage(to, "█████████▒... 90.0%")
                    line.sendMessage(to, "███████████..100.0%")
                    line.sendMessage(to, "🎯〘บอทยังอยู่จะท่านผู้ชม〙🎯\n ❈͜͡✯Armtheking.🇹🇭✯͜͡❈ ")
                elif text.lower() == 'เริ่มใหม่':
                    line.sendMessage(to, "กำลังเริ่มต้นใหม่ ... โปรดรอสักครู่ ..", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                    line.sendMessage(to, "Success Restarting.", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                    restartBot()
                elif text.lower() == 'เวลออน':
                    icon = "http://dl.profile.line.naver.jp/"+lineProfile.pictureStatus
                    name = "เซลบอท"                   
                    link = "http://line.me/ti/p/~tome2527"
                    timeNow = time.time()
                    runtime = timeNow - botStart
                    runtime = format_timespan(runtime)
                    line.sendMessage(to, "ระยะเวลาการทำงานของบอท {}".format(str(runtime),link ,icon,name))
                if text.lower() == 'ออน':
                    eltime = time.time() - mulai
                    van = "ระยะเวลาการทำงานของบอท\n"+waktu(eltime)
                    line.sendMessage(receiver,van)
                elif text.lower() == 'ข้อมูล':
                    try:
                        icon = "http://dl.profile.line.naver.jp/"+lineProfile.pictureStatus
                        name = "ข้อมูลโดยบอทตาต้อม"                   
                        link = "http://line.me/ti/p/~tome2527"
                        arr = []
                        owner = adminMID
                        creator = line.getContact(owner)
                        contact = line.getContact(lineMID)
                        grouplist = line.getGroupIdsJoined()
                        contactlist = line.getAllContactIds()
                        blockedlist = line.getBlockedContactIds()
                        ret_ = "╔══[ ◐✯ARM SELFBOT✯◐➣]"
                        ret_ += "\n╠۞➢ชื่อ ═ {}".format(contact.displayName)
                        ret_ += "\n╠۞➢ กลุ่ม ═ {}".format(str(len(grouplist)))
                        ret_ += "\n╠۞➢ เพื่อน ═ {}".format(str(len(contactlist)))
                        ret_ += "\n╠۞➢บล็อค ═ {}".format(str(len(blockedlist)))
                        ret_ += "\n╠➢➢➢[สถานะ] ═ {}".format(contact.statusMessage)
                        ret_ += "\n╠۞➢ ผู้สร้าง ═ {}".format(creator.displayName)
                        ret_ += "\n╚══[ ◐✯ARM SELFBOT✯◐➣]"
                        line.sendContact(to, owner)
                        line.sendFooter(to, str(ret_),link ,icon,name)
                        line.sendMentionFooter(to, '「ผู้สร้างบอท」\n', sender, "https://line.me/ti/p/~tomebot333", "http://dl.profile.line-cdn.net/"+line.getContact(sender).pictureStatus, line.getContact(sender).displayName);line.sendMessage(to, line.getContact(sender).displayName, contentMetadata = {'previewUrl': 'http://dl.profile.line-cdn.net/'+line.getContact(sender).pictureStatus, 'i-installUrl': 'https://line.me/ti/p/~samuri5.', 'type': 'mt', 'subText': "SAMURAI BOT", 'a-installUrl': 'https://line.me/ti/p/~samuri5.', 'a-installUrl': ' https://line.me/ti/p/~samuri5.', 'a-packageName': 'com.spotify.music', 'countryCode': 'ID', 'a-linkUri': 'https://line.me/ti/p/~samuri5.', 'i-linkUri': 'https://line.me/ti/p/~samuri5.', 'id': 'mt000000000a6b79f9', 'text': 'Khie', 'linkUri': 'https://line.me/ti/p/~samuri5'}, contentType=19)
                    except Exception as e:
                        line.sendMessage(msg.to, str(e))
#==============================================================================#
                elif text.lower() == 'เช็ค':
                    try:
                        ret_ = "╭════[เช็คการตั้งค่า]\n╠═══════════════════\n║◐✯Armtheking.🇹🇭✯◐\n╠═══════════════════"
                        if settings["autoAdd"] == True: ret_ += "\n╠۞➣✔ ออโต้แอด[ ᴏɴ ]"
                        else: ret_ += "\n╠۞➣✖ ออโต้แอด[ ᴏғғ ]"
                        if settings["autoBlock"] == True: ret_ += "\n╠۞➣✔ ออโต้บล็อค[ ᴏɴ ]"
                        else: ret_ += "\n╠۞➣✖ ออโต้บล็อค[ ᴏғғ ]"
                        if settings["autoJoinTicket"] == True: ret_ += "\n╠۞➣✔ มุดลิ้ง[ ᴏɴ ]"
                        else: ret_ += "\n╠۞➣✖ มุดลิ้ง[ ᴏғғ ]"
                        if settings["autoJoin"] == True: ret_ += "\n╠۞➣✔ เข้าห้องออโต้ [ ᴏɴ ]"
                        else: ret_ += "\n╠۞➣✖ เข้าห้องออโต้[ ᴏғғ ]"
                        #ret_ += "\n╠════[🔰โหมดแสกนคำพูด🔰]\n║"
                        if settings["Api"] == True: ret_ += "\n╠۞➣✔ บอท api[ ᴏɴ ]"
                        else: ret_ += "\n╠۞➣✖ บอท api[ ᴏғғ ]"
                        if settings["Aip"] == True: ret_ += "\n╠۞➣✔ แสกนคำพูด+คำสั่งบิน[ ᴏɴ ]"
                        else: ret_ += "\n╠۞➣✖ แสกนคำพูด+คำสั่งบิน[ ᴏғғ ]"
                        #ret_ += "\n╠════[🔷เปิด/ปิดข้อความ🔷]\n║"
                        if settings["Wc"] == True: ret_ += "\n╠۞➣✔ ข้อความต้อนรับสมาชิก [ ᴏɴ ]"
                        else: ret_ += "\n╠۞➣✖ ข้อความต้อนรับสมาชิก[ ᴏғғ ]"
                        if settings["Lv"] == True: ret_ += "\n╠۞➣✔ ข้อความอำลาสมาชิก [ ᴏɴ ]"
                        else: ret_ += "\n╠۞➣✖ ข้อความอำลาสมาชิก[ ᴏғғ ]"
                        if settings["Nk"] == True: ret_ += "\n╠۞➣✔ ข้อความแจ้งเตือนคนลบ ื[ ᴏɴ ]"
                        else: ret_ += "\n╠۞➣✖ ข้อความแจ้งเตือนคนลบ[ ᴏғғ ]"
                        if settings["autoCancel"]["on"] == True:ret_+="\n╠۞➣🚻 ปฏิเสธกลุ่มที่มีสมาชิกต่ำกว่า: " + str(settings["autoCancel"]["members"]) + "คน"
                        else: ret_ += "\n╠۞➣✖ ปฏิเสธกลุ่มเชิญ[ ᴏғғ ]"						
                        if settings["autoLeave"] == True: ret_ += "\n╠۞➣✔ ออกแชทรวม [ ᴏɴ ]"
                        else: ret_ += "\n╠۞➣✖ ออกแชทรวม[ ᴏғғ ]"
                        if settings["autoRead"] == True: ret_ += "\n╠۞➣✔ อ่านออโต้ [ ᴏɴ ]"
                        else: ret_ += "\n╠۞➣✖ อ่านออโต้[ ᴏғғ ]"				
                        if settings["checkContact"] == True: ret_ += "\n╠۞➣✔ อ่านคท [ ᴏɴ ]"
                        else: ret_ += "\n╠۞➣✖ อ่านคท[ ᴏғғ ]"
                        if settings["checkPost"] == True: ret_ += "\n╠۞➣✔ เช็คโพส [ ᴏɴ ]"
                        else: ret_ += "\n╠❂➣✖ เช็คโพส[ ᴏғғ ]"
                        if settings["checkSticker"] == True: ret_ += "\n╠۞➣✔ Sticker [ ᴏɴ ]"
                        else: ret_ += "\n╠۞➣✖ Sticker[ ᴏғғ ]"
                        #ret_ += "\n╠═════[🔶ระบบแทค🔶]\n║"
                        if settings["pmMessage"] == True: ret_ += "\n╠۞➣✔ ตอบแทคแชท [ ᴏɴ ]"
                        else: ret_ += "\n╠۞➣✖ ตอบแทคในแชท[ ᴏғғ ]"
                        if settings["detectMention"] == True: ret_ += "\n╠۞➣✔ ตอบกลับคนแทค [ ᴏɴ ]"
                        else: ret_ += "\n╠۞➣✖ ตอบกลับคนแทค[ ᴏғғ ]"
                        if settings["potoMention"] == True: ret_ += "\n╠۞➣✔ แสดงภาพคนแทค [ ᴏɴ ]"
                        else: ret_ += "\n╠۞➣✖ แสดงภาพคนแทค[ ᴏғғ ]"
                        if settings["kickMention"] == True: ret_ += "\n╠۞➣✔ เตะคนแทค [ ᴏɴ ]"
                        else: ret_ += "\n╠۞➣✖ เตะคนแทคแ[ ᴏғғ ]"
                        if settings["kickContact"] == True: ret_ += "\n╠۞➣✔ สั่งเตะด้วย คท [ ᴏɴ ]"
                        else: ret_ += "\n╠۞➣✖ สั่งเตะด้วย คท [ ᴏғғ ]"
                        if settings["delayMention"] == True: ret_ += "\n╠۞➣✔ แทคกลับคนแทค [ ᴏɴ ]"
                        else: ret_ += "\n╠۞➣✖ แทคกลับคนแทค[ ᴏғғ ]"
                        if settings["detectMentionPM"] == True: ret_ += "\n╠۞➣✔ แทคกลับทางแชท [ ᴏɴ ]"
                        else: ret_ += "\n╠۞➣✖ แทคกลับทางแชท[ ᴏғғ ]"
                        ret_ += "\n╠═════[ระบบป้องกัน]\n║"
                        if RfuProtect["inviteprotect"] == True: ret_ += "\n╠۞➣✔ กันเชิญ [ ᴏɴ ]"
                        else: ret_ += "\n╠۞➣✖ กันเชิญ[ ᴏғғ ]"
                        if RfuProtect["cancelprotect"] == True: ret_ += "\n╠۞➣✔ กันยกเชิญ [ ᴏɴ ]"
                        else: ret_ += "\n╠۞➣✖ กันยกเชิญ[ ᴏғғ ]"
                        if RfuProtect["protect"] == True: ret_ += "\n╠۞➣✔ ป้องกัน [ ᴏɴ ]"
                        else: ret_ += "\n╠۞➣✖ ป้องกัน[ ᴏғғ ]"
                        if RfuProtect["linkprotect"] == True: ret_ += "\n╠۞➣✔ ป้องกันเปิดลิ้ง [ ᴏɴ ]"
                        else: ret_ += "\n╠۞➣✖ ป้องกันเปิดลิ้ง[ ᴏғғ ]"
                        if RfuProtect["Protectguest"] == True: ret_ += "\n╠۞➣✔ ป้องกันสมาชิก [ ᴏɴ ]"
                        else: ret_ += "\n╠۞➣✖ ป้องกันสมาชิก[ ᴏғғ ]"
                        if RfuProtect["Protectjoin"] == True: ret_ += "\n╠۞➣✔ ป้องกันเข้ากลุ่ม [ ᴏɴ ]"
                        else: ret_ += "\n╠۞➣✖ ป้องกันเข้ากลุ่ม[ ᴏғғ ]"						
                        ret_ += "\n╠═══════════════════\n╰═══[🇹🇭™◐✯Armtheking.🇹🇭✯◐]"
                        icon = "http://dl.profile.line.naver.jp/"+lineProfile.pictureStatus
                        name = "เช็คการตั้งค่าบอท"                   
                        link = "http://line.me/ti/p/~tome2527"
                        line.sendFooter(to, str(ret_),link ,icon,name)
                        line.sendMentionFooter(to, '「ผู้ควบคุมบอท」\n', sender, "https://line.me/ti/p/~tome2527", "http://dl.profile.line-cdn.net/"+line.getContact(sender).pictureStatus, line.getContact(sender).displayName);line.sendMessage(to, line.getContact(sender).displayName, contentMetadata = {'previewUrl': 'http://dl.profile.line-cdn.net/'+line.getContact(sender).pictureStatus, 'i-installUrl': 'https://line.me/ti/p/~tome2527', 'type': 'mt', 'subText': "TOMEBOTLINE", 'a-installUrl': 'https://line.me/ti/p/~tome2527', 'a-installUrl': ' https://line.me/ti/p/~tome2527', 'a-packageName': 'com.spotify.music', 'countryCode': 'ID', 'a-linkUri': 'https://line.me/ti/p/~tome2527', 'i-linkUri': 'https://line.me/ti/p/~tome2527', 'id': 'mt000000000a6b79f9', 'text': 'Khie', 'linkUri': 'https://line.me/ti/p/~tome2527'}, contentType=19)
                    except Exception as e:
                        line.sendMessage(msg.to, str(e))
                elif text.lower() == 'เปิดแอด':
                    settings["autoAdd"] = True
                    settings["autoBlock"] = False
                    RfuProtect["autoAdd"] == True
                    RfuProtect["autoBlock"] == False
                    line.sendMessage(to, "     [ Add ᴏɴ ]\n\nออโต้แอดเปิดใช้งานเรียบร้อยแล้ว🔰\n◐✯ARM SELFBOT✯◐", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                elif text.lower() == 'เปิดบล็อค':
                    settings["autoBlock"] = True
                    settings["autoAdd"] = False
                    RfuProtect["autoBlock"] == True
                    RfuProtect["autoAdd"] == False
                    line.sendMessage(to, "     [ Block ᴏɴ ]\n\nออโต้บล๊อคเปิดใช้งานแล้ว🔰\n◐✯ARM SELFBOT✯◐", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                elif text.lower() == 'ปิดแอด':
                    settings["autoAdd"] = False
                    RfuProtect["autoAdd"] == False
                    line.sendMessage(to, "     [ Add ᴏғғ ]\n\nออโต้แอดปิดใช้งานแล้ว🔰\n◐✯ARM SELFBOT✯◐", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                elif text.lower() == 'ปิดบล็อค':
                    settings["autoBlock"] = False
                    RfuProtect["autoBlock"] == False
                    line.sendMessage(to, "     [ Block ᴏғғ ]\n\nออโต้บล็อคปิดใช้งานแล้ว🔰\n◐✯ARM SELFBOT✯◐", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                elif text.lower() == 'เปิดเข้า':
                    settings["autoJoin"] = True
                    line.sendMessage(to, "[ ᴏɴ ]ออโต้เข้าห้องเปิดใช้งาน🔰\n◐✯ARM SELFBOT✯◐", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                elif text.lower() == 'ปิดเข้า':
                    settings["autoJoin"] = False
                    line.sendMessage(to, "[ ᴏғғ ]ออโต้เข้าห้องปิดใช้งาน🔰\n◐✯ARM SELFBOT✯◐", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                elif "gcancel:" in msg.text:
                    try:
                        strnum = msg.text.replace("gcancel:","")
                        if strnum == "off":
                                settings["autoCancel"]["on"] = False
                                if settings["lang"] == "JP":
                                    line.sendText(msg.to,"ปิดใช้งานระบบปฏิเสธคำเชิญตามจำนวนสมาชิก\n◐✯AEM SELFBOT✯◐", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                                else:
                                    line.sendText(msg.to,"关了邀请拒绝。要时开请指定人数发送")
                        else:
                                num =  int(strnum)
                                settings["autoCancel"]["on"] = True
                                if settings["lang"] == "JP":
                                    line.sendText(msg.to, " สมาชิกในกลุ่มที่ไม่ถึง" + strnum + "จะถูกปฏิเสธคำเชิญโดยอัตโนมัติ", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                                else:
                                    line.sendText(msg.to,strnum + "使人以下的小组用自动邀请拒绝")
                    except:
                        if settings["lang"] == "JP":
                                line.sendText(msg.to,str(settings["eror"]))
                        else:
                                line.sendText(msg.to,"Bizarre ratings")					
                elif text.lower() == 'เปิดออก':
                    settings["autoLeave"] = True
                    line.sendMessage(to, "เปิดระบบออกแชทรวมอัตโนมัติ🔰\n◐✯ARM SELFBOT✯◐", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                elif text.lower() == 'ปิดออก':
                    settings["autoLeave"] = False
                    line.sendMessage(to, "ปิดระบบออกจากแชทอัตโนมัติแล้ว🔰\n◐✯ARM SELFBOT✯◐", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                elif text.lower() == 'เปิดอ่าน':
                    settings["autoRead"] = True
                    line.sendMessage(to, "เปิดใช้งานการอ่านอัตโนมัตแล้ว🔰\n◐✯ARM SELFBOT✯◐", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                elif text.lower() == 'ปิดอ่าน':
                    settings["autoRead"] = False
                    line.sendMessage(to, "ปิดใช้งานการอ่านอัตโนมัติแล้ว🔰\n◐✯ARM SELFBOT✯◐", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                elif text.lower() == 'เปิดติ๊ก':
                    settings["checkSticker"] = True
                    line.sendMessage(to, "Check sticker enabled.\n◐✯ARM SELFBOT✯◐", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                elif text.lower() == 'ปิดติ๊ก':
                    settings["checkSticker"] = False
                    line.sendMessage(to, "Check sticker disabled.\n◐✯ARM SELFBOT✯◐", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                elif text.lower() == 'เปิดมุด':
                    settings["autoJoinTicket"] = True
                    line.sendMessage(to, "Autojoin byTicket  enabled.\n◐✯ARM SELFBOT✯◐", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                elif text.lower() == 'ปิดมุด':
                    settings["autoJoinTicket"] = False
                    line.sendMessage(to, "Autojoin byTicket  disabled.\n◐✯ARM SELFBOT✯◐", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                elif text.lower() == 'เปิดหวดคท':
                    settings["kickContact"] = True
                    line.sendMessage(to, "KickContact ✔\n◐✯ARM SELFBOT✯◐", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                elif text.lower() == 'ปิดหวดคท':
                    settings["kickContact"] = False
                    line.sendMessage(to, "KickContact ✘\n◐✯ARM SELFBOT✯◐", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
#==============================================================================#
                elif msg.text.lower() == "me":
                    me = line.getContact(lineMID)
                    line.sendMessage(msg.to,"[👇ชื่อของคุณ👇]")
                    sendMessageWithMention(to, lineMID)
                    #line.sendMessage(msg.to,"[สเตตัส]\n" + me.statusMessage)
                    line.sendContact(to, lineMID)
                    line.sendImageWithURL(msg.to,"http://dl.profile.line-cdn.net/" + me.pictureStatus)
                    cover = line.getProfileCoverURL(lineMID)
                   # line.sendImageWithURL(msg.to, cover)
                    #line.sendMessage(msg.to,str(settings["comment"]))
                elif text.lower() == "ตัวเรา":
                    line.sendMentionFooter(to, '「ผู้สร้างบอท」\n', sender, "https://line.me/ti/p/~samuri5.", "http://dl.profile.line-cdn.net/"+line.getContact(sender).pictureStatus, line.getContact(sender).displayName);line.sendMessage(to, line.getContact(sender).displayName, contentMetadata = {'previewUrl': 'http://dl.profile.line-cdn.net/'+line.getContact(sender).pictureStatus, 'i-installUrl': 'https://line.me/ti/p/~samuri5.', 'type': 'mt', 'subText': "SAMURAI BOT", 'a-installUrl': 'https://line.me/ti/p/~samuri5.', 'a-installUrl': ' https://line.me/ti/p/~samuri5.', 'a-packageName': 'com.spotify.music', 'countryCode': 'ID', 'a-linkUri': 'https://line.me/ti/p/~samuri5.', 'i-linkUri': 'https://line.me/ti/p/~samuri5.', 'id': 'mt000000000a6b79f9', 'text': 'Khie', 'linkUri': 'https://line.me/ti/p/~samuri5'}, contentType=19)
                elif text.lower() == "ศรราม":
                    userid = "https://line.me/ti/p/~" + line.profile.userid
                    line.sendImageWithFooter(to, "http://dl.profile.line-cdn.net/"+line.getContact(sender).pictureStatus, str(userid), "http://dl.profile.line-cdn.net/"+line.getContact(sender).pictureStatus, line.getContact(sender).displayName)
                    line.sendMentionFooter(to, '「Me」\n', sender, str(userid), "http://dl.profile.line-cdn.net/"+line.getContact(sender).pictureStatus, line.getContact(sender).displayName)
                    line.sendMusic(to, line.getContact(sender).displayName, "http://dl.profile.line-cdn.net/"+line.getContact(sender).pictureStatus, str(userid), "SAMURAI BOT", line.getContact(sender).displayName)
                elif text.lower() == 'คทเรา':
                    sendMessageWithMention(to, lineMID)
                    line.sendContact(to, lineMID)
                elif text.lower() == 'Me':
                    sendMessageWithMention(to, lineMID)
                    line.sendContact(to, adminMID)
                elif text.lower() == 'ไอดี':
                    line.sendMessage(msg.to,"[MID]\n" +  lineMID)
                elif text.lower() == 'ชื่อ':
                    me = line.getContact(lineMID)
                    line.sendMessage(msg.to,"[DisplayName]\n" + me.displayName, contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                elif text.lower() == 'ตัส':
                    me = line.getContact(lineMID)
                    line.sendMessage(msg.to,"[StatusMessage]\n" + me.statusMessage, contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                elif text.lower() == 'รูปโปร':
                    me = line.getContact(lineMID)
                    line.sendImageWithURL(msg.to,"http://dl.profile.line-cdn.net/" + me.pictureStatus)
                elif text.lower() == 'วีดีโอโปร':
                    me = line.getContact(lineMID)
                    line.sendVideoWithURL(msg.to,"http://dl.profile.line-cdn.net/" + me.pictureStatus + "/vp")
                elif text.lower() == 'รูปปก':
                    me = line.getContact(lineMID)
                    cover = line.getProfileCoverURL(lineMID)    
                    line.sendImageWithURL(msg.to, cover)
                elif text.lower() == 'คอมเม้น':
                    line.sendMessage(msg.to,str(settings["comment1"]), contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                    line.sendMessage(msg.to, None, contentMetadata={"STKID":"52114123","STKPKGID":"11539","STKVER":"1"}, contentType=7)
                elif text.lower() == 'ทักเข้า':
                    line.sendMessage(msg.to, str(settings["welcome"]), contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                elif text.lower() == 'ทักออก':
                    line.sendMessage(msg.to, str(settings["bye"]), contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                elif text.lower() == 'ทักเตะ':
                    line.sendMessage(msg.to, str(settings["kick"]), contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                elif text.lower() == 'ข้อความแอด':
                    line.sendMessage(msg.to, str(settings["message"]), contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                elif text.lower() == 'ข้อความแทค':
                    line.sendMessage(msg.to, str(settings["Respontag"]), contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                elif text.lower() == 'แทคล่อง':
                    gs = line.getGroup(to)
                    targets = []
                    for g in gs.members:
                        if g.displayName in "":
                            targets.append(g.mid)
                    if targets == []:
                        line.sendMessage(to, "ม่มีคนใส่ร่องหนในกลุ่มนี้😂")
                    else:
                        mc = ""
                        for target in targets:
                            mc += sendMessageWithMention(to,target) + "\n"
                        line.sendMessage(to, mc)
                elif text.lower() == 'ไอดีล่อง':
                    gs = line.getGroup(to)
                    lists = []
                    for g in gs.members:
                        if g.displayName in "":
                            lists.append(g.mid)
                    if lists == []:
                        line.sendMessage(to, "ไม่มีmidคนใส่ร่องหน🤗")
                    else:
                        mc = ""
                        for mi_d in lists:
                            mc += "->" + mi_d + "\n"
                        line.sendMessage(to,mc)
                elif text.lower() == 'คทล่อง':
                    gs = line.getGroup(to)
                    lists = []
                    for g in gs.members:
                        if g.displayName in "":
                            lists.append(g.mid)
                    if lists == []:
                        line.sendMessage(to, "ไม่มีคนใส่ร่องหนในกลุ่มนี้😂")
                    else:
                        for ls in lists:
                            contact = line.getContact(ls)
                            mi_d = contact.mid
                            line.sendContact(to, mi_d)
                elif msg.text.lower().startswith("คท "):
                    if 'MENTION' in list(msg.contentMetadata.keys())!= None:
                        names = re.findall(r'@(\w+)', text)
                        mention = ast.literal_eval(msg.contentMetadata['MENTION'])
                        mentionees = mention['MENTIONEES']
                        lists = []
                        for mention in mentionees:
                            if mention["M"] not in lists:
                                lists.append(mention["M"])
                        for ls in lists:
                            contact = line.getContact(ls)
                            mi_d = contact.mid
                            line.sendContact(msg.to, mi_d)
                elif msg.text.lower().startswith("ไอดี "):
                    if 'MENTION' in list(msg.contentMetadata.keys())!= None:
                        names = re.findall(r'@(\w+)', text)
                        mention = ast.literal_eval(msg.contentMetadata['MENTION'])
                        mentionees = mention['MENTIONEES']
                        lists = []
                        for mention in mentionees:
                            if mention["M"] not in lists:
                                lists.append(mention["M"])
                        ret_ = "[ Mid User ]"
                        for ls in lists:
                            ret_ += "\n{}" + ls
                        line.sendMessage(msg.to, str(ret_))
                elif msg.text.lower().startswith("ชื่อ "):
                    if 'MENTION' in list(msg.contentMetadata.keys())!= None:
                        names = re.findall(r'@(\w+)', text)
                        mention = ast.literal_eval(msg.contentMetadata['MENTION'])
                        mentionees = mention['MENTIONEES']
                        lists = []
                        for mention in mentionees:
                            if mention["M"] not in lists:
                                lists.append(mention["M"])
                        for ls in lists:
                            contact = line.getContact(ls)
                            line.sendMessage(msg.to, "[ Display Name ]\n" + contact.displayName)
                elif msg.text.lower().startswith("ตัส "):
                    if 'MENTION' in list(msg.contentMetadata.keys())!= None:
                        names = re.findall(r'@(\w+)', text)
                        mention = ast.literal_eval(msg.contentMetadata['MENTION'])
                        mentionees = mention['MENTIONEES']
                        lists = []
                        for mention in mentionees:
                            if mention["M"] not in lists:
                                lists.append(mention["M"])
                        for ls in lists:
                            contact = line.getContact(ls)
                            line.sendMessage(msg.to, "[ Status Message ]\n{}" + contact.statusMessage)
                elif msg.text.lower().startswith("รูปโปร "):
                    if 'MENTION' in list(msg.contentMetadata.keys())!= None:
                        names = re.findall(r'@(\w+)', text)
                        mention = ast.literal_eval(msg.contentMetadata['MENTION'])
                        mentionees = mention['MENTIONEES']
                        lists = []
                        for mention in mentionees:
                            if mention["M"] not in lists:
                                lists.append(mention["M"])
                        for ls in lists:
                            path = "http://dl.profile.line.naver.jp/" + line.getContact(ls).pictureStatus
                            line.sendImageWithURL(msg.to, str(path))
                elif msg.text.lower().startswith("วีดีโอโปร "):
                    if 'MENTION' in list(msg.contentMetadata.keys())!= None:
                        names = re.findall(r'@(\w+)', text)
                        mention = ast.literal_eval(msg.contentMetadata['MENTION'])
                        mentionees = mention['MENTIONEES']
                        lists = []
                        for mention in mentionees:
                            if mention["M"] not in lists:
                                lists.append(mention["M"])
                        for ls in lists:
                            path = "http://dl.profile.line.naver.jp/" + line.getContact(ls).pictureStatus + "/vp"
                            line.sendImageWithURL(msg.to, str(path))
                elif msg.text.lower().startswith("รูปปก "):
                    if line != None:
                        if 'MENTION' in list(msg.contentMetadata.keys())!= None:
                            names = re.findall(r'@(\w+)', text)
                            mention = ast.literal_eval(msg.contentMetadata['MENTION'])
                            mentionees = mention['MENTIONEES']
                            lists = []
                            for mention in mentionees:
                                if mention["M"] not in lists:
                                    lists.append(mention["M"])
                            for ls in lists:
                                path = line.getProfileCoverURL(ls)
                                line.sendImageWithURL(msg.to, str(path))
                elif msg.text.lower().startswith("เพิ่มเพื่อน "):
                    if 'MENTION' in msg.contentMetadata.keys()!= None:
                        names = re.findall(r'@(\w+)', text)
                        mention = ast.literal_eval(msg.contentMetadata['MENTION'])
                        mentionees = mention['MENTIONEES']
                        lists = []
                        for mention in mentionees:
                            if mention["M"] not in lists:
                                lists.append(mention["M"])
                        for ls in lists:
                            contact = line.getContact(ls)
                            line.findAndAddContactsByMid(ls)
                        line.sendMessage(to, "เพิ่มคุณ" + str(contact.displayName) + " เป็นเพื่อนแล้ว")
                elif msg.text.lower().startswith("ลบเพื่อน "):
                    if 'MENTION' in msg.contentMetadata.keys()!= None:
                        names = re.findall(r'@(\w+)', text)
                        mention = ast.literal_eval(msg.contentMetadata['MENTION'])
                        mentionees = mention['MENTIONEES']
                        lists = []
                        for mention in mentionees:
                            if mention["M"] not in lists:
                                lists.append(mention["M"])
                        for ls in lists:
                            line.delContact(ls)
                        line.sendMessage(to, "ลบออกจากการเป็นเพื่อนแล้ว", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                elif text.lower()  == "ล้างเพื่อน" or text.lower()  == " unfriendall":
                    try:
                        friend = line.getContacts(line.getAllContactIds())
                        line.sendMessage(to,"คุณได้ล้างเพื่อนทั่งหมด {} คน".format(len(friend)))
                        for unfriend in friend:
                            line.delContact(unfriend.mid)
                        line.sendMessage(to,"คุณได้ล้างเพื่อนทั่งหมด {} คน".format(len(friend)))
                    except Exception as error:
                        line.sendMessage(to, "「 Result Error 」\n" + str(error))
                elif ".โพส " in msg.text:
                    tl_text = msg.text.replace("โพส ","")
                    line.sendText(msg.to,"line://home/post?userMid="+lineMID+"&postId="+line.new_post(tl_text)["result"]["post"]["postInfo"]["postId"])
                elif msg.text in [".โหลด"]:
                    if msg._from in admin:
                        wek = line.getContact(lineMID)
                        a = wek.pictureStatus
                        r = wek.displayName
                        i = wek.statusMessage
                        s = open('mydn.txt',"w")
                        s.write(r)
                        s.close()
                        t = open('mysm.txt',"w")
                        t.write(i)
                        t.close()
                        u = open('myps.txt',"w")
                        u.write(a)
                        u.close()
                        line.sendText(msg.to, "backup has been active")
                        print (wek)
                        print (a)
                        print (r)
                        print (i)
                
                elif "ก๊อป " in msg.text:
                    targets = []
                    key = eval(msg.contentMetadata["MENTION"])
                    key["MENTIONEES"][0]["M"]
                    for x in key["MENTIONEES"]:
                            targets.append(x["M"])
                    for target in targets:
                        try:
                            contact = line.getContact(target)
                            X = contact.displayName
                            profile = line.getProfile()
                            profile.displayName = X
                            line.updateProfile(profile)
                            line.sendMessage(msg.to, "Success...")
                        #---------------------------------------
                            Y = contact.statusMessage
                            lol = line.getProfile()
                            lol.statusMessage = Y
                            line.updateProfile(lol)
                        #---------------------------------------
                            settings["changePictureProfile"] = True
                            me = line.getContact(target)     
                            line.sendImageWithURL(msg.to,"http://dl.profile.line-cdn.net/" + me.pictureStatus)
                        except Exception as e:
                            line.sendMessage(msg.to, "Failed!")
                            print (e)

                elif "คืนร่าง" in msg.text:
                    if msg._from in admin:
                            try:
                                h = open('mydn.txt',"r")
                                name = h.read()
                                h.close()
                                x = name
                                profile = line.getProfile()
                                profile.displayName = x
                                line.updateProfile(profile)
                                i = open('mysm.txt',"r")
                                sm = i.read()
                                i.close()
                                y = sm
                                cak = line.getProfile()
                                cak.statusMessage = y
                                line.updateProfile(cak)
                                line.sendText(msg.to, "คืนได้แค่ชื่อกับตัสนะ😂😂")

                            except Exception as e:
                                line.sendText(msg.to,"การคืนร่างล้มเหลว!")
                                print (e)
                elif msg.text in ["Allprotect on","เปิดกทม"]:
                        settings["kickMention"] = True
                        settings["Aip"] = False
                        RfuProtect["protect"] = True
                        RfuProtect["cancelprotect"] = True
                        RfuProtect["inviteprotect"] = True 
                        RfuProtect["linkprotect"] = True 
                        RfuProtect["Protectguest"] = True
                        RfuProtect["Protectjoin"] = True
                        line.sendText(msg.to,"การตั้งค่าชุดรักษาความปลอดภัยทั้งหมด เปิด👌\n◐✯ARM SELFBOT✯◐", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
						
                elif msg.text in ["Allprotect off","ปิดกทม"]:
                        settings["kickMention"] = False
                        settings["Aip"] = False
                        RfuProtect["protect"] = False
                        RfuProtect["cancelprotect"] = False
                        RfuProtect["inviteprotect"] = False 
                        RfuProtect["linkprotect"] = False 
                        RfuProtect["Protectguest"] = False
                        RfuProtect["Protectjoin"] = False
                        line.sendText(msg.to,"การตั้งค่าชุดรักษาความปลอดภัยทั้งหมด ปิด👌\n◐✯ARM SELFBOT✯◐", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                        
                elif msg.text in ["Allmsg on","เปิดข้อความ"]:
                        settings["Wc"] = True
                        settings["Lv"] = True
                        settings["Nk"] = True
                        settings["autoRead"] = True
                        settings["checkSticker"] = True 
                        settings["checkContact"] = True 
                        settings["checkPost"] = True
                        settings["potoMention"] = True
                        settings["detectMention"] = True
                        settings["delayMention"] = True
                        settings["Api"] = True
                        line.sendText(msg.to,"การตั้งค่าชุดข้อความทั้งหมด เปิด👌\n◐✯ARM SELFBOT✯◐", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
						
                elif msg.text in ["Allmsg off","ปิดข้อความ"]:
                        settings["Wc"] = False
                        settings["Lv"] = False
                        settings["Nk"] = False
                        settings["autoRead"] = True
                        settings["checkSticker"] = False 
                        settings["checkContact"] = False 
                        settings["checkPost"] = False
                        settings["detectMention"] = False
                        settings["potoMention"] = False
                        settings["delayMention"] = False
                        settings["Api"] = False
                        line.sendText(msg.to,"การตั้งค่าชุดข้อความทั้งหมด ปิด👌\n◐✯ARM SELFBOT✯◐", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
#==============================================================================#
                elif msg.text.lower().startswith("mimicadd "):
                    targets = []
                    key = eval(msg.contentMetadata["MENTION"])
                    key["MENTIONEES"][0]["M"]
                    for x in key["MENTIONEES"]:
                        targets.append(x["M"])
                    for target in targets:
                        try:
                            settings["mimic"]["target"][target] = True
                            line.sendMessage(msg.to,"Mimic has been added as")
                            break
                        except:
                            line.sendMessage(msg.to,"Added Target Fail !")
                            break
                elif msg.text.lower().startswith("mimicdel "):
                    targets = []
                    key = eval(msg.contentMetadata["MENTION"])
                    key["MENTIONEES"][0]["M"]
                    for x in key["MENTIONEES"]:
                        targets.append(x["M"])
                    for target in targets:
                        try:
                            del settings["mimic"]["target"][target]
                            line.sendMessage(msg.to,"Mimic deleting succes...", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                            break
                        except:
                            line.sendMessage(msg.to,"Deleted Target Fail !", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                            break
                elif text.lower() == 'mimiclist':
                    if settings["mimic"]["target"] == {}:
                        line.sendMessage(msg.to,"Tidak Ada Target", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                    else:
                        mc = "╔══[ Mimic List ]"
                        for mi_d in settings["mimic"]["target"]:
                            mc += "\n╠ "+line.getContact(mi_d).displayName
                        line.sendMessage(msg.to,mc + "\n╚══[ Finish ]", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                    
                elif "mimic" in msg.text.lower():
                    sep = text.split(" ")
                    mic = text.replace(sep[0] + " ","")
                    if mic == "on":
                        if settings["mimic"]["status"] == False:
                            settings["mimic"]["status"] = True
                            line.sendMessage(msg.to,"Mimic enabled.", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                    elif mic == "off":
                        if settings["mimic"]["status"] == True:
                            settings["mimic"]["status"] = False
                            line.sendMessage(msg.to,"Mimic disabled.", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                elif 'เพลสโต ' in msg.text.lower():
                        tob = msg.text.lower().replace('เพลสโต ',"")
                        line.sendText(msg.to,"กรุณารอสักครู่...")
                        line.sendText(msg.to,"ผลจากการค้นหา : "+tob+"\nจาก : Google Play\nลิ้งโหลด : https://play.google.com/store/search?q=" + tob)
                        line.sendText(msg.to,"👆กรุณากดลิ้งเพื่อทำการโหลดแอพ👆")
                elif 'ขอเพลง ' in msg.text.lower():
                        tob = msg.text.lower().replace('ขอเพลง ',"")
                        line.sendText(msg.to,"กรุณารอสักครู่...")
                        line.sendText(msg.to,"ผลจากการค้นหา : "+tob+"\nจาก : ยูทูป\nลิ้งรับชม : https://m.youtube.com/results?search_query=เพลง" + tob)
                        line.sendText(msg.to,"👆กรุณากดลิ้งเพื่อทำการโหลดแอพ👆")
                elif 'github ' in msg.text.lower():
                        tob = msg.text.lower().replace('github ',"")
                        line.sendText(msg.to,"กรุณารอสักครู่...")
                        line.sendText(msg.to,"ผลจากการค้นหา : "+tob+"\nจาก : GitHub\nลิ้ง : https://github.com/search?q=" + tob)
                        line.sendText(msg.to,"👆ค้นหาสำเร็จแล้ว👆")
                elif 'กูเกิ้ล ' in msg.text.lower():
                        tob = msg.text.lower().replace('กูเกิ้ล ',"")
                        line.sendText(msg.to,"กรุณารอสักครู่...")
                        line.sendText(msg.to,"ผลจากการค้นหา : "+tob+"\nจาก : กูเกิ้ล\nลิ้ง : https://www.google.co.th/search?q=" + tob)
                        line.sendText(msg.to,"👆ค้นหาสำเร็จแล้ว👆")
                elif 'เฟสบุค ' in msg.text.lower():
                        tob = msg.text.lower().replace('เฟสบุค ',"")
                        line.sendText(msg.to,"กรุณารอสักครู่...")
                        line.sendText(msg.to,"ผลจากการค้นหา : "+tob+"\nจาก : เฟสบุค\nลิ้ง : https://m.facebook.com/search/top/?q=" + tob)
                        line.sendText(msg.to,"👆ค้นหาสำเร็จแล้วเชิญกดลิ้งเพื่อเข้าไปดูรายละเอียด👆")
                elif "คท:" in msg.text:
                    mmid = msg.text.replace("คท:","")
                    line.sendMessage(to, text=None, contentMetadata={'mid': mmid}, contentType=13)
                elif "ค้นหาไอดี " in msg.text:
                    msgg = msg.text.replace("ดำค้นหาไอดี ",'')
                    conn = line.findContactsByUserid(msgg)
                    if True:
                        msg.contentType = 13
                        msg.contentMetadata = {'mid': conn.mid}
                        line.sendText(msg.to,"http://line.me/ti/p/~" + msgg)
                        line.sendMessage(to,msg)
                elif "Spam " in msg.text:
                    txt = msg.text.split(" ")
                    jmlh = int(txt[2])
                    teks = msg.text.replace("Spam "+str(txt[1])+" "+str(jmlh)+" ","")
                    tulisan = jmlh * (teks+"\n")
                    if txt[1] == "on":
                        if jmlh <= 100000:
                           for x in range(jmlh):
                               line.sendMessage(msg.to, teks)
                        else:
                           line.sendMessage(msg.to, "Out of Range!", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                    elif txt[1] == "off":
                        if jmlh <= 100000:
                            line.sendMessage(msg.to, tulisan)
                        else:
                            line.sendMessage(msg.to, "Out Of Range!", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
#==============================================================================#
                elif text.lower() == 'แอด':
                    group = line.getGroup(to)
                    GS = group.creator.mid
                    line.sendContact(to, GS)
                    line.sendMessage(to, "☝คนนี้แหล่ะคนสร้างกลุ่มนี้", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                elif text.lower() == 'ไอดีกลุ่ม':
                    gid = line.getGroup(to)
                    line.sendMessage(to, "ไอดีกลุ่ม \n" + gid.id)
                elif text.lower() == 'รูปกลุ่ม':
                    group = line.getGroup(to)
                    path = "http://dl.profile.line-cdn.net/" + group.pictureStatus
                    line.sendImageWithURL(to, path)
                elif text.lower() == 'ชื่อกลุ่ม':
                    gid = line.getGroup(to)
                    line.sendMessage(to, "ชื่อกลุ่ม -> \n" + gid.name)
                elif text.lower() == 'ลิ้ง':
                    if msg.toType == 2:
                        group = line.getGroup(to)
                        if group.preventedJoinByTicket == False:
                            ticket = line.reissueGroupTicket(to)
                            line.sendMessage(to, "ลิ้งของกลุ่ม\nhttps://line.me/R/ti/g/{}".format(str(ticket)), contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                elif text.lower() == 'เปิดลิ้ง':
                    if msg.toType == 2:
                        group = line.getGroup(to)
                        if group.preventedJoinByTicket == False:
                            line.sendMessage(to, "เปิดลิ้งเรียบร้อย\n◐✯ARM SELFBOT✯◐", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                        else:
                            group.preventedJoinByTicket = False
                            line.updateGroup(group)
                            line.sendMessage(to, "เปิดลิ้งเรียบร้อย\n◐✯ARM SELFBOT✯◐", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                elif text.lower() == 'ปิดลิ้ง':
                    if msg.toType == 2:
                        group = line.getGroup(to)
                        if group.preventedJoinByTicket == True:
                            line.sendMessage(to, "ปิดลิ้งเรียบร้อย\n◐✯ARM SELFBOT✯◐", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                        else:
                            group.preventedJoinByTicket = True
                            line.updateGroup(group)
                            line.sendMessage(to, "ปิดลิ้งเรียบร้อย\n◐✯ARM SELFBOT✯◐", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                elif text.lower() == 'ข้อมูลกลุ่ม':
                    group = line.getGroup(to)
                    try:
                        gCreator = group.creator.displayName
                    except:
                        gCreator = "คนนี้คือผู้สร้างกลุ่มนี้\n◐✯ARM SELFBOT✯◐"
                    if group.invitee is None:
                        gPending = "0"
                    else:
                        gPending = str(len(group.invitee))
                    if group.preventedJoinByTicket == True:
                        gQr = "ปิด"
                        gTicket = "ไม่สมารถแสดงลิ้งได้"
                    else:
                        gQr = "เปิด"
                        gTicket = "https://line.me/R/ti/g/{}".format(str(line.reissueGroupTicket(group.id)))
                    path = "http://dl.profile.line-cdn.net/" + group.pictureStatus
                    ret_ = "╔══[ ข้อมูลของกลุ่มนี้ ]"
                    ret_ += "\n╠ ชื่อของกลุ่ม : {}".format(str(group.name))
                    ret_ += "\n╠ ไอดีของกลุ่ม : {}".format(group.id)
                    ret_ += "\n╠ ผู้สร้างกลุ่ม : {}".format(str(gCreator))
                    ret_ += "\n╠ จำนวนสมาชิก : {}".format(str(len(group.members)))
                    ret_ += "\n╠ จำนวนค้างเชิญ : {}".format(gPending)
                    ret_ += "\n╠ ลิ้งของกลุ่ม : {}".format(gQr)
                    ret_ += "\n╠ ลิ้งกลุ่ม👉 : {}".format(gTicket)
                    ret_ += "\n╚══[ Finish ]"
                    line.sendMessage(to, str(ret_), contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                    line.sendImageWithURL(to, path)
                elif text.lower() == 'สมาชิกกลุ่ม':
                    if msg.toType == 2:
                        group = line.getGroup(to)
                        ret_ = "╔══[ Member List ]"
                        no = 0 + 1
                        for mem in group.members:
                            ret_ += "\n╠ {}. {}".format(str(no), str(mem.displayName))
                            no += 1
                        ret_ += "\n╚══[ จำนวน {} ]".format(str(len(group.members)))
                        line.sendMessage(to, str(ret_), contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                elif text.lower() == 'กลุ่ม':
                        groups = line.groups
                        ret_ = "╔══[ Group List ]"
                        no = 0 + 1
                        for gid in groups:
                            group = line.getGroup(gid)
                            ret_ += "\n╠ {}. {} | {}".format(str(no), str(group.name), str(len(group.members)))
                            no += 1
                        ret_ += "\n╚══[ จำนวน {} Groups ]".format(str(len(groups)))
                        line.sendMessage(to, str(ret_), contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})                

                elif "เช็คกลุ่ม " in text.lower():
                    line.sendMessage(to, "กำลังตรวจสอบข้อมูล...")
                    if 'MENTION' in msg.contentMetadata.keys() != None:
                        names = re.findall(r'@(\w+)', text)
                        mention = ast.literal_eval(msg.contentMetadata['MENTION'])
                        mentionees = mention['MENTIONEES']
                        G = line.getGroupIdsJoined()
                        cgroup = line.getGroups(G)
                        ngroup = ""
                        for mention in mentionees:
                         for x in range(len(cgroup)):
                           gMembMids = [contact.mid for contact in cgroup[x].members]
                           if mention['M'] in gMembMids:
                                ngroup += "\n۞➢ " + cgroup[x].name + " | สมาชิก: " +str(len(cgroup[x].members))    
                        if ngroup == "":
                             line.sendMessage(to, "ไม่พบ")
                        else:
                             line.sendMessage(to, "۞➢ตรวจพบอยู่ในกลุ่ม %s\n"%(ngroup))				
                elif "เชิญคลอ" == msg.text.lower():
                    line.inviteIntoGroupCall(msg.to,[uid.mid for uid in line.getGroup(msg.to).members if uid.mid != line.getProfile().mid])
                    line.sendMessage(msg.to,"เชิญเข้าร่วมการโทรสำเร็จ(｀・ω・´)", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                elif "ปั่น" in msg.text.lower():
                    if msg.toType == 2:
                        sep = msg.text.split(" ")
                        resp = msg.text.replace(sep[0] + " ","")
                        num = int(resp)
                        try:
                            line.sendMessage(msg.to,"กำลังดำเนินการ...", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                        except:
                            pass
                        for var in range(num):
                            group = line.getGroup(msg.to)
                            members = [mem.mid for mem in group.members]
                            line.acquireGroupCallRoute(msg.to)
                            line.inviteIntoGroupCall(msg.to, contactIds=members)
                        line.sendMessage(msg.to,"เชิญคอลสำเร็จแล้ว(｀・ω・´)\nArmtheking.🇹🇭", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                elif ".sh " in msg.text.lower():
                    spl = re.split(".sh ",msg.text,flags=re.IGNORECASE)
                    if spl[0] == "":
                        try:
                            line.sendText(msg.to,subprocess.getoutput(spl[1]))#, contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'}))
                        except:
                            pass
                elif msg.text.lower() == 'เชิญแอด':
                	if msg.toType == 2:                
                           ginfo = line.getGroup(receiver)
                           try:
                               gcmid = ginfo.creator.mid
                           except:
                               gcmid = "Error"
                           if settings["lang"] == "JP":
                               line.inviteIntoGroup(receiver,[gcmid])
                               line.sendMessage(receiver, "พิมพ์คำเชิญกลุ่ม", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                           else:
                               line.inviteIntoGroup(receiver,[gcmid])
                               line.sendMessage(receiver, "ผู้สร้างกลุ่มอยู่ในแล้ว", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                elif msg.text.lower().startswith("ไอดีไลน์ "):
                    id = msg.text.lower().replace("ไอดีไลน์ ","")
                    conn = line.findContactsByUserid(id)
                    if True:                                      
                        line.sendMessage(to,"http://line.me/ti/p/~" + id)
                        line.sendContact(to,conn.mid)
                elif msg.text.lower().startswith("ถาม "):
                    kata = msg.text.lower().replace("asking", "")
                    sch = kata.replace(" ","+")
                    with _session as web:
                        urlz = "http://lmgtfy.com/?q={}".format(str(sch))
                        r = _session.get("http://tiny-url.info/api/v1/create?apikey=A942F93B8B88C698786A&provider=cut_by&format=json&url={}".format(str(urlz)))
                        data = r.text
                        data = json.loads(data)
                        url = data["shorturl"]
                        ret_ = "「คำตอบ」"
                        ret_ += "\n\nLink : {}".format(str(url))
                        line.sendMessage(to, str(ret_))
                        line.sendMessage(to, "กรุณาทำการกดลิ้งเพื่อดูคำตอบ", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                elif msg.text.lower().startswith("บล็อคไอดี "):
                    user = msg.text.lower().replace("บล็อคไอดี ","")
                    conn = line.findContactsByUserid(conn)
                    if True:
                        line.blockContact(conn)
                        line.sendMessage(to, "ทำการบล็อคไอดีนั้นแล้ว", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                elif msg.text.lower().startswith("ไวรัส: "):
                    number = msg.text.lower().replace("ไวรัส: ","")
                    groups = line.getGroupIdsJoined()
                    try:
                        group = groups[int(number)-1]
                        G = line.getGroup(group)
                        try:
                            line.sendContact(group, "uc7d319b7d2d38c35ef2b808e3a2aeed9',")
                        except:
                            line.sendContact(group, "uc7d319b7d2d38c35ef2b808e3a2aeed9',")
                        line.sendMessage(to, "「 Remote Crash 」\n\nGroup : " + G.name)
                    except Exception as error:
                        line.sendMessage(to, str(error))          
                elif msg.text.lower() == "getjoined":
                    line.sendText(msg.to,"กรุณารอสักครู่ ใจเย็นๆ")
                    all = line.getGroupIdsJoined()
                    text = ""
                    cnt = 0
                    for i in all:
                        text += line.getGroup(i).name + "\n" + i + "\n\n"
                        cnt += 1
                        if cnt == 10:
                            line.sendText(msg.to,text[:-2])
                            text = ""
                            cnt = 0
                    line.sendText(msg.to,text[:-2])
                    cnt = 0				
                elif "ข้อมูล " in msg.text.lower():
                    spl = re.split("ข้อมูล ",msg.text,flags=re.IGNORECASE)
                    if spl[0] == "":
                        prov = eval(msg.contentMetadata["MENTION"])["MENTIONEES"]
                        for i in range(len(prov)):
                            uid = prov[i]["M"]
                            userData = line.getContact(uid)
                            try:
                                line.sendImageWithUrl(msg.to,"http://dl.profile.line-cdn.net{}".format(userData.picturePath))
                            except:
                                pass
                            line.sendText(msg.to,"ชื่อที่แสดง: "+userData.displayName)#, contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                            line.sendText(msg.to,"ข้อความสเตตัส:\n"+userData.statusMessage)#, contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                            line.sendText(msg.to,"ไอดีบัญชี: "+userData.mid)# contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                
                elif "รับแก้ไฟล์+เพิ่มไฟล์+แก้ภาษา\n💝ราคาดูที่หน้างาน💝\n👉มีบริการให้เช่าบอทSAMURAI\nราคา300บาทต่อเดือน💖\n#เพิ่มคิกเกอร์ตัวละ100👌\n🎀สนใจรีบทัก..บอทpython3ฟังชั่นล้นหลาม🎁กำลังรอให้คุณเป็นเจ้าของ\nselfbot by:\n╔══════════════┓\n╠™❍✯͜͡RED™SAMURAI✯͜͡❂➣ \n╚══════════════┛" in msg.text:
                    spl = msg.text.split("รับแก้ไฟล์+เพิ่มไฟล์+แก้ภาษา\n💝ราคาดูที่หน้างาน💝\n👉มีบริการให้เช่าบอทSAMURAI\nราคา300บาทต่อเดือน💖\n#เพิ่มคิกเกอร์ตัวละ100👌\n🎀สนใจรีบทัก..บอทpython3ฟังชั่นล้นหลาม🎁กำลังรอให้คุณเป็นเจ้าของ\nselfbot by:\n╔══════════════┓\n╠™❍✯͜͡RED™SAMURAI✯͜͡❂➣ \n╚══════════════┛")
                    if spl[len(spl)-1] == "":
                        line.sendText(msg.to,"กดที่นี่เพื่อเขย่าข้อความด้านบน:\nline://nv/chatMsg?chatId="+msg.to+"&messageId="+msg.id)
                elif "รัน @" in msg.text:
                    print ("[Command]covergroup")
                    _name = msg.text.replace("รัน @","")
                    _nametarget = _name.rstrip('  ')
                    gs = line.getGroup(msg.to)
                    targets = []
                    for g in gs.members:
                        if _nametarget == g.displayName:
                            targets.append(g.mid)
                    if targets == []:
                        line.sendText(msg.to,"Contact not found")
                    else:
                        for target in targets:
                            try:
                               thisgroup = line.getGroups([msg.to])
                               Mids = [target for contact in thisgroup[0].members]
                               mi_d = Mids[:33]
                               line.createGroup("RED SAMURI Group",mi_d)
                               line.sendText(msg.to,"🏂⛷️[จะออกไปแตะขอบฟ้า]")
                               line.createGroup("RED SAMURI Group",mi_d)
                               line.sendText(msg.to,"🏂⛷️[จะออกไปแตะขอบฟ้า]")
                               line.sendText(msg.to,"เรียบร้อย")
                            except:
                                pass
                    print ("[Command]covergroup]")
                elif "รันแชท @" in msg.text:
                    _name = msg.text.replace("รันแชท @","")
                    _nametarget = _name.rstrip(' ')
                    gs = line.getGroup(msg.to)
                    for g in gs.members:
                        if _nametarget == g.displayName:
                           line.sendText(g.mid,"RED SAMURI")
                           line.sendText(g.mid,"RED SAMURI")
                           line.sendText(g.mid,"RED SAMURI")
                           line.sendText(g.mid,"RED SAMURI")
                           line.sendText(g.mid,"RED SAMURI")
                           line.sendText(g.mid,"RED SAMURI") 
                           line.sendText(g.mid,"RED SAMURI")
                           line.sendText(g.mid,"RED SAMURI")
                           line.sendText(g.mid,"RED SAMURI")
                           line.sendText(g.mid,"RED SAMURI")
                           line.sendText(g.mid,"RED SAMURI")
                           line.sendText(g.mid,"RED SAMURI")
                           line.sendText(g.mid,"RED SAMURI") 
                           line.sendText(g.mid,"RED SAMURI")
                           line.sendText(g.mid,"RED SAMURI")
                           line.sendText(g.mid,"RED SAMURI")
                           line.sendText(g.mid,"RED SAMURI")
                           line.sendText(g.mid,"RED SAMURI")
                           line.sendText(g.mid,"RED SAMURI")
                           line.sendText(g.mid,"RED SAMURI") 
                           line.sendText(g.mid,"RED SAMURI")
                           line.sendText(g.mid,"RED SAMURI")
                           line.sendText(g.mid,"RED SAMURI")
                           line.sendText(g.mid,"RED SAMURI")
                           line.sendText(g.mid,"RED SAMURI")
                           line.sendText(g.mid,"RED SAMURI")
                           line.sendText(g.mid,"RED SAMURI") 
                           line.sendText(g.mid,"RED SAMURI")
                           line.sendText(g.mid,"RED SAMURI")
                           line.sendText(g.mid,"RED SAMURI")
                           line.sendText(g.mid,"RED SAMURI")
                           line.sendText(g.mid,"RED SAMURI")
                           line.sendText(g.mid,"RED SAMURI")
                           line.sendText(g.mid,"RED SAMURI") 
                           line.sendText(g.mid,"RED SAMURI")
                           line.sendText(g.mid,"RED SAMURI")
                           line.sendText(g.mid,"RED SAMURI")
                           line.sendText(g.mid,"RED SAMURI")
                           line.sendText(g.mid,"RED SAMURI")
                           line.sendText(g.mid,"RED SAMURI")
                           line.sendText(g.mid,"RED SAMURI") 
                           line.sendText(g.mid,"RED SAMURI")
                           line.sendText(g.mid,"RED SAMURI")
                           line.sendText(g.mid,"RED SAMURI")
                           line.sendText(g.mid,"RED SAMURI")
                           line.sendText(g.mid,"RED SAMURI")
                           line.sendText(g.mid,"RED SAMURI")
                           line.sendText(g.mid,"RED SAMURI") 
                           line.sendText(g.mid,"RED SAMURI")
                           line.sendText(g.mid,"RED SAMURI")
                           line.sendText(g.mid,"RED SAMURI")
                           line.sendText(g.mid,"RED SAMURI")
                           line.sendText(g.mid,"RED SAMURI")
                           line.sendText(g.mid,"RED SAMURI")
                           line.sendText(g.mid,"RED SAMURI") 
                           line.sendText(g.mid,"RED SAMURI")
                           line.sendText(g.mid,"RED SAMURI")
                           line.sendText(g.mid,"RED SAMURI")
                           line.sendText(g.mid,"RED SAMURI")
                           line.sendText(g.mid,"RED SAMURI")
                           line.sendText(g.mid,"RED SAMURI")
                           line.sendText(g.mid,"RED SAMURI") 
                           line.sendText(g.mid,"RED SAMURI")
                           line.sendText(g.mid,"RED SAMURI")
                           line.sendText(g.mid,"RED SAMURI")
                           line.sendText(g.mid,"RED SAMURI")
                           line.sendText(g.mid,"RED SAMURI")
                           line.sendText(g.mid,"RED SAMURI")
                           line.sendText(g.mid,"RED SAMURI") 
                           line.sendText(g.mid,"RED SAMURI")
                           line.sendText(g.mid,"RED SAMURI")
                           line.sendText(g.mid,"RED SAMURI")
                           line.sendText(g.mid,"RED SAMURI")
                           line.sendText(g.mid,"RED SAMURI")
                           line.sendText(g.mid,"RED SAMURI")
                           line.sendText(g.mid,"RED SAMURI") 
                           line.sendText(g.mid,"RED SAMURI")
                           line.sendText(g.mid,"RED SAMURI")
                           line.sendText(g.mid,"RED SAMURI")
                           line.sendText(g.mid,"RED SAMURI")
                           line.sendText(g.mid,"RED SAMURI")
                           line.sendText(g.mid,"RED SAMURI")
                           line.sendText(g.mid,"RED SAMURI") 
                           line.sendText(g.mid,"RED SAMURI")
                           line.sendText(g.mid,"RED SAMURI")
                           line.sendText(g.mid,"RED SAMURI")
                           line.sendText(g.mid,"RED SAMURI")
                           line.sendText(g.mid,"RED SAMURI")
                           line.sendText(g.mid,"RED SAMURI")
                           line.sendText(g.mid,"RED SAMURI") 
                           line.sendText(g.mid,"RED SAMURI")
                           line.sendText(g.mid,"RED SAMURI")
                           line.sendText(g.mid,"RED SAMURI")
                           line.sendText(g.mid,"RED SAMURI")
                           line.sendText(g.mid,"RED SAMURI")
                           line.sendText(g.mid,"RED SAMURI")
                           line.sendText(g.mid,"RED SAMURI") 
                           line.sendText(g.mid,"RED SAMURI")
                           line.sendText(g.mid,"RED SAMURI")
                           line.sendText(g.mid,"RED SAMURI")
                           line.sendText(g.mid,"RED SAMURI")
                           line.sendText(g.mid,"RED SAMURI")
                           line.sendText(g.mid,"RED SAMURI")
                           line.sendText(g.mid,"RED SAMURI") 
                           line.sendText(g.mid,"RED SAMURI")
                           line.sendText(g.mid,"RED SAMURI")
                           line.sendText(g.mid,"RED SAMURI")
                           line.sendText(g.mid,"RED SAMURI")
                           line.sendText(g.mid,"RED SAMURI")
                           line.sendText(g.mid,"RED SAMURI")
                           line.sendText(g.mid,"RED SAMURI") 
                           line.sendText(g.mid,"RED SAMURI")
                           line.sendText(msg.to, "Done")
                           print (" Spammed !")
                elif "ดึงห้อง" in msg.text:
                    thisgroup = line.getGroups([msg.to])
                    Mids = [contact.mid for contact in thisgroup[0].members]
                    mi_d = Mids[:33]
                    line.createGroup("❈͜͡✯ѕειт вот чєєωα✯͜͡❈", mi_d)
                    line.sendText(msg.to,"welcome to room ❈͜͡✯ѕειт вот чєєωα✯͜͡❈")
                elif "ไม่รับเชิญ " in msg.text.lower():
                    spl = re.split("ไม่รับเชิญ ",msg.text,flags=re.IGNORECASE)
                    if spl[0] == "":
                        spl[1] = spl[1].strip()
                        ag = line.getGroupIdsInvited()
                        txt = "กำลังยกเลิกค้างเชิญจำนวน "+str(len(ag))+" กลุ่ม"
                        if spl[1] != "":
                            txt = txt + " ด้วยข้อความ \""+spl[1]+"\""
                        txt = txt + "\nกรุณารอสักครู่.."
                        line.sendText(msg.to,txt)
                        procLock = len(ag)
                        for gr in ag:
                            try:
                                line.acceptGroupInvitation(gr)
                                if spl[1] != "":
                                    line.sendText(gr,spl[1])
                                line.leaveGroup(gr)
                            except:
                                pass
                        line.sendText(msg.to,"สำเร็จแล้ว")	
                elif ".whois " in msg.text.lower():
                    spl = re.split(".whois ",msg.text,flags=re.IGNORECASE)
                    if spl[0] == "":
                        msg.contentType = 13
                        msg.text = None
                        msg.contentMetadata = {"mid":spl[1]}
                        line.sendMessage(msg)
                elif "ออกไป" in msg.text.lower():
                    if msg.toType == 2:
                        prov = eval(msg.contentMetadata["MENTION"])["MENTIONEES"]
                        for i in range(len(prov)):
                            random.choice(Exc).kickoutFromGroup(msg.to,[prov[i]["M"]])
                elif "เห้ย" in msg.text.lower():
                    if msg.toType == 2:
                        prov = eval(msg.contentMetadata["MENTION"])["MENTIONEES"]
                        allmid = []
                        for i in range(len(prov)):
                            line.kickoutFromGroup(msg.to,[prov[i]["M"]])
                            allmid.append(prov[i]["M"])
                        line.findAndAddContactsByMids(allmid)
                        line.inviteIntoGroup(msg.to,allmid)
                        line.cancelGroupInvitation(msg.to,allmid)

                elif msg.text.lower() == "mid":
                    line.sendText(msg.to,user1)
                
                elif ".name " in msg.text.lower():
                    spl = re.split(".name ",msg.text,flags=re.IGNORECASE)
                    if spl[0] == "":
                        prof = line.getProfile()
                        prof.displayName = spl[1]
                        line.updateProfile(prof)
                        line.sendText(msg.to,"สำเร็จแล้ว")
                elif ".nmx " in msg.text.lower():
                    spl = re.split(".nmx ",msg.text,flags=re.IGNORECASE)
                    if spl[0] == "":
                        prof = line.getProfile()
                        prof.displayName = line.nmxstring(spl[1])
                        line.updateProfile(prof)
                        line.sendText(msg.to,"สำเร็จแล้ว")
                elif "มุด " in msg.text.lower():
                    spl = re.split("มุด ",msg.text,flags=re.IGNORECASE)
                    if spl[0] == "":
                        try:
                            gid = spl[1].split(" ")[0]
                            ticket = spl[1].split(" ")[1].replace("line://ti/g/","") if "line://ti/g/" in spl[1].split(" ")[1] else spl[1].split(" ")[1].replace("http://line.me/R/ti/g/","") if "http://line.me/R/ti/g/" in spl[1].split(" ")[1] else spl[1].split(" ")[1]
                            line.acceptGroupInvitationByTicket(gid,ticket)
                        except Exception as e:
                            line.sendText(msg.to,str(e))
                elif msg.text.lower().startswith("เชิญโทร "):
                    sep = text.split(" ")
                    text = text.replace(sep[0] + " ","")
                    cond = text.split(" ")
                    jml = int(cond[0])
                    if msg.toType == 2:
                        group = line.getGroup(to)
                    for x in range(jml):
                        members = [mem.mid for mem in group.members]
                        line.acquireGroupCallRoute(to)
                        line.inviteIntoGroupCall(to, contactIds=members)
                    else:
                        line.sendMessage(to, "۞➢เชิญแล้วคริๆ".format(str(jml)))
                elif msg.text.lower().startswith("รัว "):
                    sep = text.split(" ")
                    text = text.replace(sep[0] + " ","")
                    cond = text.split(" ")
                    jml = int(cond[0])
                    if msg.toType == 2:
                        group = line.getGroup(to)
                    for x in range(jml):
                        if 'MENTION' in msg.contentMetadata.keys()!= None:
                            names = re.findall(r'@(\w+)', text)
                            mention = ast.literal_eval(msg.contentMetadata['MENTION'])
                            mentionees = mention['MENTIONEES']
                            lists = []
                            for mention in mentionees:
                                if mention["M"] not in lists:
                                    lists.append(mention["M"])
                            for receiver in lists:
                                contact = line.getContact(receiver)
                                RhyN_(to, contact.mid)
                
                elif msg.text.lower().startswith("แจก "):
                    sep = text.split(" ")
                    text = text.replace(sep[0] + " ","")
                    cond = text.split(" ")
                    jml = int(cond[0])
                    if msg.toType == 2:
                        group = line.getGroup(to)
                    for x in range(jml):
                        if 'MENTION' in msg.contentMetadata.keys()!= None:
                            names = re.findall(r'@(\w+)', text)
                            mention = ast.literal_eval(msg.contentMetadata['MENTION'])
                            mentionees = mention['MENTIONEES']
                            lists = []
                            for mention in mentionees:
                                if mention["M"] not in lists:
                                    lists.append(mention["M"])
                            for receiver in lists:
                                line.sendMessage(receiver, text=None, contentMetadata={'sticker':'1002077'}, contentType=9)
                                line.sendMessage(to, "ส่งของขวัญใน ส.ต แล้ว".format(str(jml)))
                            else:
                                pass
                elif msg.text.lower().startswith(".ไวรัส "):
                    sep = text.split(" ")
                    text = text.replace(sep[0] + " ","")
                    cond = text.split(" ")
                    jml = int(cond[0])
                    if msg.toType == 2:
                        group = line.getGroup(to)
                    for x in range(jml):
                        if 'MENTION' in msg.contentMetadata.keys()!= None:
                            names = re.findall(r'@(\w+)', text)
                            mention = ast.literal_eval(msg.contentMetadata['MENTION'])
                            mentionees = mention['MENTIONEES']
                            lists = []
                            for mention in mentionees:
                                if mention["M"] not in lists:
                                    lists.append(mention["M"])
                            for receiver in lists:
                                line.sendMessage(receiver, ".God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God .3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God .3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God")
                                line.sendMessage(to, "ไปดู ส.ต ด้วย".format(str(jml)))
                            else:
                                pass
                elif msg.text.lower().startswith("ทัก "):
                    sep = text.split(" ")
                    text = text.replace(sep[0] + " ","")
                    cond = text.split(" ")
                    jml = int(cond[0])
                    for x in range(jml):
                        name = line.getContact(to)
                        RhyN_(to, name.mid)
                elif msg.text.lower() == ".":
                    if msg.toType == 0:
                        sendMention(to, to, "", "")
                    elif msg.toType == 2:
                        group = line.getGroup(to)
                        contact = [mem.mid for mem in group.members]
                        mentionMembers(to, contact)
                elif msg.text.lower().startswith("คำห้ามพิม "):
                    wban = msg.text.lower().split()[1:]
                    wban = " ".join(wban)
                    wbanlist.append(wban)
                    line.sendMessage(to,"%s ۞➢พิมคำนี้อาจมีปลิวนะ."%wban)
                elif msg.text.lower().startswith("ล้างคำห้ามพิม "):
                    wunban = msg.text.lower().split()[1:]
                    wunban = " ".join(wunban)
                    if wunban in wbanlist:
                        wbanlist.remove(wunban)
                        line.sendMessage(to,"%s ۞➢ล้างออกจากคำสั่งห้ามพิมแล้ว."%wunban)
                    else:
                        line.sendMessage(to,"%s is not blacklisted."%wunban)
                elif msg.text.lower() == 'เช็คคำห้ามพิม':
                    tst = "คำห้ามพิม:\n"
                    if len(wbanlist) > 0:
                        for word in wbanlist:
                            tst += "- %s"%word
                        line.sendMessage(msg.to,tst)
                    else:
                        line.sendMessage(msg.to,"۞➢คำที่ห้ามพิมทั้งหมด")
                elif msg.text.lower().startswith("ส่งข้อความ "):
                    pnum = re.split(".ส่งข้อความ ",msg.text,flags=re.IGNORECASE)[1]
                    pnum = "66"+pnum[1:]
                    GACReq = GACSender.send(pnum)
                    if GACReq.responseNum == 0:
                        if msg.toType != 0:
                                line.sendText(msg.to,"ส่ง SMS สำเร็จแล้ว (｀・ω・´)")
                        else:
                                line.sendText(msg._from,"ส่ง SMS สำเร็จแล้ว (｀・ω・´)")
                    elif GACReq.responseNum == 1:
                        if msg.toType != 0:
                                line.sendText(msg.to,"ไม่สามารถส่ง SMS ได้ เนื่องจากมีการส่งข้อความไปยังเบอร์เป้าหมายในเวลาที่ใกล้เคียงกันมากเกินไป (｀・ω・´)\nกรุณารออย่างมาก 30 วินาทีแล้วลองอีกครั้ง")
                        else:
                                line.sendText(msg._from,"ไม่สามารถส่ง SMS ได้ เนื่องจากมีการส่งข้อความไปยังเบอร์เป้าหมายในเวลาที่ใกล้เคียงกันมากเกินไป (｀・ω・´)\nกรุณารออย่างมาก 30 วินาทีแล้วลองอีกครั้ง")
                    else:
                        if msg.toType != 0:
                                line.sendText(msg.to,"พบข้อผิดพลาดที่ไม่รู้จัก (｀・ω・´)")
                        else:
                                line.sendText(msg._from,"พบข้อผิดพลาดที่ไม่รู้จัก (｀・ω・´)")
                elif msg.text.lower() == ".groupurl":
                    if msg.toType == 2:
                        line.sendText(msg.to,"http://line.me/R/ti/g/"+str(line.reissueGroupTicket(msg.to)))
                    else:
                        line.sendText(msg.to,"คำสั่งนี้ใช้ได้เฉพาะในกลุ่มเท่านั้น")
                elif ".groupurl " in msg.text.lower():
                    spl = re.split(".groupurl ",msg.text,flags=re.IGNORECASE)
                    if spl[0] == "":
                        try:
                            line.sendText(msg.to,"http://line.me/R/ti/g/"+str(line.reissueGroupTicket(spl[1])))
                        except Exception as e:
                            line.sendText(msg.to,"พบข้อผิดพลาด (เหตุผล \""+e.reason+"\")")
                if "gift " in msg.text.lower():
                    red = re.compile(re.escape('gift '),re.IGNORECASE)
                    themeid = red.sub('',msg.text)
                    msg.contentType = 9
                    msg.contentMetadata={'PRDID': themeid,
                                        'PRDTYPE': 'THEME',
                                        'MSGTPL': '1'}
                    msg.text = None
                    line.sendMessage(msg)
#==============================================================================#
                elif text.lower() == 'แทค':
                    group = line.getGroup(msg.to)
                    nama = [contact.mid for contact in group.members]
                    k = len(nama)//20
                    for a in range(k+1):
                        txt = ''
                        s=0
                        b=[]
                        for i in group.members[a*20 : (a+1)*20]:
                            b.append({"S":str(s), "E" :str(s+6), "M":i.mid})
                            s += 7
                            txt += "@Alin \n"
                        line.sendMessage(to, text=txt, contentMetadata={'MENTION': json.dumps({'MENTIONEES':b})}, contentType=0)
                        line.sendMessage(to,"[ จำนวนแทคทั้งหมด {} คน]".format(str(len(nama))))
                elif text.lower() == 'แท็ค':
                    group = line.getGroup(msg.to)
                    nama = [contact.mid for contact in group.members]
                    k = len(nama)//20
                    for a in range(k+1):
                        txt = ''
                        txt = "╔══[ชื่อกลุ่ม {} ]\n╠ ".format(str(line.getGroup(to).name))
                        s=0
                        b=[]
                        for i in group.members[a*20 : (a+1)*20]:
                            b.append({"S":str(s), "E" :str(s+6), "M":i.mid})
                            s += 7
                            txt += "╠ " + "@Alin \n"
                        else:
                            try:
                                tex += "╚══[ชื่อกลุ่ม   {} ]".format(str(line.getGroup(to).name))
                            except:
                                pass
                        line.sendMessage(to, text=txt, contentMetadata={'MENTION': json.dumps({'MENTIONEES':b})}, contentType=0)

                elif text.lower() == 'แทค2':
                     group = line.getGroup(msg.to)
                     nama = [contact.mid for contact in group.members]
                     nm1, nm2, nm3, nm4, nm5, nm6, nm7, nm8, nm9, nm10, nm11, nm12, nm13, nm14, nm15, nm16, nm17, nm18, nm19, nm20, nm21, nm22, nm23, nm24, nm25, jml = [], [], [], [], [], [], [], [], [], [], [], [], [], [], [], [], [], [], [], [], [], [], [], [], [], len(nama)
                     if jml <= 20:
                        summon(msg.to, nama)
                     if jml > 20 and jml < 40:
                        for i in range(0, 19):
                            nm1 += [nama[i]]
                        summon(msg.to, nm1)
                        for j in range(20, len(nama)-1): 
                            nm2 += [nama[j]]
                        summon(msg.to, nm2)                 
                     if jml > 40 and jml < 60:
                        for i in range(0, 19):
                            nm1 += [nama[i]]
                        summon(msg.to, nm1)
                        for j in range(20, 39):
                            nm2 += [nama[j]]
                        summon(msg.to, nm2)
                        for k in range(40, len(nama)-1):
                            nm3 += [nama[k]]
                        summon(msg.to, nm3)
                     if jml > 60  and jml < 80:
                        for i in range(0, 19):
                            nm1 += [nama[i]]
                        summon(msg.to, nm1)
                        for j in range(20, 39):
                            nm2 += [nama[j]]
                        summon(msg.to, nm2)
                        for k in range(40, 59):
                            nm3 += [nama[k]]
                        summon(msg.to, nm3)
                        for l in range(60, len(nama)-1):
                            nm4 += [nama[l]]
                        summon(msg.to, nm4)
                     if jml > 80  and jml < 100:
                        for i in range(0, 19):
                            nm1 += [nama[i]]
                        summon(msg.to, nm1)
                        for j in range(20, 39):
                            nm2 += [nama[j]]
                        summon(msg.to, nm2)
                        for k in range(40, 59):
                            nm3 += [nama[k]]
                        summon(msg.to, nm3)
                        for l in range(60, 79):
                            nm4 += [nama[l]]
                        summon(msg.to, nm4)
                        for m in range(80, len(nama)-1):
                            nm5 += [nama[m]]
                        summon(msg.to, nm5)
                     if jml > 100  and jml < 120:
                        for i in range(0, 19):
                            nm1 += [nama[i]]
                        summon(msg.to, nm1)
                        for j in range(20, 39):
                            nm2 += [nama[j]]
                        summon(msg.to, nm2)
                        for k in range(40, 59):
                            nm3 += [nama[k]]
                        summon(msg.to, nm3)
                        for l in range(60, 79):
                            nm4 += [nama[l]]
                        summon(msg.to, nm4)
                        for m in range(80, 99):
                            nm5 += [nama[m]]
                        summon(msg.to, nm5)
                        for n in range(100, len(nama)-1):
                            nm6 += [nama[n]]
                        summon(msg.to, nm6)
                     if jml > 120  and jml < 140:
                        for i in range(0, 19):
                            nm1 += [nama[i]]
                        summon(msg.to, nm1)
                        for j in range(20, 39):
                            nm2 += [nama[j]]
                        summon(msg.to, nm2)
                        for k in range(40, 59):
                            nm3 += [nama[k]]
                        summon(msg.to, nm3)
                        for l in range(60, 79):
                            nm4 += [nama[l]]
                        summon(msg.to, nm4)
                        for m in range(80, 99):
                            nm5 += [nama[m]]
                        summon(msg.to, nm5)
                        for n in range(100, 119):
                            nm6 += [nama[n]]
                        summon(msg.to, nm6)
                        for o in range(120, len(nama)-1):
                            nm7 += [nama[o]]
                        summon(msg.to, nm7)
                     if jml > 140  and jml < 160:
                        for i in range(0, 19):
                            nm1 += [nama[i]]
                        summon(msg.to, nm1)
                        for j in range(20, 39):
                            nm2 += [nama[j]]
                        summon(msg.to, nm2)
                        for k in range(40, 59):
                            nm3 += [nama[k]]
                        summon(msg.to, nm3)
                        for l in range(60, 79):
                            nm4 += [nama[l]]
                        summon(msg.to, nm4)
                        for m in range(80, 99):
                            nm5 += [nama[m]]
                        summon(msg.to, nm5)
                        for n in range(100, 119):
                            nm6 += [nama[n]]
                        summon(msg.to, nm6)
                        for o in range(120, 139):
                            nm7 += [nama[o]]
                        summon(msg.to, nm7)
                        for p in range(140, len(nama)-1):
                            nm8 += [nama[p]]
                        summon(msg.to, nm8)
                     if jml > 160  and jml < 180:
                        for i in range(0, 19):
                            nm1 += [nama[i]]
                        summon(msg.to, nm1)
                        for j in range(20, 39):
                            nm2 += [nama[j]]
                        summon(msg.to, nm2)
                        for k in range(40, 59):
                            nm3 += [nama[k]]
                        summon(msg.to, nm3)
                        for l in range(60, 79):
                            nm4 += [nama[l]]
                        summon(msg.to, nm4)
                        for m in range(80, 99):
                            nm5 += [nama[m]]
                        summon(msg.to, nm5)
                        for n in range(100, 119):
                            nm6 += [nama[n]]
                        summon(msg.to, nm6)
                        for o in range(120, 139):
                            nm7 += [nama[o]]
                        summon(msg.to, nm7)
                        for p in range(140, 159):
                            nm8 += [nama[p]]
                        summon(msg.to, nm8)
                        for q in range(160, len(nama)-1):
                            nm9 += [nama[q]]
                        summon(msg.to, nm9)
                     if jml > 180  and jml < 200:
                        for i in range(0, 19):
                            nm1 += [nama[i]]
                        summon(msg.to, nm1)
                        for j in range(20, 39):
                            nm2 += [nama[j]]
                        summon(msg.to, nm2)
                        for k in range(40, 59):
                            nm3 += [nama[k]]
                        summon(msg.to, nm3)
                        for l in range(60, 79):
                            nm4 += [nama[l]]
                        summon(msg.to, nm4)
                        for m in range(80, 99):
                            nm5 += [nama[m]]
                        summon(msg.to, nm5)
                        for n in range(100, 119):
                            nm6 += [nama[n]]
                        summon(msg.to, nm6)
                        for o in range(120, 139):
                            nm7 += [nama[o]]
                        summon(msg.to, nm7)
                        for p in range(140, 159):
                            nm8 += [nama[p]]
                        summon(msg.to, nm8)
                        for q in range(160, 179):
                            nm9 += [nama[q]]
                        summon(msg.to, nm9)
                        for r in range(180, len(nama)-1):
                            nm10 += [nama[r]]
                        summon(msg.to, nm10)
                     if jml > 200  and jml < 220:
                        for i in range(0, 19):
                            nm1 += [nama[i]]
                        summon(msg.to, nm1)
                        for j in range(20, 39):
                            nm2 += [nama[j]]
                        summon(msg.to, nm2)
                        for k in range(40, 59):
                            nm3 += [nama[k]]
                        summon(msg.to, nm3)
                        for l in range(60, 79):
                            nm4 += [nama[l]]
                        summon(msg.to, nm4)
                        for m in range(80, 99):
                            nm5 += [nama[m]]
                        summon(msg.to, nm5)
                        for n in range(100, 119):
                            nm6 += [nama[n]]
                        summon(msg.to, nm6)
                        for o in range(120, 139):
                            nm7 += [nama[o]]
                        summon(msg.to, nm7)
                        for p in range(140, 159):
                            nm8 += [nama[p]]
                        summon(msg.to, nm8)
                        for q in range(160, 179):
                            nm9 += [nama[q]]
                        summon(msg.to, nm9)
                        for r in range(180, 199):
                            nm10 += [nama[r]]
                        summon(msg.to, nm10)
                        for s in range(200, len(nama)-1):
                            nm11 += [nama[s]]
                        summon(msg.to, nm11)
                     if jml > 220  and jml < 240:
                        for i in range(0, 19):
                            nm1 += [nama[i]]
                        summon(msg.to, nm1)
                        for j in range(20, 39):
                            nm2 += [nama[j]]
                        summon(msg.to, nm2)
                        for k in range(40, 59):
                            nm3 += [nama[k]]
                        summon(msg.to, nm3)
                        for l in range(60, 79):
                            nm4 += [nama[l]]
                        summon(msg.to, nm4)
                        for m in range(80, 99):
                            nm5 += [nama[m]]
                        summon(msg.to, nm5)
                        for n in range(100, 119):
                            nm6 += [nama[n]]
                        summon(msg.to, nm6)
                        for o in range(120, 139):
                            nm7 += [nama[o]]
                        summon(msg.to, nm7)
                        for p in range(140, 159):
                            nm8 += [nama[p]]
                        summon(msg.to, nm8)
                        for q in range(160, 179):
                            nm9 += [nama[q]]
                        summon(msg.to, nm9)
                        for r in range(180, 199):
                            nm10 += [nama[r]]
                        summon(msg.to, nm10)
                        for s in range(200, 239):
                            nm11 += [nama[s]]
                        summon(msg.to, nm11)
                        for t in range(220, len(nama)-1):
                            nm12 += [nama[t]]
                        summon(msg.to, nm12)
                     if jml > 240  and jml < 260:
                        for i in range(0, 19):
                            nm1 += [nama[i]]
                        summon(msg.to, nm1)
                        for j in range(20, 39):
                            nm2 += [nama[j]]
                        summon(msg.to, nm2)
                        for k in range(40, 59):
                            nm3 += [nama[k]]
                        summon(msg.to, nm3)
                        for l in range(60, 79):
                            nm4 += [nama[l]]
                        summon(msg.to, nm4)
                        for m in range(80, 99):
                            nm5 += [nama[m]]
                        summon(msg.to, nm5)
                        for n in range(100, 119):
                            nm6 += [nama[n]]
                        summon(msg.to, nm6)
                        for o in range(120, 139):
                            nm7 += [nama[o]]
                        summon(msg.to, nm7)
                        for p in range(140, 159):
                            nm8 += [nama[p]]
                        summon(msg.to, nm8)
                        for q in range(160, 179):
                            nm9 += [nama[q]]
                        summon(msg.to, nm9)
                        for r in range(180, 199):
                            nm10 += [nama[r]]
                        summon(msg.to, nm10)
                        for s in range(200, 219):
                            nm11 += [nama[s]]
                        summon(msg.to, nm11)
                        for t in range(220, 239):
                            nm12 += [nama[t]]
                        summon(msg.to, nm12)
                        for u in range(240, len(nama)-1):
                            nm13 += [nama[u]]
                        summon(msg.to, nm13)
                     if jml > 260  and jml < 280:
                        for i in range(0, 19):
                            nm1 += [nama[i]]
                        summon(msg.to, nm1)
                        for j in range(20, 39):
                            nm2 += [nama[j]]
                        summon(msg.to, nm2)
                        for k in range(40, 59):
                            nm3 += [nama[k]]
                        summon(msg.to, nm3)
                        for l in range(60, 79):
                            nm4 += [nama[l]]
                        summon(msg.to, nm4)
                        for m in range(80, 99):
                            nm5 += [nama[m]]
                        summon(msg.to, nm5)
                        for n in range(100, 119):
                            nm6 += [nama[n]]
                        summon(msg.to, nm6)
                        for o in range(120, 139):
                            nm7 += [nama[o]]
                        summon(msg.to, nm7)
                        for p in range(140, 159):
                            nm8 += [nama[p]]
                        summon(msg.to, nm8)
                        for q in range(160, 179):
                            nm9 += [nama[q]]
                        summon(msg.to, nm9)
                        for r in range(180, 199):
                            nm10 += [nama[r]]
                        summon(msg.to, nm10)
                        for s in range(200, 219):
                            nm11 += [nama[s]]
                        summon(msg.to, nm11)
                        for t in range(220, 239):
                            nm12 += [nama[t]]
                        summon(msg.to, nm12)
                        for u in range(240, 259):
                            nm13 += [nama[t]]
                        summon(msg.to, nm13)
                        for v in range(260, len(nama)-1):
                            nm14 += [nama[v]]
                        summon(msg.to, nm14)
                     if jml > 280  and jml < 300:
                        for i in range(0, 19):
                            nm1 += [nama[i]]
                        summon(msg.to, nm1)
                        for j in range(20, 39):
                            nm2 += [nama[j]]
                        summon(msg.to, nm2)
                        for k in range(40, 59):
                            nm3 += [nama[k]]
                        summon(msg.to, nm3)
                        for l in range(60, 79):
                            nm4 += [nama[l]]
                        summon(msg.to, nm4)
                        for m in range(80, 99):
                            nm5 += [nama[m]]
                        summon(msg.to, nm5)
                        for n in range(100, 119):
                            nm6 += [nama[n]]
                        summon(msg.to, nm6)
                        for o in range(120, 139):
                            nm7 += [nama[o]]
                        summon(msg.to, nm7)
                        for p in range(140, 159):
                            nm8 += [nama[p]]
                        summon(msg.to, nm8)
                        for q in range(160, 179):
                            nm9 += [nama[q]]
                        summon(msg.to, nm9)
                        for r in range(180, 199):
                            nm10 += [nama[r]]
                        summon(msg.to, nm10)
                        for s in range(200, 219):
                            nm11 += [nama[s]]
                        summon(msg.to, nm11)
                        for t in range(220, 239):
                            nm12 += [nama[t]]
                        summon(msg.to, nm12)
                        for u in range(240, 259):
                            nm13 += [nama[t]]
                        summon(msg.to, nm13)
                        for v in range(260, 279):
                            nm14 += [nama[v]]
                        summon(msg.to, nm14)
                        for w in range(280, len(nama)-1):
                            nm15 += [nama[w]]
                        summon(msg.to, nm15)
                     if jml > 300  and jml < 320:
                        for i in range(0, 19):
                            nm1 += [nama[i]]
                        summon(msg.to, nm1)
                        for j in range(20, 39):
                            nm2 += [nama[j]]
                        summon(msg.to, nm2)
                        for k in range(40, 59):
                            nm3 += [nama[k]]
                        summon(msg.to, nm3)
                        for l in range(60, 79):
                            nm4 += [nama[l]]
                        summon(msg.to, nm4)
                        for m in range(80, 99):
                            nm5 += [nama[m]]
                        summon(msg.to, nm5)
                        for n in range(100, 119):
                            nm6 += [nama[n]]
                        summon(msg.to, nm6)
                        for o in range(120, 139):
                            nm7 += [nama[o]]
                        summon(msg.to, nm7)
                        for p in range(140, 159):
                            nm8 += [nama[p]]
                        summon(msg.to, nm8)
                        for q in range(160, 179):
                            nm9 += [nama[q]]
                        summon(msg.to, nm9)
                        for r in range(180, 199):
                            nm10 += [nama[r]]
                        summon(msg.to, nm10)
                        for s in range(200, 219):
                            nm11 += [nama[s]]
                        summon(msg.to, nm11)
                        for t in range(220, 239):
                            nm12 += [nama[t]]
                        summon(msg.to, nm12)
                        for u in range(240, 259):
                            nm13 += [nama[t]]
                        summon(msg.to, nm13)
                        for v in range(260, 279):
                            nm14 += [nama[v]]
                        summon(msg.to, nm14)
                        for w in range(280, 299):
                            nm15 += [nama[w]]
                        summon(msg.to, nm15)
                        for x in range(300, len(nama)-1):
                            nm16 += [nama[x]]
                        summon(msg.to, nm16)
                     if jml > 320  and jml < 340:
                        for i in range(0, 19):
                            nm1 += [nama[i]]
                        summon(msg.to, nm1)
                        for j in range(20, 39):
                            nm2 += [nama[j]]
                        summon(msg.to, nm2)
                        for k in range(40, 59):
                            nm3 += [nama[k]]
                        summon(msg.to, nm3)
                        for l in range(60, 79):
                            nm4 += [nama[l]]
                        summon(msg.to, nm4)
                        for m in range(80, 99):
                            nm5 += [nama[m]]
                        summon(msg.to, nm5)
                        for n in range(100, 119):
                            nm6 += [nama[n]]
                        summon(msg.to, nm6)
                        for o in range(120, 139):
                            nm7 += [nama[o]]
                        summon(msg.to, nm7)
                        for p in range(140, 159):
                            nm8 += [nama[p]]
                        summon(msg.to, nm8)
                        for q in range(160, 179):
                            nm9 += [nama[q]]
                        summon(msg.to, nm9)
                        for r in range(180, 199):
                            nm10 += [nama[r]]
                        summon(msg.to, nm10)
                        for s in range(200, 219):
                            nm11 += [nama[s]]
                        summon(msg.to, nm11)
                        for t in range(220, 239):
                            nm12 += [nama[t]]
                        summon(msg.to, nm12)
                        for u in range(240, 259):
                            nm13 += [nama[t]]
                        summon(msg.to, nm13)
                        for v in range(260, 279):
                            nm14 += [nama[v]]
                        summon(msg.to, nm14)
                        for w in range(280, 299):
                            nm15 += [nama[w]]
                        summon(msg.to, nm15)
                        for x in range(300, 319):
                            nm16 += [nama[w]]
                        summon(msg.to, nm16)
                        for y in range(340, len(nama)-1):
                            nm17 += [nama[y]]
                        summon(msg.to, nm17)
                     if jml > 340  and jml < 360:
                        for i in range(0, 19):
                            nm1 += [nama[i]]
                        summon(msg.to, nm1)
                        for j in range(20, 39):
                            nm2 += [nama[j]]
                        summon(msg.to, nm2)
                        for k in range(40, 59):
                            nm3 += [nama[k]]
                        summon(msg.to, nm3)
                        for l in range(60, 79):
                            nm4 += [nama[l]]
                        summon(msg.to, nm4)
                        for m in range(80, 99):
                            nm5 += [nama[m]]
                        summon(msg.to, nm5)
                        for n in range(100, 119):
                            nm6 += [nama[n]]
                        summon(msg.to, nm6)
                        for o in range(120, 139):
                            nm7 += [nama[o]]
                        summon(msg.to, nm7)
                        for p in range(140, 159):
                            nm8 += [nama[p]]
                        summon(msg.to, nm8)
                        for q in range(160, 179):
                            nm9 += [nama[q]]
                        summon(msg.to, nm9)
                        for r in range(180, 199):
                            nm10 += [nama[r]]
                        summon(msg.to, nm10)
                        for s in range(200, 219):
                            nm11 += [nama[s]]
                        summon(msg.to, nm11)
                        for t in range(220, 239):
                            nm12 += [nama[t]]
                        summon(msg.to, nm12)
                        for u in range(240, 259):
                            nm13 += [nama[t]]
                        summon(msg.to, nm13)
                        for v in range(260, 279):
                            nm14 += [nama[v]]
                        summon(msg.to, nm14)
                        for w in range(280, 299):
                            nm15 += [nama[w]]
                        summon(msg.to, nm15)
                        for x in range(300, 319):
                            nm16 += [nama[w]]
                        summon(msg.to, nm16)
                        for y in range(320, 339):
                            nm17 += [nama[y]]
                        summon(msg.to, nm17)
                        for z in range(340, len(nama)-1):
                            nm18 += [nama[z]]
                        summon(msg.to, nm18)
                     if jml > 360  and jml < 380:
                        for i in range(0, 19):
                            nm1 += [nama[i]]
                        summon(msg.to, nm1)
                        for j in range(20, 39):
                            nm2 += [nama[j]]
                        summon(msg.to, nm2)
                        for k in range(40, 59):
                            nm3 += [nama[k]]
                        summon(msg.to, nm3)
                        for l in range(60, 79):
                            nm4 += [nama[l]]
                        summon(msg.to, nm4)
                        for m in range(80, 99):
                            nm5 += [nama[m]]
                        summon(msg.to, nm5)
                        for n in range(100, 119):
                            nm6 += [nama[n]]
                        summon(msg.to, nm6)
                        for o in range(120, 139):
                            nm7 += [nama[o]]
                        summon(msg.to, nm7)
                        for p in range(140, 159):
                            nm8 += [nama[p]]
                        summon(msg.to, nm8)
                        for q in range(160, 179):
                            nm9 += [nama[q]]
                        summon(msg.to, nm9)
                        for r in range(180, 199):
                            nm10 += [nama[r]]
                        summon(msg.to, nm10)
                        for s in range(200, 219):
                            nm11 += [nama[s]]
                        summon(msg.to, nm11)
                        for t in range(220, 239):
                            nm12 += [nama[t]]
                        summon(msg.to, nm12)
                        for u in range(240, 259):
                            nm13 += [nama[t]]
                        summon(msg.to, nm13)
                        for v in range(260, 279):
                            nm14 += [nama[v]]
                        summon(msg.to, nm14)
                        for w in range(280, 299):
                            nm15 += [nama[w]]
                        summon(msg.to, nm15)
                        for x in range(300, 319):
                            nm16 += [nama[w]]
                        summon(msg.to, nm16)
                        for y in range(320, 339):
                            nm17 += [nama[y]]
                        summon(msg.to, nm17)
                        for z in range(340, 359):
                            nm18 += [nama[z]]
                        summon(msg.to, nm18)
                        for a in range(360, len(nama)-1):
                            nm119 += [nama[a]]
                        summon(msg.to, nm19)
                     if jml > 380  and jml < 400:
                        for i in range(0, 19):
                            nm1 += [nama[i]]
                        summon(msg.to, nm1)
                        for j in range(20, 39):
                            nm2 += [nama[j]]
                        summon(msg.to, nm2)
                        for k in range(40, 59):
                            nm3 += [nama[k]]
                        summon(msg.to, nm3)
                        for l in range(60, 79):
                            nm4 += [nama[l]]
                        summon(msg.to, nm4)
                        for m in range(80, 99):
                            nm5 += [nama[m]]
                        summon(msg.to, nm5)
                        for n in range(100, 119):
                            nm6 += [nama[n]]
                        summon(msg.to, nm6)
                        for o in range(120, 139):
                            nm7 += [nama[o]]
                        summon(msg.to, nm7)
                        for p in range(140, 159):
                            nm8 += [nama[p]]
                        summon(msg.to, nm8)
                        for q in range(160, 179):
                            nm9 += [nama[q]]
                        summon(msg.to, nm9)
                        for r in range(180, 199):
                            nm10 += [nama[r]]
                        summon(msg.to, nm10)
                        for s in range(200, 219):
                            nm11 += [nama[s]]
                        summon(msg.to, nm11)
                        for t in range(220, 239):
                            nm12 += [nama[t]]
                        summon(msg.to, nm12)
                        for u in range(240, 259):
                            nm13 += [nama[t]]
                        summon(msg.to, nm13)
                        for v in range(260, 279):
                            nm14 += [nama[v]]
                        summon(msg.to, nm14)
                        for w in range(280, 299):
                            nm15 += [nama[w]]
                        summon(msg.to, nm15)
                        for x in range(300, 319):
                            nm16 += [nama[w]]
                        summon(msg.to, nm16)
                        for y in range(320, 339):
                            nm17 += [nama[y]]
                        summon(msg.to, nm17)
                        for z in range(340, 359):
                            nm18 += [nama[z]]
                        summon(msg.to, nm18)
                        for a in range(360, 379):
                            nm19 += [nama[a]]
                        summon(msg.to, nm19)
                        for b in range(380, len(nama)-1):
                            nm20 += [nama[b]]
                        summon(msg.to, nm20)
                     if jml > 400  and jml < 420:
                        for i in range(0, 19):
                            nm1 += [nama[i]]
                        summon(msg.to, nm1)
                        for j in range(20, 39):
                            nm2 += [nama[j]]
                        summon(msg.to, nm2)
                        for k in range(40, 59):
                            nm3 += [nama[k]]
                        summon(msg.to, nm3)
                        for l in range(60, 79):
                            nm4 += [nama[l]]
                        summon(msg.to, nm4)
                        for m in range(80, 99):
                            nm5 += [nama[m]]
                        summon(msg.to, nm5)
                        for n in range(100, 119):
                            nm6 += [nama[n]]
                        summon(msg.to, nm6)
                        for o in range(120, 139):
                            nm7 += [nama[o]]
                        summon(msg.to, nm7)
                        for p in range(140, 159):
                            nm8 += [nama[p]]
                        summon(msg.to, nm8)
                        for q in range(160, 179):
                            nm9 += [nama[q]]
                        summon(msg.to, nm9)
                        for r in range(180, 199):
                            nm10 += [nama[r]]
                        summon(msg.to, nm10)
                        for s in range(200, 219):
                            nm11 += [nama[s]]
                        summon(msg.to, nm11)
                        for t in range(220, 239):
                            nm12 += [nama[t]]
                        summon(msg.to, nm12)
                        for u in range(240, 259):
                            nm13 += [nama[t]]
                        summon(msg.to, nm13)
                        for v in range(260, 279):
                            nm14 += [nama[v]]
                        summon(msg.to, nm14)
                        for w in range(280, 299):
                            nm15 += [nama[w]]
                        summon(msg.to, nm15)
                        for x in range(300, 319):
                            nm16 += [nama[w]]
                        summon(msg.to, nm16)
                        for y in range(320, 339):
                            nm17 += [nama[y]]
                        summon(msg.to, nm17)
                        for z in range(340, 359):
                            nm18 += [nama[z]]
                        summon(msg.to, nm18)
                        for a in range(360, 379):
                            nm19 += [nama[a]]
                        summon(msg.to, nm19)
                        for b in range(380, 399):
                            nm20 += [nama[b]]
                        summon(msg.to, nm20)
                        for c in range(400, len(nama)-1):
                            nm21 += [nama[c]]
                        summon(msg.to, nm21)
                     if jml > 420  and jml < 440:
                        for i in range(0, 19):
                            nm1 += [nama[i]]
                        summon(msg.to, nm1)
                        for j in range(20, 39):
                            nm2 += [nama[j]]
                        summon(msg.to, nm2)
                        for k in range(40, 59):
                            nm3 += [nama[k]]
                        summon(msg.to, nm3)
                        for l in range(60, 79):
                            nm4 += [nama[l]]
                        summon(msg.to, nm4)
                        for m in range(80, 99):
                            nm5 += [nama[m]]
                        summon(msg.to, nm5)
                        for n in range(100, 119):
                            nm6 += [nama[n]]
                        summon(msg.to, nm6)
                        for o in range(120, 139):
                            nm7 += [nama[o]]
                        summon(msg.to, nm7)
                        for p in range(140, 159):
                            nm8 += [nama[p]]
                        summon(msg.to, nm8)
                        for q in range(160, 179):
                            nm9 += [nama[q]]
                        summon(msg.to, nm9)
                        for r in range(180, 199):
                            nm10 += [nama[r]]
                        summon(msg.to, nm10)
                        for s in range(200, 219):
                            nm11 += [nama[s]]
                        summon(msg.to, nm11)
                        for t in range(220, 239):
                            nm12 += [nama[t]]
                        summon(msg.to, nm12)
                        for u in range(240, 259):
                            nm13 += [nama[t]]
                        summon(msg.to, nm13)
                        for v in range(260, 279):
                            nm14 += [nama[v]]
                        summon(msg.to, nm14)
                        for w in range(280, 299):
                            nm15 += [nama[w]]
                        summon(msg.to, nm15)
                        for x in range(300, 319):
                            nm16 += [nama[w]]
                        summon(msg.to, nm16)
                        for y in range(320, 339):
                            nm17 += [nama[y]]
                        summon(msg.to, nm17)
                        for z in range(340, 359):
                            nm18 += [nama[z]]
                        summon(msg.to, nm18)
                        for a in range(360, 379):
                            nm19 += [nama[a]]
                        summon(msg.to, nm19)
                        for b in range(380, 399):
                            nm20 += [nama[b]]
                        summon(msg.to, nm20)
                        for c in range(400, 419):
                            nm21 += [nama[c]]
                        summon(msg.to, nm21)
                        for d in range(420, len(nama)-1):
                            nm22 += [nama[d]]
                        summon(msg.to, nm22)
                     if jml > 440  and jml < 460:
                        for i in range(0, 19):
                            nm1 += [nama[i]]
                        summon(msg.to, nm1)
                        for j in range(20, 39):
                            nm2 += [nama[j]]
                        summon(msg.to, nm2)
                        for k in range(40, 59):
                            nm3 += [nama[k]]
                        summon(msg.to, nm3)
                        for l in range(60, 79):
                            nm4 += [nama[l]]
                        summon(msg.to, nm4)
                        for m in range(80, 99):
                            nm5 += [nama[m]]
                        summon(msg.to, nm5)
                        for n in range(100, 119):
                            nm6 += [nama[n]]
                        summon(msg.to, nm6)
                        for o in range(120, 139):
                            nm7 += [nama[o]]
                        summon(msg.to, nm7)
                        for p in range(140, 159):
                            nm8 += [nama[p]]
                        summon(msg.to, nm8)
                        for q in range(160, 179):
                            nm9 += [nama[q]]
                        summon(msg.to, nm9)
                        for r in range(180, 199):
                            nm10 += [nama[r]]
                        summon(msg.to, nm10)
                        for s in range(200, 219):
                            nm11 += [nama[s]]
                        summon(msg.to, nm11)
                        for t in range(220, 239):
                            nm12 += [nama[t]]
                        summon(msg.to, nm12)
                        for u in range(240, 259):
                            nm13 += [nama[t]]
                        summon(msg.to, nm13)
                        for v in range(260, 279):
                            nm14 += [nama[v]]
                        summon(msg.to, nm14)
                        for w in range(280, 299):
                            nm15 += [nama[w]]
                        summon(msg.to, nm15)
                        for x in range(300, 319):
                            nm16 += [nama[w]]
                        summon(msg.to, nm16)
                        for y in range(320, 339):
                            nm17 += [nama[y]]
                        summon(msg.to, nm17)
                        for z in range(340, 359):
                            nm18 += [nama[z]]
                        summon(msg.to, nm18)
                        for a in range(360, 379):
                            nm19 += [nama[a]]
                        summon(msg.to, nm19)
                        for b in range(380, 399):
                            nm20 += [nama[b]]
                        summon(msg.to, nm20)
                        for c in range(380, 399):
                            nm21 += [nama[c]]
                        summon(msg.to, nm21)
                        for d in range(400, 419):
                            nm22 += [nama[d]]
                        summon(msg.to, nm22)
                        for e in range(420, 439):
                            nm23 += [nama[e]]
                        summon(msg.to, nm23)
                        for f in range(440, len(nama)-1):
                            nm24 += [nama[f]]
                        summon(msg.to, nm24)
                     if jml > 460  and jml < 480:
                        for i in range(0, 19):
                            nm1 += [nama[i]]
                        summon(msg.to, nm1)
                        for j in range(20, 39):
                            nm2 += [nama[j]]
                        summon(msg.to, nm2)
                        for k in range(40, 59):
                            nm3 += [nama[k]]
                        summon(msg.to, nm3)
                        for l in range(60, 79):
                            nm4 += [nama[l]]
                        summon(msg.to, nm4)
                        for m in range(80, 99):
                            nm5 += [nama[m]]
                        summon(msg.to, nm5)
                        for n in range(100, 119):
                            nm6 += [nama[n]]
                        summon(msg.to, nm6)
                        for o in range(120, 139):
                            nm7 += [nama[o]]
                        summon(msg.to, nm7)
                        for p in range(140, 159):
                            nm8 += [nama[p]]
                        summon(msg.to, nm8)
                        for q in range(160, 179):
                            nm9 += [nama[q]]
                        summon(msg.to, nm9)
                        for r in range(180, 199):
                            nm10 += [nama[r]]
                        summon(msg.to, nm10)
                        for s in range(200, 219):
                            nm11 += [nama[s]]
                        summon(msg.to, nm11)
                        for t in range(220, 239):
                            nm12 += [nama[t]]
                        summon(msg.to, nm12)
                        for u in range(240, 259):
                            nm13 += [nama[t]]
                        summon(msg.to, nm13)
                        for v in range(260, 279):
                            nm14 += [nama[v]]
                        summon(msg.to, nm14)
                        for w in range(280, 299):
                            nm15 += [nama[w]]
                        summon(msg.to, nm15)
                        for x in range(300, 319):
                            nm16 += [nama[w]]
                        summon(msg.to, nm16)
                        for y in range(320, 339):
                            nm17 += [nama[y]]
                        summon(msg.to, nm17)
                        for z in range(340, 359):
                            nm18 += [nama[z]]
                        summon(msg.to, nm18)
                        for a in range(360, 379):
                            nm19 += [nama[a]]
                        summon(msg.to, nm19)
                        for b in range(380, 399):
                            nm20 += [nama[b]]
                        summon(msg.to, nm20)
                        for c in range(400, 419):
                            nm21 += [nama[c]]
                        summon(msg.to, nm21)
                        for d in range(420, 439):
                            nm22 += [nama[d]]
                        summon(msg.to, nm22)
                        for e in range(440, 459):
                            nm23 += [nama[e]]
                        summon(msg.to, nm23)
                        for r in range(460, 479):
                            nm24 += [nama[f]]
                        summon(msg.to, nm24)
                        for g in range(480, len(nama)-1):
                            nm25 += [nama[g]]
                        summon(msg.to, nm25)
                     if jml > 500:
                         #print "###500+"
                      cnt = Message()
                      cnt.text = "⭐️สมาชิกทั้งหมด: " + str(jml) +  " คน \nby. ❈͜͡✯ѕειт вот чєєωα✯͜͡❈"
                      cnt.to = msg.to
                      line.sendMessage(cnt)                 
   
                elif text.lower() == 'จับ':
                    tz = pytz.timezone("Asia/Jakarta")
                    timeNow = datetime.now(tz=tz)
                    day = ["Sunday", "Monday", "Tuesday", "Wednesday", "Thursday","Friday", "Saturday"]
                    hari = ["วันอาทิตย์", "วันจันทร์", "วันอังคาร", "วันพุธ", "วันพฤหัสบดี", "วันศุกร์", "วันเสาร์"]
                    bulan = ["Januari", "Februari", "Maret", "April", "Mei", "Juni", "Juli", "Agustus", "September", "Oktober", "November", "Desember"]
                    hr = timeNow.strftime("%A")
                    bln = timeNow.strftime("%m")
                    for i in range(len(day)):
                        if hr == day[i]: hasil = hari[i]
                    for k in range(0, len(bulan)):
                        if bln == str(k): bln = bulan[k-1]
                    readTime = hasil + ", " + timeNow.strftime('%d') + " - " + bln + " - " + timeNow.strftime('%Y') + "\nJam : [ " + timeNow.strftime('%H:%M:%S') + " ]"
                    if msg.to in read['readPoint']:
                            try:
                                del read['readPoint'][msg.to]
                                del read['readMember'][msg.to]
                                del read['readTime'][msg.to]
                            except:
                                pass
                            read['readPoint'][msg.to] = msg.id
                            read['readMember'][msg.to] = ""
                            read['readTime'][msg.to] = datetime.now().strftime('%H:%M:%S')
                            read['ROM'][msg.to] = {}
                            with open('read.json', 'w') as fp:
                                json.dump(read, fp, sort_keys=True, indent=4)
                                line.sendMessage(msg.to,"Lurking enabled")
                    else:
                        try:
                            del read['readPoint'][msg.to]
                            del read['readMember'][msg.to]
                            del read['readTime'][msg.to]
                        except:
                            pass
                        read['readPoint'][msg.to] = msg.id
                        read['readMember'][msg.to] = ""
                        read['readTime'][msg.to] = datetime.now().strftime('%H:%M:%S')
                        read['ROM'][msg.to] = {}
                        with open('read.json', 'w') as fp:
                            json.dump(read, fp, sort_keys=True, indent=4)
                            line.sendMessage(msg.to, "Set reading point:\n" + readTime)
                            
                elif text.lower() == 'เลิกจับ':
                    tz = pytz.timezone("Asia/Jakarta")
                    timeNow = datetime.now(tz=tz)
                    day = ["Sunday", "Monday", "Tuesday", "Wednesday", "Thursday","Friday", "Saturday"]
                    hari = ["วันอาทิตย์", "วันจันทร์", "วันอังคาร", "วันพุธ", "วันพฤหัสบดี", "วันศุกร์", "วันเสาร์"]
                    bulan = ["Januari", "Februari", "Maret", "April", "Mei", "Juni", "Juli", "Agustus", "September", "Oktober", "November", "Desember"]
                    hr = timeNow.strftime("%A")
                    bln = timeNow.strftime("%m")
                    for i in range(len(day)):
                        if hr == day[i]: hasil = hari[i]
                    for k in range(0, len(bulan)):
                        if bln == str(k): bln = bulan[k-1]
                    readTime = hasil + ", " + timeNow.strftime('%d') + " - " + bln + " - " + timeNow.strftime('%Y') + "\nJam : [ " + timeNow.strftime('%H:%M:%S') + " ]"
                    if msg.to not in read['readPoint']:
                        line.sendMessage(msg.to,"Lurking disabled")
                    else:
                        try:
                            del read['readPoint'][msg.to]
                            del read['readMember'][msg.to]
                            del read['readTime'][msg.to]
                        except:
                              pass
                        line.sendMessage(msg.to, "Delete reading point:\n" + readTime)
    
                elif text.lower() == 'จับใหม่':
                    tz = pytz.timezone("Asia/Jakarta")
                    timeNow = datetime.now(tz=tz)
                    day = ["Sunday", "Monday", "Tuesday", "Wednesday", "Thursday","Friday", "Saturday"]
                    hari = ["วันอาทิตย์", "วันจันทร์", "วันอังคาร", "วันพุธ", "วันพฤหัสบดี", "วันศุกร์", "วันเสาร์"]
                    bulan = ["Januari", "Februari", "Maret", "April", "Mei", "Juni", "Juli", "Agustus", "September", "Oktober", "November", "Desember"]
                    hr = timeNow.strftime("%A")
                    bln = timeNow.strftime("%m")
                    for i in range(len(day)):
                        if hr == day[i]: hasil = hari[i]
                    for k in range(0, len(bulan)):
                        if bln == str(k): bln = bulan[k-1]
                    readTime = hasil + ", " + timeNow.strftime('%d') + " - " + bln + " - " + timeNow.strftime('%Y') + "\nJam : [ " + timeNow.strftime('%H:%M:%S') + " ]"
                    if msg.to in read["readPoint"]:
                        try:
                            del read["readPoint"][msg.to]
                            del read["readMember"][msg.to]
                            del read["readTime"][msg.to]
                        except:
                            pass
                        line.sendMessage(msg.to, "Reset reading point:\n" + readTime)
                    else:
                        line.sendMessage(msg.to, "Lurking belum diaktifkan ngapain di reset?")
                        
                elif text.lower() == 'อ่าน':
                    tz = pytz.timezone("Asia/Jakarta")
                    timeNow = datetime.now(tz=tz)
                    day = ["Sunday", "Monday", "Tuesday", "Wednesday", "Thursday","Friday", "Saturday"]
                    hari = ["วันอาทิตย์", "วันจันทร์", "วันอังคาร", "วันพุธ", "วันพฤหัสบดี", "วันศุกร์", "วันเสาร์"]
                    bulan = ["Januari", "Februari", "Maret", "April", "Mei", "Juni", "Juli", "Agustus", "September", "Oktober", "November", "Desember"]
                    hr = timeNow.strftime("%A")
                    bln = timeNow.strftime("%m")
                    for i in range(len(day)):
                        if hr == day[i]: hasil = hari[i]
                    for k in range(0, len(bulan)):
                        if bln == str(k): bln = bulan[k-1]
                    readTime = hasil + ", " + timeNow.strftime('%d') + " - " + bln + " - " + timeNow.strftime('%Y') + "\nJam : [ " + timeNow.strftime('%H:%M:%S') + " ]"
                    if receiver in read['readPoint']:
                        if list(read["ROM"][receiver].items()) == []:
                            line.sendMessage(receiver,"[ Reader ]:\nNone")
                        else:
                            chiya = []
                            for rom in list(read["ROM"][receiver].items()):
                                chiya.append(rom[1])
                            cmem = line.getContacts(chiya) 
                            zx = ""
                            zxc = ""
                            zx2 = []
                            xpesan = '[ *** LurkDetector *** ]:\n'
                        for x in range(len(cmem)):
                            xname = str(cmem[x].displayName)
                            pesan = ''
                            pesan2 = pesan+"@c\n"
                            xlen = str(len(zxc)+len(xpesan))
                            xlen2 = str(len(zxc)+len(pesan2)+len(xpesan)-1)
                            zx = {'S':xlen, 'E':xlen2, 'M':cmem[x].mid}
                            zx2.append(zx)
                            zxc += pesan2
                        text = xpesan+ zxc + "\n[ Lurking time ]: \n" + readTime
                        try:
                            line.sendMessage(receiver, text, contentMetadata={'MENTION':str('{"MENTIONEES":'+json.dumps(zx2).replace(' ','')+'}')}, contentType=0)
                        except Exception as error:
                            print (error)
                        pass
                    else:
                        line.sendMessage(receiver,"Lurking has not been set.")
#==============================================================================#
                elif msg.text.lower().startswith("say-af "):
                    sep = text.split(" ")
                    say = text.replace(sep[0] + " ","")
                    lang = 'af'
                    tts = gTTS(text=say, lang=lang)
                    tts.save("hasil.mp3")
                    line.sendAudio(msg.to,"hasil.mp3")
        
                elif msg.text.lower().startswith("say-sq "):
                    sep = text.split(" ")
                    say = text.replace(sep[0] + " ","")
                    lang = 'sq'
                    tts = gTTS(text=say, lang=lang)
                    tts.save("hasil.mp3")
                    line.sendAudio(msg.to,"hasil.mp3")
                    
                elif msg.text.lower().startswith("say-ar "):
                    sep = text.split(" ")
                    say = text.replace(sep[0] + " ","")
                    lang = 'ar'
                    tts = gTTS(text=say, lang=lang)
                    tts.save("hasil.mp3")
                    line.sendAudio(msg.to,"hasil.mp3")
                    
                elif msg.text.lower().startswith("say-hy "):
                    sep = text.split(" ")
                    say = text.replace(sep[0] + " ","")
                    lang = 'hy'
                    tts = gTTS(text=say, lang=lang)
                    tts.save("hasil.mp3")
                    line.sendAudio(msg.to,"hasil.mp3")
                    
                elif msg.text.lower().startswith("say-bn "):
                    sep = text.split(" ")
                    say = text.replace(sep[0] + " ","")
                    lang = 'bn'
                    tts = gTTS(text=say, lang=lang)
                    tts.save("hasil.mp3")
                    line.sendAudio(msg.to,"hasil.mp3")
                    
                elif msg.text.lower().startswith("say-ca "):
                    sep = text.split(" ")
                    say = text.replace(sep[0] + " ","")
                    lang = 'ca'
                    tts = gTTS(text=say, lang=lang)
                    tts.save("hasil.mp3")
                    line.sendAudio(msg.to,"hasil.mp3")
                    
                elif msg.text.lower().startswith("say-zh "):
                    sep = text.split(" ")
                    say = text.replace(sep[0] + " ","")
                    lang = 'zh'
                    tts = gTTS(text=say, lang=lang)
                    tts.save("hasil.mp3")
                    line.sendAudio(msg.to,"hasil.mp3")
                    
                elif msg.text.lower().startswith("say-zh-cn "):
                    sep = text.split(" ")
                    say = text.replace(sep[0] + " ","")
                    lang = 'zh-cn'
                    tts = gTTS(text=say, lang=lang)
                    tts.save("hasil.mp3")
                    line.sendAudio(msg.to,"hasil.mp3")
                    
                elif msg.text.lower().startswith("say-zh-tw "):
                    sep = text.split(" ")
                    say = text.replace(sep[0] + " ","")
                    lang = 'zh-tw'
                    tts = gTTS(text=say, lang=lang)
                    tts.save("hasil.mp3")
                    line.sendAudio(msg.to,"hasil.mp3")
                    
                elif msg.text.lower().startswith("say-zh-yue "):
                    sep = text.split(" ")
                    say = text.replace(sep[0] + " ","")
                    lang = 'zh-yue'
                    tts = gTTS(text=say, lang=lang)
                    tts.save("hasil.mp3")
                    line.sendAudio(msg.to,"hasil.mp3")
                    
                elif msg.text.lower().startswith("say-hr "):
                    sep = text.split(" ")
                    say = text.replace(sep[0] + " ","")
                    lang = 'hr'
                    tts = gTTS(text=say, lang=lang)
                    tts.save("hasil.mp3")
                    line.sendAudio(msg.to,"hasil.mp3")
                    
                elif msg.text.lower().startswith("say-cs "):
                    sep = text.split(" ")
                    say = text.replace(sep[0] + " ","")
                    lang = 'cs'
                    tts = gTTS(text=say, lang=lang)
                    tts.save("hasil.mp3")
                    line.sendAudio(msg.to,"hasil.mp3")
                    
                elif msg.text.lower().startswith("say-da "):
                    sep = text.split(" ")
                    say = text.replace(sep[0] + " ","")
                    lang = 'da'
                    tts = gTTS(text=say, lang=lang)
                    tts.save("hasil.mp3")
                    line.sendAudio(msg.to,"hasil.mp3")
                    
                elif msg.text.lower().startswith("say-nl "):
                    sep = text.split(" ")
                    say = text.replace(sep[0] + " ","")
                    lang = 'nl'
                    tts = gTTS(text=say, lang=lang)
                    tts.save("hasil.mp3")
                    line.sendAudio(msg.to,"hasil.mp3")
                    
                elif msg.text.lower().startswith("say-en "):
                    sep = text.split(" ")
                    say = text.replace(sep[0] + " ","")
                    lang = 'en'
                    tts = gTTS(text=say, lang=lang)
                    tts.save("hasil.mp3")
                    line.sendAudio(msg.to,"hasil.mp3")
                    
                elif msg.text.lower().startswith("say-en-au "):
                    sep = text.split(" ")
                    say = text.replace(sep[0] + " ","")
                    lang = 'en-au'
                    tts = gTTS(text=say, lang=lang)
                    tts.save("hasil.mp3")
                    line.sendAudio(msg.to,"hasil.mp3")
                    
                elif msg.text.lower().startswith("say-en-uk "):
                    sep = text.split(" ")
                    say = text.replace(sep[0] + " ","")
                    lang = 'en-uk'
                    tts = gTTS(text=say, lang=lang)
                    tts.save("hasil.mp3")
                    line.sendAudio(msg.to,"hasil.mp3")
                    
                elif msg.text.lower().startswith("say-en-us "):
                    sep = text.split(" ")
                    say = text.replace(sep[0] + " ","")
                    lang = 'en-us'
                    tts = gTTS(text=say, lang=lang)
                    tts.save("hasil.mp3")
                    line.sendAudio(msg.to,"hasil.mp3")
                    
                elif msg.text.lower().startswith("say-eo "):
                    sep = text.split(" ")
                    say = text.replace(sep[0] + " ","")
                    lang = 'eo'
                    tts = gTTS(text=say, lang=lang)
                    tts.save("hasil.mp3")
                    line.sendAudio(msg.to,"hasil.mp3")
                    
                elif msg.text.lower().startswith("say-fi "):
                    sep = text.split(" ")
                    say = text.replace(sep[0] + " ","")
                    lang = 'fi'
                    tts = gTTS(text=say, lang=lang)
                    tts.save("hasil.mp3")
                    line.sendAudio(msg.to,"hasil.mp3")
                    
                elif msg.text.lower().startswith("say-fr "):
                    sep = text.split(" ")
                    say = text.replace(sep[0] + " ","")
                    lang = 'fr'
                    tts = gTTS(text=say, lang=lang)
                    tts.save("hasil.mp3")
                    line.sendAudio(msg.to,"hasil.mp3")
                    
                elif msg.text.lower().startswith("say-de "):
                    sep = text.split(" ")
                    say = text.replace(sep[0] + " ","")
                    lang = 'de'
                    tts = gTTS(text=say, lang=lang)
                    tts.save("hasil.mp3")
                    line.sendAudio(msg.to,"hasil.mp3")
                    
                elif msg.text.lower().startswith("say-el "):
                    sep = text.split(" ")
                    say = text.replace(sep[0] + " ","")
                    lang = 'el'
                    tts = gTTS(text=say, lang=lang)
                    tts.save("hasil.mp3")
                    line.sendAudio(msg.to,"hasil.mp3")
                    
                elif msg.text.lower().startswith("say-hi "):
                    sep = text.split(" ")
                    say = text.replace(sep[0] + " ","")
                    lang = 'hi'
                    tts = gTTS(text=say, lang=lang)
                    tts.save("hasil.mp3")
                    line.sendAudio(msg.to,"hasil.mp3")
                    
                elif msg.text.lower().startswith("say-hu "):
                    sep = text.split(" ")
                    say = text.replace(sep[0] + " ","")
                    lang = 'hu'
                    tts = gTTS(text=say, lang=lang)
                    tts.save("hasil.mp3")
                    line.sendAudio(msg.to,"hasil.mp3")
                    
                elif msg.text.lower().startswith("say-is "):
                    sep = text.split(" ")
                    say = text.replace(sep[0] + " ","")
                    lang = 'is'
                    tts = gTTS(text=say, lang=lang)
                    tts.save("hasil.mp3")
                    line.sendAudio(msg.to,"hasil.mp3")
                    
                elif msg.text.lower().startswith("say-id "):
                    sep = text.split(" ")
                    say = text.replace(sep[0] + " ","")
                    lang = 'id'
                    tts = gTTS(text=say, lang=lang)
                    tts.save("hasil.mp3")
                    line.sendAudio(msg.to,"hasil.mp3")
                    
                elif msg.text.lower().startswith("say-it "):
                    sep = text.split(" ")
                    say = text.replace(sep[0] + " ","")
                    lang = 'it'
                    tts = gTTS(text=say, lang=lang)
                    tts.save("hasil.mp3")
                    line.sendAudio(msg.to,"hasil.mp3")
                    
                elif msg.text.lower().startswith("say-ja "):
                    sep = text.split(" ")
                    say = text.replace(sep[0] + " ","")
                    lang = 'ja'
                    tts = gTTS(text=say, lang=lang)
                    tts.save("hasil.mp3")
                    line.sendAudio(msg.to,"hasil.mp3")
                    
                elif msg.text.lower().startswith("say-km "):
                    sep = text.split(" ")
                    say = text.replace(sep[0] + " ","")
                    lang = 'km'
                    tts = gTTS(text=say, lang=lang)
                    tts.save("hasil.mp3")
                    line.sendAudio(msg.to,"hasil.mp3")
                    
                elif msg.text.lower().startswith("say-ko "):
                    sep = text.split(" ")
                    say = text.replace(sep[0] + " ","")
                    lang = 'ko'
                    tts = gTTS(text=say, lang=lang)
                    tts.save("hasil.mp3")
                    line.sendAudio(msg.to,"hasil.mp3")
                    
                elif msg.text.lower().startswith("say-la "):
                    sep = text.split(" ")
                    say = text.replace(sep[0] + " ","")
                    lang = 'la'
                    tts = gTTS(text=say, lang=lang)
                    tts.save("hasil.mp3")
                    line.sendAudio(msg.to,"hasil.mp3")
                    
                elif msg.text.lower().startswith("say-lv "):
                    sep = text.split(" ")
                    say = text.replace(sep[0] + " ","")
                    lang = 'lv'
                    tts = gTTS(text=say, lang=lang)
                    tts.save("hasil.mp3")
                    line.sendAudio(msg.to,"hasil.mp3")
                    
                elif msg.text.lower().startswith("say-mk "):
                    sep = text.split(" ")
                    say = text.replace(sep[0] + " ","")
                    lang = 'mk'
                    tts = gTTS(text=say, lang=lang)
                    tts.save("hasil.mp3")
                    line.sendAudio(msg.to,"hasil.mp3")
                    
                elif msg.text.lower().startswith("say-no "):
                    sep = text.split(" ")
                    say = text.replace(sep[0] + " ","")
                    lang = 'no'
                    tts = gTTS(text=say, lang=lang)
                    tts.save("hasil.mp3")
                    line.sendAudio(msg.to,"hasil.mp3")
                    
                elif msg.text.lower().startswith("say-pl "):
                    sep = text.split(" ")
                    say = text.replace(sep[0] + " ","")
                    lang = 'pl'
                    tts = gTTS(text=say, lang=lang)
                    tts.save("hasil.mp3")
                    line.sendAudio(msg.to,"hasil.mp3")
                    
                elif msg.text.lower().startswith("say-pt "):
                    sep = text.split(" ")
                    say = text.replace(sep[0] + " ","")
                    lang = 'pt'
                    tts = gTTS(text=say, lang=lang)
                    tts.save("hasil.mp3")
                    line.sendAudio(msg.to,"hasil.mp3")
                    
                elif msg.text.lower().startswith("say-do "):
                    sep = text.split(" ")
                    say = text.replace(sep[0] + " ","")
                    lang = 'ro'
                    tts = gTTS(text=say, lang=lang)
                    tts.save("hasil.mp3")
                    line.sendAudio(msg.to,"hasil.mp3")
                    
                elif msg.text.lower().startswith("say-ru "):
                    sep = text.split(" ")
                    say = text.replace(sep[0] + " ","")
                    lang = 'ru'
                    tts = gTTS(text=say, lang=lang)
                    tts.save("hasil.mp3")
                    line.sendAudio(msg.to,"hasil.mp3")
                    
                elif msg.text.lower().startswith("say-sr "):
                    sep = text.split(" ")
                    say = text.replace(sep[0] + " ","")
                    lang = 'sr'
                    tts = gTTS(text=say, lang=lang)
                    tts.save("hasil.mp3")
                    line.sendAudio(msg.to,"hasil.mp3")
                    
                elif msg.text.lower().startswith("say-si "):
                    sep = text.split(" ")
                    say = text.replace(sep[0] + " ","")
                    lang = 'si'
                    tts = gTTS(text=say, lang=lang)
                    tts.save("hasil.mp3")
                    line.sendAudio(msg.to,"hasil.mp3")
                    
                elif msg.text.lower().startswith("say-sk "):
                    sep = text.split(" ")
                    say = text.replace(sep[0] + " ","")
                    lang = 'sk'
                    tts = gTTS(text=say, lang=lang)
                    tts.save("hasil.mp3")
                    line.sendAudio(msg.to,"hasil.mp3")
                    
                elif msg.text.lower().startswith("say-es "):
                    sep = text.split(" ")
                    say = text.replace(sep[0] + " ","")
                    lang = 'es'
                    tts = gTTS(text=say, lang=lang)
                    tts.save("hasil.mp3")
                    line.sendAudio(msg.to,"hasil.mp3")
                    
                elif msg.text.lower().startswith("say-es-es "):
                    sep = text.split(" ")
                    say = text.replace(sep[0] + " ","")
                    lang = 'es-es'
                    tts = gTTS(text=say, lang=lang)
                    tts.save("hasil.mp3")
                    line.sendAudio(msg.to,"hasil.mp3")
                    
                elif msg.text.lower().startswith("say-es-us "):
                    sep = text.split(" ")
                    say = text.replace(sep[0] + " ","")
                    lang = 'es-us'
                    tts = gTTS(text=say, lang=lang)
                    tts.save("hasil.mp3")
                    line.sendAudio(msg.to,"hasil.mp3")
                    
                elif msg.text.lower().startswith("say-sw "):
                    sep = text.split(" ")
                    say = text.replace(sep[0] + " ","")
                    lang = 'sw'
                    tts = gTTS(text=say, lang=lang)
                    tts.save("hasil.mp3")
                    line.sendAudio(msg.to,"hasil.mp3")
                    
                elif msg.text.lower().startswith("say-sv "):
                    sep = text.split(" ")
                    say = text.replace(sep[0] + " ","")
                    lang = 'sv'
                    tts = gTTS(text=say, lang=lang)
                    tts.save("hasil.mp3")
                    line.sendAudio(msg.to,"hasil.mp3")
                    
                elif msg.text.lower().startswith("say-ta "):
                    sep = text.split(" ")
                    say = text.replace(sep[0] + " ","")
                    lang = 'ta'
                    tts = gTTS(text=say, lang=lang)
                    tts.save("hasil.mp3")
                    line.sendAudio(msg.to,"hasil.mp3")
                    
                elif msg.text.lower().startswith("say-th "):
                    sep = text.split(" ")
                    say = text.replace(sep[0] + " ","")
                    lang = 'th'
                    tts = gTTS(text=say, lang=lang)
                    tts.save("hasil.mp3")
                    line.sendAudio(msg.to,"hasil.mp3")
                    
                elif msg.text.lower().startswith("say-tr "):
                    sep = text.split(" ")
                    say = text.replace(sep[0] + " ","")
                    lang = 'tr'
                    tts = gTTS(text=say, lang=lang)
                    tts.save("hasil.mp3")
                    line.sendAudio(msg.to,"hasil.mp3")
                    
                elif msg.text.lower().startswith("say-uk "):
                    sep = text.split(" ")
                    say = text.replace(sep[0] + " ","")
                    lang = 'uk'
                    tts = gTTS(text=say, lang=lang)
                    tts.save("hasil.mp3")
                    line.sendAudio(msg.to,"hasil.mp3")
                    
                elif msg.text.lower().startswith("say-vi "):
                    sep = text.split(" ")
                    say = text.replace(sep[0] + " ","")
                    lang = 'vi'
                    tts = gTTS(text=say, lang=lang)
                    tts.save("hasil.mp3")
                    line.sendAudio(msg.to,"hasil.mp3")
                    
                elif msg.text.lower().startswith("say-cy "):
                    sep = text.split(" ")
                    say = text.replace(sep[0] + " ","")
                    lang = 'cy'
                    tts = gTTS(text=say, lang=lang)
                    tts.save("hasil.mp3")
                    line.sendAudio(msg.to,"hasil.mp3")
#==============================================================================# 
                elif msg.text.lower().startswith("tr-af "):
                    sep = text.split(" ")
                    isi = text.replace(sep[0] + " ","")
                    translator = Translator()
                    hasil = translator.translate(isi, dest='af')
                    A = hasil.text
                    line.sendMessage(msg.to, A)
                elif msg.text.lower().startswith("tr-sq "):
                    sep = text.split(" ")
                    isi = text.replace(sep[0] + " ","")
                    translator = Translator()
                    hasil = translator.translate(isi, dest='sq')
                    A = hasil.text
                    line.sendMessage(msg.to, A)
                elif msg.text.lower().startswith("tr-am "):
                    sep = text.split(" ")
                    isi = text.replace(sep[0] + " ","")
                    translator = Translator()
                    hasil = translator.translate(isi, dest='am')
                    A = hasil.text
                    line.sendMessage(msg.to, A)
                elif msg.text.lower().startswith("tr-ar "):
                    sep = text.split(" ")
                    isi = text.replace(sep[0] + " ","")
                    translator = Translator()
                    hasil = translator.translate(isi, dest='ar')
                    A = hasil.text
                    line.sendMessage(msg.to, A)
                elif msg.text.lower().startswith("tr-hy "):
                    sep = text.split(" ")
                    isi = text.replace(sep[0] + " ","")
                    translator = Translator()
                    hasil = translator.translate(isi, dest='hy')
                    A = hasil.text
                    line.sendMessage(msg.to, A)
                elif msg.text.lower().startswith("tr-az "):
                    sep = text.split(" ")
                    isi = text.replace(sep[0] + " ","")
                    translator = Translator()
                    hasil = translator.translate(isi, dest='az')
                    A = hasil.text
                    line.sendMessage(msg.to, A)
                elif msg.text.lower().startswith("tr-eu "):
                    sep = text.split(" ")
                    isi = text.replace(sep[0] + " ","")
                    translator = Translator()
                    hasil = translator.translate(isi, dest='eu')
                    A = hasil.text
                    line.sendMessage(msg.to, A)
                elif msg.text.lower().startswith("tr-be "):
                    sep = text.split(" ")
                    isi = text.replace(sep[0] + " ","")
                    translator = Translator()
                    hasil = translator.translate(isi, dest='be')
                    A = hasil.text
                    line.sendMessage(msg.to, A)
                elif msg.text.lower().startswith("tr-bn "):
                    sep = text.split(" ")
                    isi = text.replace(sep[0] + " ","")
                    translator = Translator()
                    hasil = translator.translate(isi, dest='bn')
                    A = hasil.text
                    line.sendMessage(msg.to, A)
                elif msg.text.lower().startswith("tr-bs "):
                    sep = text.split(" ")
                    isi = text.replace(sep[0] + " ","")
                    translator = Translator()
                    hasil = translator.translate(isi, dest='bs')
                    A = hasil.text
                    line.sendMessage(msg.to, A)
                elif msg.text.lower().startswith("tr-bg "):
                    sep = text.split(" ")
                    isi = text.replace(sep[0] + " ","")
                    translator = Translator()
                    hasil = translator.translate(isi, dest='bg')
                    A = hasil.text
                    line.sendMessage(msg.to, A)
                elif msg.text.lower().startswith("tr-ca "):
                    sep = text.split(" ")
                    isi = text.replace(sep[0] + " ","")
                    translator = Translator()
                    hasil = translator.translate(isi, dest='ca')
                    A = hasil.text
                    line.sendMessage(msg.to, A)
                elif msg.text.lower().startswith("tr-ceb "):
                    sep = text.split(" ")
                    isi = text.replace(sep[0] + " ","")
                    translator = Translator()
                    hasil = translator.translate(isi, dest='ceb')
                    A = hasil.text
                    line.sendMessage(msg.to, A)
                elif msg.text.lower().startswith("tr-ny "):
                    sep = text.split(" ")
                    isi = text.replace(sep[0] + " ","")
                    translator = Translator()
                    hasil = translator.translate(isi, dest='ny')
                    A = hasil.text
                    line.sendMessage(msg.to, A)
                elif msg.text.lower().startswith("tr-zh-cn "):
                    sep = text.split(" ")
                    isi = text.replace(sep[0] + " ","")
                    translator = Translator()
                    hasil = translator.translate(isi, dest='zh-cn')
                    A = hasil.text
                    line.sendMessage(msg.to, A)
                elif msg.text.lower().startswith("tr-zh-tw "):
                    sep = text.split(" ")
                    isi = text.replace(sep[0] + " ","")
                    translator = Translator()
                    hasil = translator.translate(isi, dest='zh-tw')
                    A = hasil.text
                    line.sendMessage(msg.to, A)
                elif msg.text.lower().startswith("tr-co "):
                    sep = text.split(" ")
                    isi = text.replace(sep[0] + " ","")
                    translator = Translator()
                    hasil = translator.translate(isi, dest='co')
                    A = hasil.text
                    line.sendMessage(msg.to, A)
                elif msg.text.lower().startswith("tr-hr "):
                    sep = text.split(" ")
                    isi = text.replace(sep[0] + " ","")
                    translator = Translator()
                    hasil = translator.translate(isi, dest='hr')
                    A = hasil.text
                    line.sendMessage(msg.to, A)
                elif msg.text.lower().startswith("tr-cs "):
                    sep = text.split(" ")
                    isi = text.replace(sep[0] + " ","")
                    translator = Translator()
                    hasil = translator.translate(isi, dest='cs')
                    A = hasil.text
                    line.sendMessage(msg.to, A)
                elif msg.text.lower().startswith("tr-da "):
                    sep = text.split(" ")
                    isi = text.replace(sep[0] + " ","")
                    translator = Translator()
                    hasil = translator.translate(isi, dest='da')
                    A = hasil.text
                    line.sendMessage(msg.to, A)
                elif msg.text.lower().startswith("tr-nl "):
                    sep = text.split(" ")
                    isi = text.replace(sep[0] + " ","")
                    translator = Translator()
                    hasil = translator.translate(isi, dest='nl')
                    A = hasil.text
                    line.sendMessage(msg.to, A)
                elif msg.text.lower().startswith("tr-en "):
                    sep = text.split(" ")
                    isi = text.replace(sep[0] + " ","")
                    translator = Translator()
                    hasil = translator.translate(isi, dest='en')
                    A = hasil.text
                    line.sendMessage(msg.to, A)
                elif msg.text.lower().startswith("tr-et "):
                    sep = text.split(" ")
                    isi = text.replace(sep[0] + " ","")
                    translator = Translator()
                    hasil = translator.translate(isi, dest='et')
                    A = hasil.text
                    line.sendMessage(msg.to, A)
                elif msg.text.lower().startswith("tr-fi "):
                    sep = text.split(" ")
                    isi = text.replace(sep[0] + " ","")
                    translator = Translator()
                    hasil = translator.translate(isi, dest='fi')
                    A = hasil.text
                    line.sendMessage(msg.to, A)
                elif msg.text.lower().startswith("tr-fr "):
                    sep = text.split(" ")
                    isi = text.replace(sep[0] + " ","")
                    translator = Translator()
                    hasil = translator.translate(isi, dest='fr')
                    A = hasil.text
                    line.sendMessage(msg.to, A)
                elif msg.text.lower().startswith("tr-fy "):
                    sep = text.split(" ")
                    isi = text.replace(sep[0] + " ","")
                    translator = Translator()
                    hasil = translator.translate(isi, dest='fy')
                    A = hasil.text
                    line.sendMessage(msg.to, A)
                elif msg.text.lower().startswith("tr-gl "):
                    sep = text.split(" ")
                    isi = text.replace(sep[0] + " ","")
                    translator = Translator()
                    hasil = translator.translate(isi, dest='gl')
                    A = hasil.text
                    line.sendMessage(msg.to, A)
                elif msg.text.lower().startswith("tr-ka "):
                    sep = text.split(" ")
                    isi = text.replace(sep[0] + " ","")
                    translator = Translator()
                    hasil = translator.translate(isi, dest='ka')
                    A = hasil.text
                    line.sendMessage(msg.to, A)
                elif msg.text.lower().startswith("tr-de "):
                    sep = text.split(" ")
                    isi = text.replace(sep[0] + " ","")
                    translator = Translator()
                    hasil = translator.translate(isi, dest='de')
                    A = hasil.text
                    line.sendMessage(msg.to, A)
                elif msg.text.lower().startswith("tr-el "):
                    sep = text.split(" ")
                    isi = text.replace(sep[0] + " ","")
                    translator = Translator()
                    hasil = translator.translate(isi, dest='el')
                    A = hasil.text
                    line.sendMessage(msg.to, A)
                elif msg.text.lower().startswith("tr-gu "):
                    sep = text.split(" ")
                    isi = text.replace(sep[0] + " ","")
                    translator = Translator()
                    hasil = translator.translate(isi, dest='gu')
                    A = hasil.text
                    line.sendMessage(msg.to, A)
                elif msg.text.lower().startswith("tr-ht "):
                    sep = text.split(" ")
                    isi = text.replace(sep[0] + " ","")
                    translator = Translator()
                    hasil = translator.translate(isi, dest='ht')
                    A = hasil.text
                    line.sendMessage(msg.to, A)
                elif msg.text.lower().startswith("tr-ha "):
                    sep = text.split(" ")
                    isi = text.replace(sep[0] + " ","")
                    translator = Translator()
                    hasil = translator.translate(isi, dest='ha')
                    A = hasil.text
                    line.sendMessage(msg.to, A)
                elif msg.text.lower().startswith("tr-haw "):
                    sep = text.split(" ")
                    isi = text.replace(sep[0] + " ","")
                    translator = Translator()
                    hasil = translator.translate(isi, dest='haw')
                    A = hasil.text
                    line.sendMessage(msg.to, A)
                elif msg.text.lower().startswith("tr-iw "):
                    sep = text.split(" ")
                    isi = text.replace(sep[0] + " ","")
                    translator = Translator()
                    hasil = translator.translate(isi, dest='iw')
                    A = hasil.text
                    line.sendMessage(msg.to, A)
                elif msg.text.lower().startswith("tr-hi "):
                    sep = text.split(" ")
                    isi = text.replace(sep[0] + " ","")
                    translator = Translator()
                    hasil = translator.translate(isi, dest='hi')
                    A = hasil.text
                    line.sendMessage(msg.to, A)
                elif msg.text.lower().startswith("tr-hmn "):
                    sep = text.split(" ")
                    isi = text.replace(sep[0] + " ","")
                    translator = Translator()
                    hasil = translator.translate(isi, dest='hmn')
                    A = hasil.text
                    line.sendMessage(msg.to, A)
                elif msg.text.lower().startswith("tr-hu "):
                    sep = text.split(" ")
                    isi = text.replace(sep[0] + " ","")
                    translator = Translator()
                    hasil = translator.translate(isi, dest='hu')
                    A = hasil.text
                    line.sendMessage(msg.to, A)
                elif msg.text.lower().startswith("tr-is "):
                    sep = text.split(" ")
                    isi = text.replace(sep[0] + " ","")
                    translator = Translator()
                    hasil = translator.translate(isi, dest='is')
                    A = hasil.text
                    line.sendMessage(msg.to, A)
                elif msg.text.lower().startswith("tr-ig "):
                    sep = text.split(" ")
                    isi = text.replace(sep[0] + " ","")
                    translator = Translator()
                    hasil = translator.translate(isi, dest='ig')
                    A = hasil.text
                    line.sendMessage(msg.to, A)
                elif msg.text.lower().startswith("tr-id "):
                    sep = text.split(" ")
                    isi = text.replace(sep[0] + " ","")
                    translator = Translator()
                    hasil = translator.translate(isi, dest='id')
                    A = hasil.text
                    line.sendMessage(msg.to, A)
                elif msg.text.lower().startswith("tr-ga "):
                    sep = text.split(" ")
                    isi = text.replace(sep[0] + " ","")
                    translator = Translator()
                    hasil = translator.translate(isi, dest='ga')
                    A = hasil.text
                    line.sendMessage(msg.to, A)
                elif msg.text.lower().startswith("tr-it "):
                    sep = text.split(" ")
                    isi = text.replace(sep[0] + " ","")
                    translator = Translator()
                    hasil = translator.translate(isi, dest='it')
                    A = hasil.text
                    line.sendMessage(msg.to, A)
                elif msg.text.lower().startswith("tr-ja "):
                    sep = text.split(" ")
                    isi = text.replace(sep[0] + " ","")
                    translator = Translator()
                    hasil = translator.translate(isi, dest='ja')
                    A = hasil.text
                    line.sendMessage(msg.to, A)
                elif msg.text.lower().startswith("tr-jw "):
                    sep = text.split(" ")
                    isi = text.replace(sep[0] + " ","")
                    translator = Translator()
                    hasil = translator.translate(isi, dest='jw')
                    A = hasil.text
                    line.sendMessage(msg.to, A)
                elif msg.text.lower().startswith("tr-kn "):
                    sep = text.split(" ")
                    isi = text.replace(sep[0] + " ","")
                    translator = Translator()
                    hasil = translator.translate(isi, dest='kn')
                    A = hasil.text
                    line.sendMessage(msg.to, A)
                elif msg.text.lower().startswith("tr-kk "):
                    sep = text.split(" ")
                    isi = text.replace(sep[0] + " ","")
                    translator = Translator()
                    hasil = translator.translate(isi, dest='kk')
                    A = hasil.text
                    line.sendMessage(msg.to, A)
                elif msg.text.lower().startswith("tr-km "):
                    sep = text.split(" ")
                    isi = text.replace(sep[0] + " ","")
                    translator = Translator()
                    hasil = translator.translate(isi, dest='km')
                    A = hasil.text
                    line.sendMessage(msg.to, A)
                elif msg.text.lower().startswith("tr-ko "):
                    sep = text.split(" ")
                    isi = text.replace(sep[0] + " ","")
                    translator = Translator()
                    hasil = translator.translate(isi, dest='ko')
                    A = hasil.text
                    line.sendMessage(msg.to, A)
                elif msg.text.lower().startswith("tr-ku "):
                    sep = text.split(" ")
                    isi = text.replace(sep[0] + " ","")
                    translator = Translator()
                    hasil = translator.translate(isi, dest='ku')
                    A = hasil.text
                    line.sendMessage(msg.to, A)
                elif msg.text.lower().startswith("tr-ky "):
                    sep = text.split(" ")
                    isi = text.replace(sep[0] + " ","")
                    translator = Translator()
                    hasil = translator.translate(isi, dest='ky')
                    A = hasil.text
                    line.sendMessage(msg.to, A)
                elif msg.text.lower().startswith("tr-lo "):
                    sep = text.split(" ")
                    isi = text.replace(sep[0] + " ","")
                    translator = Translator()
                    hasil = translator.translate(isi, dest='lo')
                    A = hasil.text
                    line.sendMessage(msg.to, A)
                elif msg.text.lower().startswith("tr-la "):
                    sep = text.split(" ")
                    isi = text.replace(sep[0] + " ","")
                    translator = Translator()
                    hasil = translator.translate(isi, dest='la')
                    A = hasil.text
                    line.sendMessage(msg.to, A)
                elif msg.text.lower().startswith("tr-lv "):
                    sep = text.split(" ")
                    isi = text.replace(sep[0] + " ","")
                    translator = Translator()
                    hasil = translator.translate(isi, dest='lv')
                    A = hasil.text
                    line.sendMessage(msg.to, A)
                elif msg.text.lower().startswith("tr-lt "):
                    sep = text.split(" ")
                    isi = text.replace(sep[0] + " ","")
                    translator = Translator()
                    hasil = translator.translate(isi, dest='lt')
                    A = hasil.text
                    line.sendMessage(msg.to, A)
                elif msg.text.lower().startswith("tr-lb "):
                    sep = text.split(" ")
                    isi = text.replace(sep[0] + " ","")
                    translator = Translator()
                    hasil = translator.translate(isi, dest='lb')
                    A = hasil.text
                    line.sendMessage(msg.to, A)
                elif msg.text.lower().startswith("tr-mk "):
                    sep = text.split(" ")
                    isi = text.replace(sep[0] + " ","")
                    translator = Translator()
                    hasil = translator.translate(isi, dest='mk')
                    A = hasil.text
                    line.sendMessage(msg.to, A)
                elif msg.text.lower().startswith("tr-mg "):
                    sep = text.split(" ")
                    isi = text.replace(sep[0] + " ","")
                    translator = Translator()
                    hasil = translator.translate(isi, dest='mg')
                    A = hasil.text
                    line.sendMessage(msg.to, A)
                elif msg.text.lower().startswith("tr-ms "):
                    sep = text.split(" ")
                    isi = text.replace(sep[0] + " ","")
                    translator = Translator()
                    hasil = translator.translate(isi, dest='ms')
                    A = hasil.text
                    line.sendMessage(msg.to, A)
                elif msg.text.lower().startswith("tr-ml "):
                    sep = text.split(" ")
                    isi = text.replace(sep[0] + " ","")
                    translator = Translator()
                    hasil = translator.translate(isi, dest='ml')
                    A = hasil.text
                    line.sendMessage(msg.to, A)
                elif msg.text.lower().startswith("tr-mt "):
                    sep = text.split(" ")
                    isi = text.replace(sep[0] + " ","")
                    translator = Translator()
                    hasil = translator.translate(isi, dest='mt')
                    A = hasil.text
                    line.sendMessage(msg.to, A)
                elif msg.text.lower().startswith("tr-mi "):
                    sep = text.split(" ")
                    isi = text.replace(sep[0] + " ","")
                    translator = Translator()
                    hasil = translator.translate(isi, dest='mi')
                    A = hasil.text
                    line.sendMessage(msg.to, A)
                elif msg.text.lower().startswith("tr-mr "):
                    sep = text.split(" ")
                    isi = text.replace(sep[0] + " ","")
                    translator = Translator()
                    hasil = translator.translate(isi, dest='mr')
                    A = hasil.text
                    line.sendMessage(msg.to, A)
                elif msg.text.lower().startswith("tr-mn "):
                    sep = text.split(" ")
                    isi = text.replace(sep[0] + " ","")
                    translator = Translator()
                    hasil = translator.translate(isi, dest='mn')
                    A = hasil.text
                    line.sendMessage(msg.to, A)
                elif msg.text.lower().startswith("tr-my "):
                    sep = text.split(" ")
                    isi = text.replace(sep[0] + " ","")
                    translator = Translator()
                    hasil = translator.translate(isi, dest='my')
                    A = hasil.text
                    line.sendMessage(msg.to, A)
                elif msg.text.lower().startswith("tr-ne "):
                    sep = text.split(" ")
                    isi = text.replace(sep[0] + " ","")
                    translator = Translator()
                    hasil = translator.translate(isi, dest='ne')
                    A = hasil.text
                    line.sendMessage(msg.to, A)
                elif msg.text.lower().startswith("tr-no "):
                    sep = text.split(" ")
                    isi = text.replace(sep[0] + " ","")
                    translator = Translator()
                    hasil = translator.translate(isi, dest='no')
                    A = hasil.text
                    line.sendMessage(msg.to, A)
                elif msg.text.lower().startswith("tr-ps "):
                    sep = text.split(" ")
                    isi = text.replace(sep[0] + " ","")
                    translator = Translator()
                    hasil = translator.translate(isi, dest='ps')
                    A = hasil.text
                    line.sendMessage(msg.to, A)
                elif msg.text.lower().startswith("tr-fa "):
                    sep = text.split(" ")
                    isi = text.replace(sep[0] + " ","")
                    translator = Translator()
                    hasil = translator.translate(isi, dest='fa')
                    A = hasil.text
                    line.sendMessage(msg.to, A)
                elif msg.text.lower().startswith("tr-pl "):
                    sep = text.split(" ")
                    isi = text.replace(sep[0] + " ","")
                    translator = Translator()
                    hasil = translator.translate(isi, dest='pl')
                    A = hasil.text
                    line.sendMessage(msg.to, A)
                elif msg.text.lower().startswith("tr-pt "):
                    sep = text.split(" ")
                    isi = text.replace(sep[0] + " ","")
                    translator = Translator()
                    hasil = translator.translate(isi, dest='pt')
                    A = hasil.text
                    line.sendMessage(msg.to, A)
                elif msg.text.lower().startswith("tr-pa "):
                    sep = text.split(" ")
                    isi = text.replace(sep[0] + " ","")
                    translator = Translator()
                    hasil = translator.translate(isi, dest='pa')
                    A = hasil.text
                    line.sendMessage(msg.to, A)
                elif msg.text.lower().startswith("tr-ro "):
                    sep = text.split(" ")
                    isi = text.replace(sep[0] + " ","")
                    translator = Translator()
                    hasil = translator.translate(isi, dest='ro')
                    A = hasil.text
                    line.sendMessage(msg.to, A)
                elif msg.text.lower().startswith("tr-ru "):
                    sep = text.split(" ")
                    isi = text.replace(sep[0] + " ","")
                    translator = Translator()
                    hasil = translator.translate(isi, dest='ru')
                    A = hasil.text
                    line.sendMessage(msg.to, A)
                elif msg.text.lower().startswith("tr-sm "):
                    sep = text.split(" ")
                    isi = text.replace(sep[0] + " ","")
                    translator = Translator()
                    hasil = translator.translate(isi, dest='sm')
                    A = hasil.text
                    line.sendMessage(msg.to, A)
                elif msg.text.lower().startswith("tr-gd "):
                    sep = text.split(" ")
                    isi = text.replace(sep[0] + " ","")
                    translator = Translator()
                    hasil = translator.translate(isi, dest='gd')
                    A = hasil.text
                    line.sendMessage(msg.to, A)
                elif msg.text.lower().startswith("tr-sr "):
                    sep = text.split(" ")
                    isi = text.replace(sep[0] + " ","")
                    translator = Translator()
                    hasil = translator.translate(isi, dest='sr')
                    A = hasil.text
                    line.sendMessage(msg.to, A)
                elif msg.text.lower().startswith("tr-st "):
                    sep = text.split(" ")
                    isi = text.replace(sep[0] + " ","")
                    translator = Translator()
                    hasil = translator.translate(isi, dest='st')
                    A = hasil.text
                    line.sendMessage(msg.to, A)
                elif msg.text.lower().startswith("tr-sn "):
                    sep = text.split(" ")
                    isi = text.replace(sep[0] + " ","")
                    translator = Translator()
                    hasil = translator.translate(isi, dest='sn')
                    A = hasil.text
                    line.sendMessage(msg.to, A)
                elif msg.text.lower().startswith("tr-sd "):
                    sep = text.split(" ")
                    isi = text.replace(sep[0] + " ","")
                    translator = Translator()
                    hasil = translator.translate(isi, dest='sd')
                    A = hasil.text
                    line.sendMessage(msg.to, A)
                elif msg.text.lower().startswith("tr-si "):
                    sep = text.split(" ")
                    isi = text.replace(sep[0] + " ","")
                    translator = Translator()
                    hasil = translator.translate(isi, dest='si')
                    A = hasil.text
                    line.sendMessage(msg.to, A)
                elif msg.text.lower().startswith("tr-sk "):
                    sep = text.split(" ")
                    isi = text.replace(sep[0] + " ","")
                    translator = Translator()
                    hasil = translator.translate(isi, dest='sk')
                    A = hasil.text
                    line.sendMessage(msg.to, A)
                elif msg.text.lower().startswith("tr-sl "):
                    sep = text.split(" ")
                    isi = text.replace(sep[0] + " ","")
                    translator = Translator()
                    hasil = translator.translate(isi, dest='sl')
                    A = hasil.text
                    line.sendMessage(msg.to, A)
                elif msg.text.lower().startswith("tr-so "):
                    sep = text.split(" ")
                    isi = text.replace(sep[0] + " ","")
                    translator = Translator()
                    hasil = translator.translate(isi, dest='so')
                    A = hasil.text
                    line.sendMessage(msg.to, A)
                elif msg.text.lower().startswith("tr-es "):
                    sep = text.split(" ")
                    isi = text.replace(sep[0] + " ","")
                    translator = Translator()
                    hasil = translator.translate(isi, dest='es')
                    A = hasil.text
                    line.sendMessage(msg.to, A)
                elif msg.text.lower().startswith("tr-su "):
                    sep = text.split(" ")
                    isi = text.replace(sep[0] + " ","")
                    translator = Translator()
                    hasil = translator.translate(isi, dest='su')
                    A = hasil.text
                    line.sendMessage(msg.to, A)
                elif msg.text.lower().startswith("tr-sw "):
                    sep = text.split(" ")
                    isi = text.replace(sep[0] + " ","")
                    translator = Translator()
                    hasil = translator.translate(isi, dest='sw')
                    A = hasil.text
                    line.sendMessage(msg.to, A)
                elif msg.text.lower().startswith("tr-sv "):
                    sep = text.split(" ")
                    isi = text.replace(sep[0] + " ","")
                    translator = Translator()
                    hasil = translator.translate(isi, dest='sv')
                    A = hasil.text
                    line.sendMessage(msg.to, A)
                elif msg.text.lower().startswith("tr-tg "):
                    sep = text.split(" ")
                    isi = text.replace(sep[0] + " ","")
                    translator = Translator()
                    hasil = translator.translate(isi, dest='tg')
                    A = hasil.text
                    line.sendMessage(msg.to, A)
                elif msg.text.lower().startswith("tr-ta "):
                    sep = text.split(" ")
                    isi = text.replace(sep[0] + " ","")
                    translator = Translator()
                    hasil = translator.translate(isi, dest='ta')
                    A = hasil.text
                    line.sendMessage(msg.to, A)
                elif msg.text.lower().startswith("tr-te "):
                    sep = text.split(" ")
                    isi = text.replace(sep[0] + " ","")
                    translator = Translator()
                    hasil = translator.translate(isi, dest='te')
                    A = hasil.text
                    line.sendMessage(msg.to, A)
                elif msg.text.lower().startswith("tr-th "):
                    sep = text.split(" ")
                    isi = text.replace(sep[0] + " ","")
                    translator = Translator()
                    hasil = translator.translate(isi, dest='th')
                    A = hasil.text
                    line.sendMessage(msg.to, A)
                elif msg.text.lower().startswith("tr-tr "):
                    sep = text.split(" ")
                    isi = text.replace(sep[0] + " ","")
                    translator = Translator()
                    hasil = translator.translate(isi, dest='tr')
                    A = hasil.text
                    line.sendMessage(msg.to, A)
                elif msg.text.lower().startswith("tr-uk "):
                    sep = text.split(" ")
                    isi = text.replace(sep[0] + " ","")
                    translator = Translator()
                    hasil = translator.translate(isi, dest='uk')
                    A = hasil.text
                    line.sendMessage(msg.to, A)
                elif msg.text.lower().startswith("tr-ur "):
                    sep = text.split(" ")
                    isi = text.replace(sep[0] + " ","")
                    translator = Translator()
                    hasil = translator.translate(isi, dest='ur')
                    A = hasil.text
                    line.sendMessage(msg.to, A)
                elif msg.text.lower().startswith("tr-uz "):
                    sep = text.split(" ")
                    isi = text.replace(sep[0] + " ","")
                    translator = Translator()
                    hasil = translator.translate(isi, dest='uz')
                    A = hasil.text
                    line.sendMessage(msg.to, A)
                elif msg.text.lower().startswith("tr-vi "):
                    sep = text.split(" ")
                    isi = text.replace(sep[0] + " ","")
                    translator = Translator()
                    hasil = translator.translate(isi, dest='vi')
                    A = hasil.text
                    line.sendMessage(msg.to, A)
                elif msg.text.lower().startswith("tr-cy "):
                    sep = text.split(" ")
                    isi = text.replace(sep[0] + " ","")
                    translator = Translator()
                    hasil = translator.translate(isi, dest='cy')
                    A = hasil.text
                    line.sendMessage(msg.to, A)
                elif msg.text.lower().startswith("tr-xh "):
                    sep = text.split(" ")
                    isi = text.replace(sep[0] + " ","")
                    translator = Translator()
                    hasil = translator.translate(isi, dest='xh')
                    A = hasil.text
                    line.sendMessage(msg.to, A)
                elif msg.text.lower().startswith("tr-yi "):
                    sep = text.split(" ")
                    isi = text.replace(sep[0] + " ","")
                    translator = Translator()
                    hasil = translator.translate(isi, dest='yi')
                    A = hasil.text
                    line.sendMessage(msg.to, A)
                elif msg.text.lower().startswith("tr-yo "):
                    sep = text.split(" ")
                    isi = text.replace(sep[0] + " ","")
                    translator = Translator()
                    hasil = translator.translate(isi, dest='yo')
                    A = hasil.text
                    line.sendMessage(msg.to, A)
                elif msg.text.lower().startswith("tr-zu "):
                    sep = text.split(" ")
                    isi = text.replace(sep[0] + " ","")
                    translator = Translator()
                    hasil = translator.translate(isi, dest='zu')
                    A = hasil.text
                    line.sendMessage(msg.to, A)
                elif msg.text.lower().startswith("tr-fil "):
                    sep = text.split(" ")
                    isi = text.replace(sep[0] + " ","")
                    translator = Translator()
                    hasil = translator.translate(isi, dest='fil')
                    A = hasil.text
                    line.sendMessage(msg.to, A)
                elif msg.text.lower().startswith("tr-he "):
                    sep = text.split(" ")
                    isi = text.replace(sep[0] + " ","")
                    translator = Translator()
                    hasil = translator.translate(isi, dest='he')
                    A = hasil.text
                    line.sendMessage(msg.to, A)

#==============================================================================#
                elif "ประกาศกลุ่ม " in msg.text:
                    icon = "http://dl.profile.line.naver.jp/"+lineProfile.pictureStatus
                    name = "ข้อความประกาศ"                   
                    link = "http://line.me/ti/p/~tome2527"
                    bc = msg.text.replace(".ประกาศกลุ่ม ","")
                    gid = line.getGroupIdsJoined()
                    for i in gid:
                        line.sendFooter(i, bc+"\n\n◐✯Armtheking.🇹🇭✯◐",link ,icon,name)
                    
                         
                elif "ประกาศ: " in msg.text:
                    #if msg._from in admin:
                    sep = text.split(" ")
                    bc = text.replace(sep[0] + " ","")
                    gid = line.getGroupIdsJoined()
                    for group in gid:
                       ryan = line.getContact(mid)
                       zx = ""
                       zxc = ""
                       zx2 = []
                       xpesan =  "「 Broadcast 」\nBroadcast by "
                       ret_ = "{}".format(str(bc))
                       ry = str(ryan.displayName)
                       pesan = ''
                       pesan2 = pesan+"@x\n"
                       xlen = str(len(zxc)+len(xpesan))
                       xlen2 = str(len(zxc)+len(pesan2)+len(xpesan)-1)
                       zx = {'S':xlen, 'E':xlen2, 'M':ryan.mid}
                       zx2.append(zx)
                       zxc += pesan2
                       text = xpesan + zxc + ret_ + ""
                       line.sendMessage(group, text, contentMetadata={'MENTION':str('{"MENTIONEES":'+json.dumps(zx2).replace(' ','')+'}')}, contentType=0)                                
                    
                elif "ประกาศแชท " in msg.text:
                    bc = msg.text.replace(".ประกาศแชท ","")
                    gid = line.getAllContactIds()
                    for i in gid:
                        line.sendText(i,"Armtheking.🇹🇭\n"+bc+"\n\n◐✯Armtheking.🇹🇭✯◐")
            
                elif "ส่งรูปภาพตามกลุ่ม: " in msg.text:
                    bc = msg.text.replace("ส่งรูปภาพตามกลุ่ม: ","")
                    gid = line.getGroupIdsJoined()
                    for i in gid:
                        line.sendImageWithURL(i, bc)
                    
                elif "ส่งรูปภาพตามแชท: " in msg.text:
                    bc = msg.text.replace("ส่งรูปภาพตามแชท: ","")
                    gid = line.getAllContactIds()
                    for i in gid:
                        line.sendImageWithURL(i, bc)
                elif "ส่งเสียงกลุ่ม " in msg.text:
                    bctxt = msg.text.replace("ส่งเสียงกลุ่ม ", "")
                    bc = ("ตำบักหุ่งบ่")
                    cb = (bctxt + bc)
                    tts = gTTS(cb, lang='th', slow=False)
                    tts.save('tts.mp3')
                    n = line.getGroupIdsJoined()
                    for manusia in n:
                        line.sendAudio(manusia, 'tts.mp3')

                elif "ส่งเสียงแชท " in msg.text:
                    bctxt = msg.text.replace("ส่งเสียงแชท ", "")
                    bc = ("ตำบักหุ่งบ่")
                    cb = (bctxt + bc)
                    tts = gTTS(cb, lang='th', slow=False)
                    tts.save('tts.mp3')
                    n = line.getAllContactIdsJoined()
                    for manusia in n:
                        line.sendAudio(manusia, 'tts.mp3')
                    
                elif text.lower() == 'ปฏิทิน':
                    tz = pytz.timezone("Asia/Jakarta")
                    timeNow = datetime.now(tz=tz)
                    day = ["Sunday", "Monday", "Tuesday", "Wednesday", "Thursday","Friday", "Saturday"]
                    hari = ["วันอาทิตย์", "วันจันทร์", "วันอังคาร", "วันพุธ", "วันพฤหัสบดี", "วันศุกร์", "วันเสาร์"]
                    bulan = ["Januari", "Februari", "Maret", "April", "Mei", "Juni", "Juli", "Agustus", "September", "Oktober", "November", "Desember"]
                    hr = timeNow.strftime("%A")
                    bln = timeNow.strftime("%m")
                    for i in range(len(day)):
                        if hr == day[i]: hasil = hari[i]
                    for k in range(0, len(bulan)):
                        if bln == str(k): bln = bulan[k-1]
                    readTime = "🌴ปฏิทินโดย✯ѕειт вот чєєωα✯🌴\n\n🌿🌸🍃🌸🍃🌸🍃🌸🍃🌸🍃🌸🌿" + "\n\n🍁" + hasil + "\n🍁 ที่ " + timeNow.strftime('%d') + " - " + bln + " - " + timeNow.strftime('%Y')  + "\n🍁 เวลา : [ " + timeNow.strftime('%H:%M:%S') + " ]" + "🌿🌸🍃🌸🍃🌸🍃🌸🍃🌸🍃🌸🌿" + "\n\nBY: ™『◐✯ѕειт вот чєєωα✯◐』"
                    line.sendMessage(msg.to, readTime)

                elif "screenshotwebsite " in msg.text.lower():
                    sep = text.split(" ")
                    query = text.replace(sep[0] + " ","")
                    with requests.session() as web:
                        r = web.get("http://rahandiapi.herokuapp.com/sswebAPI?key=betakey&link={}".format(urllib.parse.quote(query)))
                        data = r.text
                        data = json.loads(data)
                        line.sendImageWithURL(to, data["result"])

                elif ".รูปภาพ " in msg.text.lower():
                    separate = msg.text.split(" ")
                    search = msg.text.replace(separate[0] + " ","")
                    with requests.session() as web:
                        web.headers["User-Agent"] = random.choice(settings["userAgent"])
                        r = web.get("http://rahandiapi.herokuapp.com/imageapi?key=betakey&q={}".format(urllib.parse.quote(search)))
                        data = r.text
                        data = json.loads(data)
                        if data["result"] != []:
                            items = data["result"]
                            path = random.choice(items)
                            a = items.index(path)
                            b = len(items)
                            line.sendImageWithURL(to, str(path))
                elif "รูปการ์ตูน " in msg.text.lower():
                    separate = msg.text.split(" ")
                    search = msg.text.replace(separate[0] + " ","")
                    with requests.session() as web:
                        web.headers["User-Agent"] = random.choice(settings["userAgent"])
                        r = web.get("http://rahandiapi.herokuapp.com/imageapi?key=betakey&q={}".format(urllib.parse.quote(search)))
                        data = r.text
                        data = json.loads(data)
                        if data["result"] != []:
                            items = data["result"]
                            path = random.choice(items)
                            a = items.index(path)
                            b = len(items)
                            line.sendImageWithURL(to, str(path))
      
                elif "ยูทูป " in msg.text.lower():
                    sep = text.split(" ")
                    search = text.replace(sep[0] + " ","")
                    params = {"search_query": search}
                    with requests.session() as web:
                        web.headers["User-Agent"] = random.choice(settings["userAgent"])
                        r = web.get("https://www.youtube.com/results", params = params)
                        soup = BeautifulSoup(r.content, "html.parser")
                        ret_ = "╔══[ ผลการค้นหา ]"
                        datas = []
                        for data in soup.select(".yt-lockup-title > a[title]"):
                            if "&lists" not in data["href"]:
                                datas.append(data)
                        for data in datas:
                            ret_ += "\n╠══[ {} ]".format(str(data["title"]))
                            ret_ += "\n╠ https://www.youtube.com{}".format(str(data["href"]))
                        ret_ += "\n╚══[ จำนวนที่พบ {} ]".format(len(datas))
                        line.sendMessage(to, str(ret_))
#===========BOT UPDATE BY NOXTIAN============#
                elif msg.text.lower().startswith("แทค"):
                  if msg._from in admin:						
                    data = msg.text[len("แทค"):].strip()
                    if data == "":
                        group = line.getGroup(msg.to)
                        nama = [contact.mid for contact in group.members if contact.mid != zxcv]
                        cb = ""
                        cb2 = ""
                        count = 1
                        strt = len(str(count)) + 2
                        akh = int(0)
                        cnt = 0
                        for md in nama:
                            akh = akh + len(str(count)) + 2 + 5
                            cb += """{"S":"""+json.dumps(str(strt))+""","E":"""+json.dumps(str(akh))+""","M":"""+json.dumps(md)+"},"""
                            strt = strt + len(str(count+1)) + 2 + 6
                            akh = akh + 1
                            cb2 += str(count)+". @name\n"
                            cnt = cnt + 1
                            if cnt == 20:
                                cb = (cb[:int(len(cb)-1)])
                                cb2 = cb2[:-1]
                                msg.contentType = 0
                                msg.text = cb2
                                msg.contentMetadata ={'MENTION':'{"MENTIONEES":['+cb+']}','EMTVER':'4'}
                                try:
                                    line.sendMessage(msg.to,text = cb2,contentMetadata ={'MENTION':'{"MENTIONEES":['+cb+']}','EMTVER':'4'},contentType = 0)
                                except:
                                    line.sendText(msg.to,"[[NO MENTION]]")
                                cb = ""
                                cb2 = ""
                                strt = len(str(count)) + 2
                                akh = int(0)
                                cnt = 0
                            count += 1
                        cb = (cb[:int(len(cb)-1)])
                        cb2 = cb2[:-1]
                        msg.contentType = 0
                        msg.text = cb2
                        msg.contentMetadata ={'MENTION':'{"MENTIONEES":['+cb+']}','EMTVER':'4'}
                        try:
                            line.sendMessage(msg.to,text = cb2,contentMetadata ={'MENTION':'{"MENTIONEES":['+cb+']}','EMTVER':'4'},contentType = 0)
                        except:
                            line.sendText(msg.to,"[[NO MENTION]]")
                    elif data[0] == "<":
                        mentargs = int(data[1:].strip())
                        group = line.getGroup(msg.to)
                        nama = [contact.mid for contact in group.members if contact.mid != zxcv]
                        cb = ""
                        cb2 = ""
                        count = 1
                        strt = len(str(count)) + 2
                        akh = int(0)
                        cnt = 0
                        for md in nama:
                            if count > mentargs:
                                break
                            akh = akh + len(str(count)) + 2 + 5
                            cb += """{"S":"""+json.dumps(str(strt))+""","E":"""+json.dumps(str(akh))+""","M":"""+json.dumps(md)+"},"""
                            strt = strt + len(str(count+1)) + 2 + 6
                            akh = akh + 1
                            cb2 += str(count)+". @name\n"
                            cnt = cnt + 1
                            if cnt == 20:
                                cb = (cb[:int(len(cb)-1)])
                                cb2 = cb2[:-1]
                                msg.contentType = 0
                                msg.text = cb2
                                msg.contentMetadata ={'MENTION':'{"MENTIONEES":['+cb+']}','EMTVER':'4'}
                                try:
                                    line.sendMessage(msg.to,text = cb2,contentMetadata ={'MENTION':'{"MENTIONEES":['+cb+']}','EMTVER':'4'},contentType = 0)
                                except:
                                    line.sendText(msg.to,"[[NO MENTION]]")
                                cb = ""
                                cb2 = ""
                                strt = len(str(count)) + 2
                                akh = int(0)
                                cnt = 0
                            count += 1
                        cb = (cb[:int(len(cb)-1)])
                        cb2 = cb2[:-1]
                        msg.contentType = 0
                        msg.text = cb2
                        msg.contentMetadata ={'MENTION':'{"MENTIONEES":['+cb+']}','EMTVER':'4'}
                        try:
                            line.sendMessage(msg.to,text = cb2,contentMetadata ={'MENTION':'{"MENTIONEES":['+cb+']}','EMTVER':'4'},contentType = 0)
                        except:
                            line.sendText(msg.to,"[[NO MENTION]]")
                    elif data[0] == ">":
                        mentargs = int(data[1:].strip())
                        group = line.getGroup(msg.to)
                        nama = [contact.mid for contact in group.members if contact.mid != zxcv]
                        cb = ""
                        cb2 = ""
                        count = 1
                        if mentargs >= 0:
                            strt = len(str(mentargs)) + 2
                        else:
                            strt = len(str(count)) + 2
                        akh = int(0)
                        cnt = 0
                        for md in nama:
                            if count < mentargs:
                                count += 1
                                continue
                            akh = akh + len(str(count)) + 2 + 5
                            cb += """{"S":"""+json.dumps(str(strt))+""","E":"""+json.dumps(str(akh))+""","M":"""+json.dumps(md)+"},"""
                            strt = strt + len(str(count+1)) + 2 + 6
                            akh = akh + 1
                            cb2 += str(count)+". @name\n"
                            cnt = cnt + 1
                            if cnt == 20:
                                cb = (cb[:int(len(cb)-1)])
                                cb2 = cb2[:-1]
                                msg.contentType = 0
                                msg.text = cb2
                                msg.contentMetadata ={'MENTION':'{"MENTIONEES":['+cb+']}','EMTVER':'4'}
                                try:
                                    line.sendMessage(msg.to,text = cb2,contentMetadata ={'MENTION':'{"MENTIONEES":['+cb+']}','EMTVER':'4'},contentType = 0)
                                except:
                                    line.sendText(msg.to,"[[NO MENTION]]")
                                cb = ""
                                cb2 = ""
                                strt = len(str(count)) + 2
                                akh = int(0)
                                cnt = 0
                            count += 1
                        cb = (cb[:int(len(cb)-1)])
                        cb2 = cb2[:-1]
                        msg.contentType = 0
                        msg.text = cb2
                        msg.contentMetadata ={'MENTION':'{"MENTIONEES":['+cb+']}','EMTVER':'4'}
                        try:
                            line.sendMessage(msg.to,text = cb2,contentMetadata ={'MENTION':'{"MENTIONEES":['+cb+']}','EMTVER':'4'},contentType = 0)
                        except:
                            line.sendText(msg.to,"[[NO MENTION]]")
                    elif data[0] == "=":
                        mentargs = int(data[1:].strip())
                        group = line.getGroup(msg.to)
                        nama = [contact.mid for contact in group.members if contact.mid != zxcv]
                        cb = ""
                        cb2 = ""
                        count = 1
                        akh = int(0)
                        cnt = 0
                        for md in nama:
                            if count != mentargs:
                                count += 1
                                continue
                            akh = akh + len(str(count)) + 2 + 5
                            strt = len(str(count)) + 2
                            cb += """{"S":"""+json.dumps(str(strt))+""","E":"""+json.dumps(str(akh))+""","M":"""+json.dumps(md)+"},"""
                            strt = strt + len(str(count+1)) + 2 + 6
                            akh = akh + 1
                            cb2 += str(count)+". @name\n"
                            cnt = cnt + 1
                            if cnt == 20:
                                cb = (cb[:int(len(cb)-1)])
                                cb2 = cb2[:-1]
                                msg.contentType = 0
                                msg.text = cb2
                                msg.contentMetadata ={'MENTION':'{"MENTIONEES":['+cb+']}','EMTVER':'4'}
                                try:
                                    line.sendMessage(msg.to,text = cb2,contentMetadata ={'MENTION':'{"MENTIONEES":['+cb+']}','EMTVER':'4'},contentType = 0)
                                except:
                                    line.sendText(msg.to,"[[NO MENTION]]")
                                cb = ""
                                cb2 = ""
                                strt = len(str(count)) + 2
                                akh = int(0)
                                cnt = 0
                            count += 1
                        cb = (cb[:int(len(cb)-1)])
                        cb2 = cb2[:-1]
                        msg.contentType = 0
                        msg.text = cb2
                        msg.contentMetadata ={'MENTION':'{"MENTIONEES":['+cb+']}','EMTVER':'4'}
                        try:
                            line.sendMessage(msg.to,text = cb2,contentMetadata ={'MENTION':'{"MENTIONEES":['+cb+']}','EMTVER':'4'},contentType = 0)
                        except:
                            line.sendText(msg.to,"[[NO MENTION]]")
#===========BOT UPDATE============#                        
                elif "google " in msg.text.lower():
                    spl = re.split("google ",msg.text,flags=re.IGNORECASE)
                    if spl[0] == "":
                        if spl[1] != "":
                                try:
                                    if msg.toType != 0:
                                        line.sendText(msg.to,"กำลังรับข้อมูล กรุณารอสักครู่..")
                                    else:
                                        line.sendText(msg.from_,"กำลังรับข้อมูล กรุณารอสักครู่..")
                                    resp = BeautifulSoup(requests.get("https://www.google.co.th/search",params={"q":spl[1],"gl":"th"}).content,"html.parser")
                                    text = "ผลการค้นหาจาก Google:\n\n"
                                    for el in resp.findAll("h3",attrs={"class":"r"}):
                                        try:
                                                tmp = el.a["class"]
                                                continue
                                        except:
                                                pass
                                        try:
                                                if el.a["href"].startswith("/search?q="):
                                                    continue
                                        except:
                                                continue
                                        text += el.a.text+"\n"
                                        text += str(el.a["href"][7:]).split("&sa=U")[0]+"\n\n"
                                    text = text[:-2]
                                    if msg.toType != 0:
                                        line.sendText(msg.to,str(text))
                                    else:
                                        line.sendText(msg.from_,str(text))
                                except Exception as e:
                                    print(e)
                        
                elif "วีดีโอ " in msg.text.lower():
                    sep = text.split(" ")
                    search = text.replace(sep[0] + "วีดีโอ ","")
                    params = {"search_query": search}
                    with requests.session() as web:
                        web.headers["User-Agent"] = random.choice(settings["userAgent"])
                        r = web.get("https://www.youtube.com/results", params = params)
                        soup = BeautifulSoup(r.content, "html.parser")
                        ret_ = "╔══[ ผลการค้นหา ]"
                        datas = []
                        for data in soup.select(".yt-lockup-title > a[title]"):
                            if "&lists" not in data["href"]:
                                datas.append(data)
                        for data in datas:
                            ret_ += "\n╠══[ {} ]".format(str(data["title"]))
                            ret_ += "\n╠ https://www.youtube.com{}".format(str(data["href"]))
                        ret_ += "\n╚══[ จำนวนที่พบ {} ]".format(len(datas))
                        line.sendMessage(to, str(ret_))
                        
                elif "หนัง " in msg.text.lower():
                    sep = text.split(" ")
                    search = text.replace(sep[0] + "หนัง ","")
                    params = {"search_query": search}
                    with requests.session() as web:
                        web.headers["User-Agent"] = random.choice(settings["userAgent"])
                        r = web.get("https://www.youtube.com/results", params = params)
                        soup = BeautifulSoup(r.content, "html.parser")
                        ret_ = "╔══[ ผลการค้นหา ]"
                        datas = []
                        for data in soup.select(".yt-lockup-title > a[title]"):
                            if "&lists" not in data["href"]:
                                datas.append(data)
                        for data in datas:
                            ret_ += "\n╠══[ {} ]".format(str(data["title"]))
                            ret_ += "\n╠ https://www.youtube.com{}".format(str(data["href"]))
                        ret_ += "\n╚══[ จำนวนที่พบ {} ]".format(len(datas))
                        line.sendMessage(to, str(ret_))
                        
                elif "เพลง " in msg.text.lower():
                    sep = text.split(" ")
                    search = text.replace(sep[0] + "เพลง ","")
                    params = {"search_query": search}
                    with requests.session() as web:
                        web.headers["User-Agent"] = random.choice(settings["userAgent"])
                        r = web.get("https://www.youtube.com/results", params = params)
                        soup = BeautifulSoup(r.content, "html.parser")
                        ret_ = "╔══[ ผลการค้นหา ]"
                        datas = []
                        for data in soup.select(".yt-lockup-title > a[title]"):
                            if "&lists" not in data["href"]:
                                datas.append(data)
                        for data in datas:
                            ret_ += "\n╠══[ {} ]".format(str(data["title"]))
                            ret_ += "\n╠ https://www.youtube.com{}".format(str(data["href"]))
                        ret_ += "\n╚══[ จำนวนที่พบ {} ]".format(len(datas))
                        line.sendMessage(to, str(ret_))

                elif msg.text in ["เปิดแสกน"]:
                    try:
                        del RfuCctv['point'][msg.to]
                        del RfuCctv['sidermem'][msg.to]
                        del RfuCctv['cyduk'][msg.to]
                    except:
                        pass
                    RfuCctv['point'][msg.to] = msg.id
                    RfuCctv['sidermem'][msg.to] = ""
                    RfuCctv['cyduk'][msg.to]=True
                    line.sendMessage(msg.to,"เปิดระบบแสกนคนอ่านอัตโนมัติ\n『◐✯ѕειт вот чєєωα✯◐』")
                elif msg.text in ["ปิดแสกน"]:
                    if msg.to in RfuCctv['point']:
                        RfuCctv['cyduk'][msg.to]=False
                        line.sendText(msg.to, RfuCctv['sidermem'][msg.to])
                    else:
                        line.sendMessage(msg.to, "ปิดระบบแสกนคนอ่านแล้ว\n『◐✯ѕειт вот чєєωα✯◐』")

                elif text.lower() == 'ปิดเซล':
                    line.sendMessage(receiver, 'หยุดการทำงานเซลบอทเรียบร้อย\n『◐✯ѕειт вот чєєωα✯◐』')
                    print ("Selfbot Off")
                    exit(1)
                elif text.lower() == "ลบแชท":
                        if msg._from in lineMID:
                            try:
                                line.removeAllMessages(op.param2)
                                line.sendMessage(msg.to,"ลบทุกการแชทเรียบร้อย\n『◐✯ѕειт вот чєєωα✯◐』")
                            except:
                                pass
                                print ("ลบแชท")
                elif text.lower() == 'เพื่อน':
                    contactlist = line.getAllContactIds()
                    kontak = line.getContacts(contactlist)
                    num=1
                    msgs="🎎รายชื่อเพื่อนทั้งหมด🎎"
                    for ids in kontak:
                        msgs+="\n[%i] %s" % (num, ids.displayName)
                        num=(num+1)
                    msgs+="\n🎎รายชื่อเพื่อนทั้งหมด🎎\n\nมีดังต่อไปนี้ : %i" % len(kontak)
                    line.sendMessage(msg.to, msgs)

                elif msg.text in ["เช็คบล็อค"]: 
                    blockedlist = line.getBlockedContactIds()
                    kontak = line.getContacts(blockedlist)
                    num=1
                    msgs="═════ไม่มีรายการบัญชีที่ถูกบล็อค═════"
                    for ids in kontak:
                        msgs+="\n[%i] %s" % (num, ids.displayName)
                        num=(num+1)
                    msgs+="\n════════รายการบัญชีที่ถูกบล็อค════════\n\nTotal Blocked : %i" % len(kontak)
                    line.sendMessage(receiver, msgs)

                elif msg.text in ["ไอดีเพื่อน"]: 
                    gruplist = line.getAllContactIds()
                    kontak = line.getContacts(gruplist)
                    num=1
                    msgs="═════════รายการไอดีเพื่อน═════════"
                    for ids in kontak:
                        msgs+="\n[%i] %s" % (num, ids.mid)
                        num=(num+1)
                    msgs+="\n═════════รายการ ไอดีเพื่อน═════════\n\nTotal Friend : %i" % len(kontak)
                    line.sendMessage(receiver, msgs)

                elif msg.text.lower() == 'gurl':
                	if msg.toType == 2:
                         g = line.getGroup(receiver)
                         line.updateGroup(g)
                         gurl = line.reissueGroupTicket(receiver)
                         line.sendMessage(receiver,"╔══════════════┓\n╠❂line://ti/g/" + gurl + "\n╠\n╠❂Link Groupnya Tanpa Buka Qr\n╚══════════════┛")

                elif msg.text == "เว็บโป๊":
                	line.sendMessage(receiver,">nekopoi.host\n>sexvideobokep.com\n>memek.com\n>pornktube.com\n>faketaxi.com\n>videojorok.com\n>watchmygf.mobi\n>xnxx.com\n>pornhd.com\n>xvideos.com\n>vidz7.com\n>m.xhamster.com\n>xxmovies.pro\n>youporn.com\n>pornhub.com\n>youjizz.com\n>thumzilla.com\n>anyporn.com\n>brazzers.com\n>redtube.com\n>youporn.com")
                elif msg.text == "ประกาศ":
                	line.sendMessage(msg.to,str(settings["message1"]))
                elif msg.text.lower() == 'ดึงแอด':
                	if msg.toType == 2:                
                           ginfo = line.getGroup(receiver)
                           try:
                               gcmid = ginfo.creator.mid
                           except:
                               gcmid = "Error"
                           if settings["lang"] == "JP":
                               line.inviteIntoGroup(receiver,[gcmid])
                               line.sendMessage(receiver, "Type👉 Invite Pembuat Group Succes")
                           else:
                               line.inviteIntoGroup(receiver,[gcmid])
                               line.sendMessage(receiver, "Pembuat Group Sudah di dalam")

                elif msg.text in ["ไม่รับเชิญ"]:
                    if msg.toType == 2:
                        ginfo = line.getGroup(receiver)
                        try:
                            line.leaveGroup(receiver)							
                        except:
                            pass
                elif msg.text in ["เช็คไอดี"]: 
                    gruplist = line.getAllContactIds()
                    kontak = line.getContacts(gruplist)
                    num=1
                    msgs="™『✯ᴛᴏᴍᴇʙᴏᴛʟɪɴᴇ✯』"
                    for ids in kontak:
                        msgs+="\n[%i] %s" % (num, ids.mid)
                        num=(num+1)
                    msgs+="\nจำนวน  %i" % len(kontak)
                    line.sendMessage(receiver, msgs)

                elif msg.text in ["เปิดแทคเจ็บ"]:
                    settings["kickMention"] = True
                    line.sendMessage(msg.to,"เปิดระบบเตะคนแท็ก\n\n『◐✯ARM SELFBOT✯◐』")
                
                elif msg.text in ["ปิดแทคเจ็บ"]:
                    settings["kickMention"] = False
                    line.sendMessage(msg.to,"ปิดระบบเตะคนแท็ก\n\n『◐✯ARM SELFBOT✯◐』")
                    
                elif msg.text in ["เปิดแทค","Tag on"]:
                        settings['detectMention'] = True
                        line.sendMessage(msg.to,"Respon enabled.\n\n『◐✯ѕειт вот чєєωα✯◐』")
                
                elif msg.text in ["ปิดแทค","Tag off"]:
                        settings['detectMention'] = False
                        line.sendMessage(msg.to,"Respon disabled.\n\n『◐✯ARM SELFBOT✯◐』")

                elif msg.text in ["เปิดแทค2"]:
                    settings["potoMention"] = True
                    line.sendMessage(msg.to,"AutoRespon enabled.\n\n『◐✯ARM SELFBOT✯◐』")
                
                elif msg.text in ["ปิดแทค2"]:
                    settings["potoMention"] = False
                    line.sendMessage(msg.to,"Autorespon disabled.\n\n『◐✯ARM SELFBOT✯◐』")
                    
                elif msg.text in ["เปิดแทค3"]:
                    settings["delayMention"] = True
                    line.sendMessage(msg.to,"เปิดระบบแทคกลับคนแทค(○ﾟεﾟ○)\n\n『◐✯ARM SELFBOT✯◐』")
                
                elif msg.text in ["ปิดแทค3"]:
                    settings["delayMention"] = False
                    line.sendMessage(msg.to,"ปิดระบบแทคกลับคนแทค(ˉ(∞)ˉ)\n\n『◐✯ARM SELFBOT✯◐』")
                elif msg.text.lower() == "เปิดแทคแชท":
                    settings["detectMentionPM"] = True
                    line.sendMessage(msg.to,"เปิดแทคแชทเรียบร้อยครับ\n\n『◐✯ARM SELFBOT✯◐』")
                elif msg.text.lower() == "ปิดแทคแชท":
                    settings["detectMentionPM"] = False
                    line.sendMessage(msg.to,"ปิดแทคแชทเรียบร้อยครับ\n\n『◐✯ARM SELFBOT✯◐』")
                elif msg.text.lower().startswith("ตั้งแทคแชท: "):
                    text = msg.text.lower().replace("ตั้งแทคแชท: ","")
                    settings["pmMessage"] = text
                    line.sendMessage(msg.to, "คำแทคแชท สต คือ : {}".format(str(settings["pmMessage"])))
                elif msg.text.lower().startswith("setrespongroup: "):
                    text = msg.text.lower().replace("setrespongroup: ","")
                    settings["respMessage"] = text
                    line.sendMessage(msg.to, "Success Update Response Group to : {}".format(str(settings["respMessage"])))
                    
                elif msg.text in ["เปิดตรวจสอบ"]:
                    settings["Aip"] = True
                    line.sendMessage(msg.to,"เปิดระบบตรวจสอบคำหยาบกับบอทบิน  ^ω^\n\n『◐✯ARM SELFBOT✯◐』")
                
                elif msg.text in ["ปิดตรวจสอบ"]:
                    settings["Aip"] = False
                    line.sendMessage(msg.to,"ปิดระบบตรวจสอบคำหยาบกับบอทบินแล้วʕ•ﻌ•ʔ\n\n『◐✯ARM SELFBOT✯◐』")
                    
                elif msg.text in ["เปิดพูด"]:
                    icon = "http://dl.profile.line.naver.jp/"+lineProfile.pictureStatus
                    name = "คำสั่งบอทตาต้อม"                   
                    link = "http://line.me/ti/p/~tome2527"
                    settings["Api"] = True
                    line.sendFooter(msg.to,"เปิดระบบApiข้อความ",link ,icon,name)
                
                elif msg.text in ["ปิดพูด"]:
                    icon = "http://dl.profile.line.naver.jp/"+lineProfile.pictureStatus
                    name = "คำสั่งบอทตาต้อม"                   
                    link = "http://line.me/ti/p/~tome2527"
                    settings["Api"] = False
                    line.sendFooter(msg.to,"ปิดระบบApiข้อความแล้ว\n\n『◐✯ARM SELFBOT✯◐』",link ,icon,name)
                    
                elif 'ตั้งแอด: ' in msg.text:
                  if msg._from in admin:
                    icon = "http://dl.profile.line.naver.jp/"+lineProfile.pictureStatus
                    name = "คำสั่งบอทตาต้อม"                   
                    link = "http://line.me/ti/p/~tome2527"
                    spl = msg.text.replace('ตั้งแอด: ','')
                    if spl in [""," ","\n",None]:
                        line.sendMessage(msg.to, "ตั้งข้อความเรืยบร้อย\n\n『◐✯ARM SELFBOT✯◐』")
                    else:
                        settings["message"] = spl
                        line.sendFooter(msg.to, "™『◐✯ARM SELFBOT✯◐』\n👇ตั้งข้อความตอบโต้เมื่อมีคนแอดแล้ว ดังนี้\n\n👉{}".format(str(spl)),link ,icon,name)
                         
                elif 'คอมเม้น: ' in msg.text:
                  if msg._from in admin:
                    icon = "http://dl.profile.line.naver.jp/"+lineProfile.pictureStatus
                    name = "คำสั่งบอทตาต้อม"                   
                    link = "http://line.me/ti/p/~tome2527"
                    spl = msg.text.replace('คอมเม้น: ','')
                    if spl in [""," ","\n",None]:
                        line.sendFooter(msg.to, "ตั้งข้อความเรืยบร้อย\n\n『◐✯ARM SELFBOT✯◐』"),link ,icon,name
                    else:
                        settings["comment1"] = spl
                        line.sendMessage(msg.to, "™『◐✯ARM SELFBOT✯◐』\n👇ตั้งข้อความคอมเม้นของคุณแล้ว ดังนี้\n\n👉{}".format(str(spl))) 
                    
                elif 'ตั้งแทค: ' in msg.text:
                  if msg._from in admin:
                    icon = "http://dl.profile.line.naver.jp/"+lineProfile.pictureStatus
                    name = "คำสั่งบอทตาต้อม"                   
                    link = "http://line.me/ti/p/~tome2527"
                    spl = msg.text.replace('ตั้งแทค: ','')
                    if spl in [""," ","\n",None]:
                        line.sendFooter(msg.to, "ตั้งข้อความเรืยบร้อย\n\n◐✯ARM SELFBOT✯◐"),link ,icon,name
                    else:
                        settings["Respontag"] = spl
                        line.sendFooter(msg.to, "™『◐✯ARM SELFBOT✯◐』\n👇ตั้งข้อความตอบโต้เมื่อมีคนแทคแล้ว\n\n👉{}".format(str(spl)),link ,icon,name)
                         
                elif 'ทักเตะ: ' in msg.text:
                  if msg._from in admin:
                    icon = "http://dl.profile.line.naver.jp/"+lineProfile.pictureStatus
                    name = "คำสั่งบอทตาต้อม"                   
                    link = "http://line.me/ti/p/~tome2527"
                    spl = msg.text.replace('ทักเตะ: ','')
                    if spl in [""," ","\n",None]:
                        line.sendMessage(msg.to, "ตั้งข้อความคนคนลบสมาชิดเรียบร้อย\n\n『◐✯ARM SELFBOT✯◐』")
                    else:
                         settings["kick"] = spl
                         line.sendFooter(msg.to, "™『◐✯ARM SELFBOT✯◐』\nตั้งค่าข้อความเมื่อมีคนลบสมาชิกแล้ว\nดังนี้\n\n👉{}".format(str(spl)),link ,icon,name)

                elif 'ทักออก: ' in msg.text:
                  if msg._from in admin:
                    icon = "http://dl.profile.line.naver.jp/"+lineProfile.pictureStatus
                    name = "คำสั่งบอทตาต้อม"                   
                    link = "http://line.me/ti/p/~tome2527"
                    spl = msg.text.replace('ทักออก: ','')
                    if spl in [""," ","\n",None]:
                        line.sendMessage(msg.to, "ตั้งข้อความคนออกเรียบร้อย\n\n『◐✯ARM SELFBOT✯◐』")
                    else:
                         settings["bye"] = spl
                         line.sendFooter(msg.to, "™『◐✯ARM SELFBOT✯◐』\nตั้งค่าข้อความเมื่อมีคนออกจากกลุ่มแล้ว\nดังนี้👇\n\n👉{}".format(str(spl)),link ,icon,name)

                elif 'ทักเข้า: ' in msg.text:
                  if msg._from in admin:
                    icon = "http://dl.profile.line.naver.jp/"+lineProfile.pictureStatus
                    name = "คำสั่งบอทตาต้อม"                   
                    link = "http://line.me/ti/p/~tome2527"
                    spl = msg.text.replace('ทักเข้า: ','')
                    if spl in [""," ","\n",None]:
                        line.sendMessage(msg.to, "ตั้งข้อความคนเข้าเรียบร้อยแล้ว\n\n『◐✯ARM SELFBOT✯◐』")
                    else:
                         settings["welcome"] = spl
                         line.sendFooter(msg.to, "™『◐✯ARM SELFBOT✯◐』\nตั้งค่าข้อความเมื่อมีคนเข้ากลุ่มแล้ว\nดังนี้👇\n\n👉{}".format(str(spl)),link ,icon,name)
                elif msg.text.lower() == "เปิดกันติ๊ก":
                        settings["sticker"] = True
                        line.sendMessage(to,"เปิดเตะคนรันสติกเกอรแล้ว\n\n◐✯ARM SELFBOT✯◐")
                elif msg.text.lower() == "ปิดกันติ๊ก":
                        settings["sticker"] = False
                        line.sendMessage(to,"ปิดเตะคนรันสติกเกอรแล้ว\n\n『◐✯ARM SELFBOT✯◐』")
                elif msg.text.lower() == "sleepmode":
                    if settings["replyPesan"] is not None:
                        line.sendMessage(to,"Your Sleepmode is : " + str(settings["replyPesan"]))
                        msgSticker = settings["messageSticker"]["listSticker"]["sleepSticker"]
                        if msgSticker != None:
                            sid = msgSticker["STKID"]
                            spkg = msgSticker["STKPKGID"]
                            sver = msgSticker["STKVER"]
                            sendSticker(to, sver, spkg, sid)
                    else:
                        line.sendMessage(to,"My Sleepmode : No messages are set")
                elif msg.text.lower() == "addsleepmodesticker":
                    settings["messageSticker"]["addStatus"] = True
                    settings["messageSticker"]["addName"] = "sleepSticker"
                    line.sendMessage(to, "โปรดส่งสติ๊กเกอร์ที่คุณต้องการเพิ่ม")
                elif msg.text.lower() == "delsleepmodesticker":
                    settings["messageSticker"]["listSticker"]["sleepSticker"] = None
                    line.sendMessage(to, "ลบรายการสติ๊กเกอร์เรียบร้อย\n\n『◐✯ARM SELFBOT✯◐』")
                elif msg.text.lower().startswith("setsleepmode: "):
                    text_ = msg.text.lower().replace("setsleepmode:", "")
                    try:
                        settings["replyPesan"] = text_
                        line.sendMessage(to,"Sleep mode changed to : " + text_)
                    except:
                        line.sendMessage(to,"SleepMode \nFailed to replace message")
                elif msg.text.lower() == "ติ๊กคนออก":
                        msgSticker = settings["messageSticker"]["listSticker"]["leaveSticker"]
                        if msgSticker != None:
                            sid = msgSticker["STKID"]
                            spkg = msgSticker["STKPKGID"]
                            sver = msgSticker["STKVER"]
                            sendSticker(to, sver, spkg, sid)
                elif msg.text.lower() == "ตั้งติ๊กคนออก":
                    settings["messageSticker"]["addStatus"] = True
                    settings["messageSticker"]["addName"] = "leaveSticker"
                    line.sendMessage(to, "ส่งสติกเกอรที่จะตั้งลงมา")
                elif msg.text.lower() == "ลบติ๊กคนออก":
                    settings["messageSticker"]["listSticker"]["leaveSticker"] = None
                    line.sendMessage(to, "ลบสติกเกอรคนเข้าแล้ว\n\n『◐✯ARM SELFBOT✯◐』")
                elif msg.text.lower() == "ติ๊กคนเตะ":
                        msgSticker = settings["messageSticker"]["listSticker"]["kickSticker"]
                        if msgSticker != None:
                            sid = msgSticker["STKID"]
                            spkg = msgSticker["STKPKGID"]
                            sver = msgSticker["STKVER"]
                            sendSticker(to, sver, spkg, sid)
                elif msg.text.lower() == "ตั้งติ๊กคนเตะ":
                    settings["messageSticker"]["addStatus"] = True
                    settings["messageSticker"]["addName"] = "kickSticker"
                    line.sendMessage(to, "ส่งสติกเกอรที่จะตั้งลงมา")
                elif msg.text.lower() == "ลบติ๊กคนเตะ":
                    settings["messageSticker"]["listSticker"]["kickSticker"] = None
                    line.sendMessage(to, "ลบสติกเกอรคนเตะแล้ว\n\n『◐✯ARM SELFBOT✯◐』")
                elif msg.text.lower() == "ติ๊กคนเข้า":
                        msgSticker = settings["messageSticker"]["listSticker"]["welcomeSticker"]
                        if msgSticker != None:
                            sid = msgSticker["STKID"]
                            spkg = msgSticker["STKPKGID"]
                            sver = msgSticker["STKVER"]
                            sendSticker(to, sver, spkg, sid)
                elif msg.text.lower() == "ตั้งติ๊กคนเข้า":
                    settings["messageSticker"]["addStatus"] = True
                    settings["messageSticker"]["addName"] = "welcomeSticker"
                    line.sendMessage(to, "ส่งสติกเกอรที่จะตั้งลงมา")
                elif msg.text.lower() == "ลบติ๊กคนเข้า":
                    settings["messageSticker"]["listSticker"]["welcomeSticker"] = None
                    line.sendMessage(to, "ลบสติกเกอรคนเข้าแล้ว\n\n『◐✯ARM SELFBOT✯◐』")
                elif msg.text.lower()== "ติ๊กคนแอด":
                        msgSticker = settings["messageSticker"]["listSticker"]["addSticker"]
                        if msgSticker != None:
                            sid = msgSticker["STKID"]
                            spkg = msgSticker["STKPKGID"]
                            sver = msgSticker["STKVER"]
                            sendSticker(to, sver, spkg, sid)
                elif msg.text.lower()== "ตั้งติ๊กคนแอด":
                    settings["messageSticker"]["addStatus"] = True
                    settings["messageSticker"]["addName"] = "addSticker"
                    line.sendMessage(to, "ส่งสติกเกอรที่จะใช่ลงมา")
                elif msg.text.lower() == "ลบติ๊กคนแอด":
                    settings["messageSticker"]["listSticker"]["addSticker"] = None
                    line.sendMessage(to, "ลบสติกเกอรคนแทคแล้ว\n\n『◐✯ARM SELFBOT✯◐』")
                elif msg.text.lower() == "ติ๊กคนแทค":
                        msgSticker = settings["messageSticker"]["listSticker"]["responSticker"]
                        if msgSticker != None:
                            sid = msgSticker["STKID"]
                            spkg = msgSticker["STKPKGID"]
                            sver = msgSticker["STKVER"]
                            sendSticker(to, sver, spkg, sid)
                elif msg.text.lower() == "ตั้งติ๊กคนแทค":
                    settings["messageSticker"]["addStatus"] = True
                    settings["messageSticker"]["addName"] = "responSticker"
                    line.sendMessage(to, "ส่งสติกเกอรที่จะใช่ลงมา")
                elif msg.text.lower() == "ลบติ๊กคนแทค":
                    settings["messageSticker"]["listSticker"]["responSticker"] = None
                    line.sendMessage(to, "ลบสติกเกอรคนแทคแล้ว\n\n『◐✯ARM SELFBOT✯◐』")
                elif msg.text.lower() == "ตั้งติ๊กคนแอบ":
                    settings["messageSticker"]["addStatus"] = True
                    settings["messageSticker"]["addName"] = "readerSticker"
                    line.sendMessage(to, "ส่งสติ๊กเกอรที่จะใช่ลงมา")
                elif msg.text.lower() == "ลบติ๊กคนแอบ":
                    settings["messageSticker"]["listSticker"]["readerSticker"] = None
                    line.sendMessage(to, "ลบสติ๊กเกอรคนแอบอ่านแล้ว\n\n『◐✯ARM SELFBOT✯◐』")
                elif msg.text.lower() == "ติ๊กคนแอบ":
                        msgSticker = settings["messageSticker"]["listSticker"]["readerSticker"]
                        if msgSticker != None:
                            sid = msgSticker["STKID"]
                            spkg = msgSticker["STKPKGID"]
                            sver = msgSticker["STKVER"]
                            sendSticker(to, sver, spkg, sid)
                elif msg.text.lower().startswith("textig "):
                    sep = msg.text.split(" ")
                    textnya = msg.text.replace(sep[0] + " ","")
                    urlnya = "http://chart.apis.google.com/chart?chs=480x80&cht=p3&chtt=" + textnya + "&chts=FFFFFF,70&chf=bg,s,000000"
                    line.sendImageWithURL(msg.to, urlnya)
                elif msg.text.lower().startswith("เขียน"):
                        sep = msg.text.split(" ")
                        textnya = msg.text.replace(sep[0] + " ","")
                        path = "http://chart.apis.google.com/chart?chs=480x80&cht=p3&chtt=" + textnya + "&chts=FFFFFF,70&chf=bg,s,000000"
                        line.sendImageWithURL(msg.to,path)
                elif "kedip " in msg.text:
                    txt = msg.text.replace("kedip ", "")
                    t1 = "\xf4\x80\xb0\x82\xf4\x80\xb0\x82\xf4\x80\xb0\x82\xf4\x80\xb0\x82\xf4\x80\xa0\x81\xf4\x80\xa0\x81\xf4\x80\xa0\x81"
                    t2 = "\xf4\x80\x82\xb3\xf4\x8f\xbf\xbf"
                    line.sendMessage(msg.to, t1 + txt + t2)						
                elif msg.text in ["ดึง"]:
                        settings["winvite"] = True
                        line.sendMessage(msg.to,"send a contact to invite user")                            
                if text.lower() == 'ยกเชิญ':
                                if msg._from in bot1:
                                
                                    if msg.toType == 2:
                                        group = line.getGroup(receiver)
                                        gMembMids = [contact.mid for contact in group.invitee]
                                        k = len(gMembMids)//30
                                        line.sendMessage(msg.to,"[ ยกค้างเชิญ จำนวน {} คน] \nรอสักครู่...".format(str(len(gMembMids))))
                                        num=1
                                        for i in range(k+1):
                                            for j in gMembMids[i*30 : (i+1)*30]:
                                                time.sleep(random.uniform(0.5,0.4))
                                                line.cancelGroupInvitation(msg.to,[j])
                                                print ("[Command] "+str(num)+" => "+str(len(gMembMids))+" cancel members")
                                                num = num+1
                                            line.sendMessage(receiver,"รอสักครู่🕛เดียวยกต่อ 30 คน\n ✯ѕειт вот чєєωα✯ ")
                                            time.sleep(random.uniform(15,10))
                                        line.sendMessage(receiver,"[ ยกค้างเชิญ จำนวน {} คน เรียบร้อยแล้ว👏]".format(str(len(gMembMids))))
                                        time.sleep(random.uniform(0.95,1))
                                        line.sendMessage(receiver, None, contentMetadata={"STKID": "64104356","STKPKGID": "4108428","STKVER": "1" }, contentType=7)
                                        gname = line.getGroup(receiver).name
                                        line.sendMessage(Notify,"[ ยกค้างเชิญ >> "+gname+"  <<] \n จำนวน {} คน เรียบร้อยแล้ว👏\n ✯ѕειт вот чєєωα✯ ".format(str(len(gMembMids))))
                                        time.sleep(random.uniform(0.95,1))
                                        line.leaveGroup(receiver)
                                								
                                    line.sendMessage(receiver,"[ไม่มีค้างเชิญ แล้วนะ😁]\n◐✯ARM SELFBOT✯◐")
                                    line.sendMessage(receiver, None, contentMetadata={"STKID": "64104356","STKPKGID": "4108428","STKVER": "1" }, contentType=7)
                                    line.leaveGroup(receiver)
#=============COMMAND KICKER===========================#
                elif msg.text in ["ดำ"]:
                  if msg._from in admin: 
                    settings["wblacklist"] = True
                    line.sendText(msg.to,"กรุณาส่งคอทแทค")
                elif msg.text in ["ขาว"]:
                  if msg._from in admin: 
                    settings["dblacklist"] = True
                    line.sendText(msg.to,"กรุณาส่งคอทแทค")
                elif msg.text in ["ล้างดำ"]:
                    settings["blacklist"] = {}
                    line.sendMessage(msg.to,"ทำการลบัญชีดำทั้งหมดเรียร้อย\n\n『◐✯ARM SELFBOT✯◐』")
                    print ("Clear Ban")
                elif msg.text.lower() == "คทบล็อค":
                    if msg._from in lineMID:
                        blockedlist = line.getBlockedContactIds()
                        if blockedlist == []:
                            line.sendMessage(to, "คุณยังไม่ได้บล็อคใคร!\n\n『◐✯ARM SELFBOT✯◐』")
                        else:
                            for kontak in blockedlist:
                                line.sendMessage(to, text=None, contentMetadata={'mid': kontak}, contentType=13)
                elif msg.text.lower() == "คทดำ":
                    if msg._from in lineMID:
                        if settings["blacklist"] == []:
                            line.sendMessage(to, "Nothing boss")
                        else:
                            for bl in settings["blacklist"]:
                                line.sendMessage(to, text=None, contentMetadata={'mid': bl}, contentType=13)
                elif 'ไอ้เวร' in text.lower():
                       targets = []
                       key = eval(msg.contentMetadata["MENTION"])
                       key["MENTIONEES"] [0] ["M"]
                       for x in key["MENTIONEES"]:
                           targets.append(x["M"])
                       for target in targets:
                           try:
                               line.kickoutFromGroup(msg.to,[target])      
                               print ("Rfu kick User")
                           except:
                               line.sendMessage(msg.to,"Limit kaka 😫\n\n『◐✯ARM SELFBOT✯◐』")

                elif 'สับ' in text.lower():
                       targets = []
                       key = eval(msg.contentMetadata["MENTION"])
                       key["MENTIONEES"] [0] ["M"]
                       for x in key["MENTIONEES"]:
                           targets.append(x["M"])
                       for target in targets:
                           try:
                               line.kickoutFromGroup(msg.to,[target])             
                               print ("Sb Kick User")
                           except:
                               line.sendMessage(msg.to,"Limit kaka 😫\n\n『◐✯ARM SELFBOT✯◐』")                               

                elif 'เชิญ' in text.lower():
                       targets = []
                       key = eval(msg.contentMetadata["MENTION"])
                       key["MENTIONEES"] [0] ["M"]
                       for x in key["MENTIONEES"]:
                           targets.append(x["M"])
                       for target in targets:
                           try:
                               line.inviteIntoGroup(msg.to,[target])
                               line.sendMessage(receiver, "Type👉 Invite Succes")
                           except:
                               line.sendMessage(msg.to,"Type👉 Limit Invite")
                elif "บล็อค @" in msg.text:
                    if msg.toType == 2:
                        print ("[block] OK")
                        _name = msg.text.replace(".บล็อค @","")
                        _nametarget = _name.rstrip('  ')
                        gs = line.getGroup(msg.to)
                        targets = []
                        for g in gs.members:
                            if _nametarget == g.displayName:
                               targets.append(g.mid)
                        if targets == []:
                            sendMassage(msg.to, "Not Found...")
                        else:
                            for target in targets:
                                try:
                                   line.blockContact(target)
                                   line.sendMessage(to, "บล็อคคุณ ✈" + str(g.displayName) + " แล้ว")
                                except Exception as e:
                                   print (e)
                elif msg.text.lower() == '.บล็อค':
                    blockedlist = line.getBlockedContactIds()
                    sendMessage(msg.to, "Please wait...")
                    kontak = line.getContacts(blockedlist)
                    num=1
                    msgs="User Blocked List\n"
                    for ids in kontak:
                        msgs+="\n%i. %s" % (num, ids.displayName)
                        num=(num+1)
                        msgs+="\n\nTotal %i blocked user(s)" % len(kontak)
                        sendMessage(msg.to, msgs)
                elif "หมูหมู!" in msg.text:
                	if msg.toType == 2:
                         _name = msg.text.replace(".ปวดตับ","")
                         gs = line.getGroup(receiver)
                         line.sendMessage(receiver,"Just some casual cleansing ô")
                         targets = []
                         for g in gs.members:
                             if _name in g.displayName:
                                 targets.append(g.mid)
                         if targets == []:
                             line.sendMessage(receiver,"Not found.")
                         else:
                             for target in targets:
                             	if not target in Rfu:
                                     try:
                                         klist=[line]
                                         kicker=random.choice(klist)
                                         kicker.kickoutFromGroup(receiver,[target])
                                         print((receiver,[g.mid]))
                                     except:
                                         line.sendMessage(receiver,"Group cleanse")
                                         print ("Cleanse Group")

                elif msg.text in ["ไล่ดำ"]:
                	if msg.toType == 2:
                         group = line.getGroup(receiver)
                         gMembMids = [contact.mid for contact in group.members]
                         matched_list = []
                         for tag in settings["blacklist"]:
                             matched_list+=[str for str in gMembMids if str == tag]
                         if matched_list == []:
                             line.sendMessage(receiver,"Nots in Blacklist")
                         else:
                             for jj in matched_list:
                                 try:
                                     klist=[line]
                                     kicker=random.choice(klist)
                                     kicker.kickoutFromGroup(receiver,[jj])
                                     print((receiver,[jj]))
                                 except:
                                     line.sendMessage(receiver,"sorry bl ke cyduk")
                                     print ("Blacklist di Kick")
                elif "ชื่อ: " in text.lower():
                    if msg._from in Family:
                        proses = text.split(":")
                        string = text.replace(proses[0] + ": ","")
                        profile_A = line.getProfile()
                        profile_A.displayName = string
                        line.updateProfile(profile_A)
                        line.sendMessage(msg.to,"Update to " + string)
                        print ("Update Name")

                elif "ตัส: " in msg.text.lower():
                    if msg._from in Family:
                        proses = text.split(":")
                        string = text.replace(proses[0] + ": ","")
                        profile_A = line.getProfile()
                        profile_A.statusMessage = string
                        line.updateProfile(profile_A)
                        line.sendMessage(msg.to,"Succes Update 👉 " + string)
                        print ("Update Bio Succes")

#=============COMMAND PROTECT=========================#
                elif msg.text.lower() == 'เปิดกัน':
                    if RfuProtect["protect"] == True:
                        if settings["lang"] == "JP":
                            line.sendMessage(msg.to,"เปิดป้องกัน   \n\n『◐✯ѕειт вот ARM✯◐』", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                        else:
                            line.sendMessage(msg.to,"เปิดป้องกัน   \n\n『◐✯ѕειт вот ARM✯◐』", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                    else:
                        RfuProtect["protect"] = True
                        if settings["lang"] == "JP":
                            line.sendMessage(msg.to,"เปิดป้องกัน   \n\n『◐✯ѕειт вот ARM✯◐』", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                        else:
                            line.sendMessage(msg.to,"เปิดป้องกัน   \n\n『◐✯ѕειт вот ARM✯◐』", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})

                elif msg.text.lower() == 'ปิดกัน':
                    if RfuProtect["protect"] == False:
                        if settings["lang"] == "JP":
                            line.sendMessage(msg.to,"ปิดป้องกัน   \n\n『◐✯ѕειт вот Armtheking.🇹🇭✯◐』", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                        else:
                            line.sendMessage(msg.to,"ปิดป้องกัน   \n\n『◐✯ѕειт вот Armtheking.🇹🇭✯◐』", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                    else:
                        RfuProtect["protect"] = False
                        if settings["lang"] == "JP":
                            line.sendMessage(msg.to,"ปิดป้องกัน   \n\n『◐✯ѕειт вот Armtheking.🇹🇭✯◐』", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                        else:
                            line.sendMessage(msg.to,"ปิดป้องกัน   \n\n『◐✯ѕειт вот Armtheking.🇹🇭✯◐』", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})

                elif msg.text.lower() == 'กันยก':
                    if RfuProtect["cancelprotect"] == True:
                        if settings["lang"] == "JP":
                            line.sendMessage(msg.to,"เปิดป้องกันยกเลิกเชิญ   \n\n『◐✯ѕειт вот Armtheking.🇹🇭✯◐』", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                        else:
                            line.sendMessage(msg.to,"เปิดป้องกันยกเลิกเชิญ   \n\n『◐✯ѕειт вот Armtheking.🇹🇭✯◐』", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                    else:
                        RfuProtect["cancelprotect"] = True
                        if settings["lang"] == "JP":
                            line.sendMessage(msg.to,"เปิดป้องกันยกเลิกเชิญ   \n\n『◐✯ѕειт вот Armtheking.🇹🇭✯◐』", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                        else:
                            line.sendMessage(msg.to,"เปิดป้องกันยกเลิกเชิญ   \n\n『◐✯ѕειт вот Armtheking.🇹🇭✯◐』", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})

                elif msg.text.lower() == 'ปิดกันยก':
                    if RfuProtect["cancelprotect"] == False:
                        if settings["lang"] == "JP":
                            line.sendMessage(msg.to,"ปิดป้องกันยกเลิกเชิญ   \n\n『◐✯ѕειт вот Armtheking.🇹🇭✯◐』", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                        else:
                            line.sendMessage(msg.to,"ปิดป้องกันยกเลิกเชิญ   \n\n『◐✯ѕειт вот Armtheking.🇹🇭✯◐』", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                    else:
                        RfuProtect["cancelprotect"] = False
                        if settings["lang"] == "JP":
                            line.sendMessage(msg.to,"ปิดป้องกันยกเลิกเชิญ   \n\n『◐✯ѕειт вот Armtheking.🇹🇭✯◐』", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                        else:
                            line.sendMessage(msg.to,"ปิดป้องกันยกเลิกเชิญ   \n\n『◐✯ѕειт вот Armtheking.🇹🇭✯◐』", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})

                elif msg.text.lower() == 'กันเชิญ':
                    if RfuProtect["inviteprotect"] == True:
                        if settings["lang"] == "JP":
                            line.sendMessage(msg.to,"เปิดป้องกันยกเชิญ   \n\n『◐✯ѕειт вот Armtheking.🇹🇭✯◐』", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                        else:
                            line.sendMessage(msg.to,"เปิดป้องกันยกเชิญ   \n\n『◐✯ѕειт вот Armtheking.🇹🇭✯◐』", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                    else:
                        RfuProtect["inviteprotect"] = True
                        if settings["lang"] == "JP":
                            line.sendMessage(msg.to,"เปิดป้องกันยกเชิญ   \n\n『◐✯ѕειт вот Armtheking.🇹🇭✯◐』", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                        else:
                            line.sendMessage(msg.to,"เปิดป้องกันยกเชิญ   \n\n『◐✯ѕειт вот Armtheking.🇹🇭✯◐』", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})

                elif msg.text.lower() == 'ปิดกันเชิญ':
                    if RfuProtect["inviteprotect"] == False:
                        if settings["lang"] == "JP":
                            line.sendMessage(msg.to,"ปิดป้องกันยกเชิญ   \n\n『◐✯ѕειт вот Armtheking.🇹🇭✯◐』", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                        else:
                            line.sendMessage(msg.to,"ปิดป้องกันยกเชิญ   \n\n『◐✯ѕειт вот Armtheking.🇹🇭✯◐』", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                    else:
                        RfuProtect["inviteprotect"] = False
                        if settings["lang"] == "JP":
                            line.sendMessage(msg.to,"ปิดป้องกันยกเชิญ   \n\n『◐✯ѕειт вот Armtheking.🇹🇭✯◐』", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                        else:
                            line.sendMessage(msg.to,"ปิดป้องกันยกเชิญ   \n\n『◐✯ѕειт вот Armtheking.🇹🇭✯◐』", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})

                elif msg.text.lower() == 'กันลิ้ง':
                    if RfuProtect["linkprotect"] == True:
                        if settings["lang"] == "JP":
                            line.sendMessage(msg.to,"เปิดป้องกันลิ้ง   \n\n『◐✯ѕειт вот Armtheking.🇹🇭✯◐』", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                        else:
                            line.sendMessage(msg.to,"เปิดป้องกันลิ้ง   \n\n『◐✯ѕειт вот Armtheking.🇹🇭✯◐』", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                    else:
                        RfuProtect["linkprotect"] = True
                        if settings["lang"] == "JP":
                            line.sendMessage(msg.to,"เปิดป้องกันลิ้ง   \n\n『◐✯ѕειт вот Armtheking.🇹🇭✯◐』", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                        else:
                            line.sendMessage(msg.to,"เปิดป้องกันลิ้ง   \n\n『◐✯ѕειт вот Armtheking.🇹🇭✯◐』", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})

                elif msg.text.lower() == 'ปิดกันลิ้ง':
                    if RfuProtect["linkprotect"] == False:
                        if settings["lang"] == "JP":
                            line.sendMessage(msg.to,"ปิดป้องกันลิ้ง   \n\n『◐✯ѕειт вот Armtheking.🇹🇭✯◐』", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                        else:
                            line.sendMessage(msg.to,"ปิดป้องกันลิ้ง   \n\n『◐✯ѕειт вот Armtheking.🇹🇭✯◐』", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                    else:
                        RfuProtect["linkprotect"] = False
                        if settings["lang"] == "JP":
                            line.sendMessage(msg.to,"ปิดป้องกันลิ้ง   \n\n『◐✯ѕειт вот Armtheking.🇹🇭✯◐』", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                        else:
                            line.sendMessage(msg.to,"ปิดป้องกันลิ้ง   \n\n『◐✯ѕειт вот Armtheking.🇹🇭✯◐』", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})

                elif msg.text.lower() == 'กันกลุ่ม':
                    if RfuProtect["Protectguest"] == True:
                        if settings["lang"] == "JP":
                            line.sendMessage(msg.to,"เปิดป้องกันสมาชิก   \n\n『◐✯ѕειт вот Armtheking.🇹🇭✯◐』", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                        else:
                            line.sendMessage(msg.to,"เปิดป้องกันสมาชิก   \n\n『◐✯ѕειт вот Armtheking.🇹🇭✯◐』", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                    else:
                        RfuProtect["Protectguest"] = True
                        if settings["lang"] == "JP":
                            line.sendMessage(msg.to,"เปิดป้องกันสมาชิก   \n\n『◐✯ѕειт вот Armtheking.🇹🇭✯◐』", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                        else:
                            line.sendMessage(msg.to,"เปิดป้องกันสมาชิก   \n\n『◐✯ѕειт вот Armtheking.🇹🇭✯◐』", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})

                elif msg.text.lower() == 'ปิดกันกลุ่ม':
                    if RfuProtect["Protectguest"] == False:
                        if settings["lang"] == "JP":
                            line.sendMessage(msg.to,"ปิดป้องกันสมาชิก   \n\n『◐✯ѕειт вот Armtheking.🇹🇭✯◐』", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                        else:
                            line.sendMessage(msg.to,"ปิดป้องกันสมาชิก   \n\n『◐✯ѕειт вот Armtheking.🇹🇭✯◐』", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                    else:
                        RfuProtect["Protectguest"] = False
                        if settings["lang"] == "JP":
                            line.sendMessage(msg.to,"ปิดป้องกันสมาชิก   \n◐✯Armtheking.🇹🇭✯◐", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                        else:
                            line.sendMessage(msg.to,"ปิดป้องกันสมาชิก   \n◐✯Armtheking.🇹🇭✯◐", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})

                elif msg.text.lower() == 'กันเข้า':
                    if RfuProtect["Protectjoin"] == True:
                        if settings["lang"] == "JP":
                            line.sendMessage(msg.to,"เปิดป้องกันคนเข้า   \n\n『◐✯ѕειт вот Armtheking.🇹🇭✯◐』", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                        else:
                            line.sendMessage(msg.to,"เปิดป้องกันคนเข้า   \n\n『◐✯ѕειт вот Armtheking.🇹🇭✯◐』", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                    else:
                        RfuProtect["Protectjoin"] = True
                        if settings["lang"] == "JP":
                            line.sendMessage(msg.to,"เปิดป้องกันคนเข้า   \n\n『◐✯ѕειт вот Armtheking.🇹🇭✯◐』", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                        else:
                            line.sendMessage(msg.to,"เปิดป้องกันคนเข้า   \n\n『◐✯ѕειт вот Armtheking.🇹🇭✯◐』", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})

                elif msg.text.lower() == 'ปิดกันเข้า':
                    if RfuProtect["Protectjoin"] == False:
                        if settings["lang"] == "JP":
                            line.sendMessage(msg.to,"ปิดป้องกันคนเข้า   \n\n『◐✯ѕειт вот Armtheking.🇹🇭✯◐』", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                        else:
                            line.sendMessage(msg.to,"ปิดป้องกันคนเข้า   \n\n『◐✯ѕειт вот Armtheking.🇹🇭✯◐』", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                    else:
                        RfuProtect["Protectjoin"] = False
                        if settings["lang"] == "JP":
                            line.sendMessage(msg.to,"ปิดป้องกันคนเข้า   \n\n『◐✯ѕειт вот Armtheking.🇹🇭✯◐』", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                        else:
                            line.sendMessage(msg.to,"ปิดป้องกันคนเข้า   \n\n『◐✯ѕειт вот Armtheking.🇹🇭✯◐』", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})

                elif msg.text.lower() == 'เปิดหมด':
                    if RfuProtect["inviteprotect"] == True:
                        if settings["lang"] == "JP":
                            line.sendMessage(msg.to,"✰เปิดป้องกันทั้งหมด✰\n\n『◐✯ѕειт вот Armtheking.🇹🇭✯◐』", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                        else:
                            line.sendMessage(msg.to,"✰เปิดป้องกันทั้งหมด✰\n\n『◐✯ѕειт вот Armtheking.🇹🇭✯◐』", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                    else:
                        RfuProtect["inviteprotect"] = True
                        if settings["lang"] == "JP":
                            line.sendMessage(msg.to,"เปิดป้องกันเชิญ\n\n『◐✯ѕειт вот Armtheking.🇹🇭✯◐』", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                    if RfuProtect["cancelprotect"] == True:
                        if settings["lang"] == "JP":
                            line.sendMessage(msg.to,"เปิดป้องกันยกเลิกเชิญ\n\n『◐✯ѕειт вот Armtheking.🇹🇭✯◐』", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                        else:
                            line.sendMessage(msg.to,"เปิดป้องกันยกเลิกเชิญ\n\n『◐✯ѕειт вот Armtheking.🇹🇭✯◐』", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                    else:
                        RfuProtect["cancelprotect"] = True
                        if settings["lang"] == "JP":
                            line.sendMessage(msg.to,"เปิดป้องกันยกเลิกเชิญ\n\n『◐✯ѕειт вот Armtheking.🇹🇭✯◐』", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                    if RfuProtect["protect"] == True:
                        if settings["lang"] == "JP":
                            line.sendMessage(msg.to,"เปิดป้องกันยกเลิกเชิญ\n\n『◐✯ѕειт вот Armtheking.🇹🇭✯◐』", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                        else:
                            line.sendMessage(msg.to,"เปิดป้องกันยกเลิกเชิญ\n\n『◐✯ѕειт вот Armtheking.🇹🇭✯◐』", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                    else:
                        RfuProtect["protect"] = True
                        if settings["lang"] == "JP":
                            line.sendMessage(msg.to,"เปิดป้องกันเตะ\n\n『◐✯ѕειт вот Armtheking.🇹🇭✯◐』", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                        else:
                            line.sendMessage(msg.to,"เปิดป้องกันเตะ\n\n『◐✯ѕειт вот Armtheking.🇹🇭✯◐』", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                    if RfuProtect["linkprotect"] == True:
                        if settings["lang"] == "JP":
                            line.sendMessage(msg.to,"เปิดป้องกันลิ้ง\n\n『◐✯ѕειт вот Armtheking.🇹🇭✯◐』", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                        else:
                            line.sendMessage(msg.to,"เปิดป้องกันลิ้ง\n\n『◐✯ѕειт вот Armtheking.🇹🇭✯◐』", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                    else:
                        RfuProtect["linkprotect"] = True
                        if settings["lang"] == "JP":
                            line.sendMessage(msg.to,"เปิดป้องกันลิ้ง\n\n『◐✯ѕειт вот Armtheking.🇹🇭✯◐』", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                        else:
                            line.sendMessage(msg.to,"เปิดป้องกันลิ้ง\n\n『◐✯ѕειт вот Armtheking.🇹🇭✯◐』", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                    if RfuProtect["Protectguest"] == True:
                        if settings["lang"] == "JP":
                            line.sendMessage(msg.to,"เปิดป้องกันกลุ่ม\n\n『◐✯ѕειт вот Armtheking.🇹🇭✯◐』", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                        else:
                            line.sendMessage(msg.to,"เปิดป้องกันกลุ่ม\n\n『◐✯ѕειт вот Armtheking.🇹🇭✯◐』", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                    else:
                        RfuProtect["Protectguest"] = True
                        if settings["lang"] == "JP":
                            line.sendMessage(msg.to,"เปิดป้องกันกลุ่ม\n\n『◐✯ѕειт вот Armtheking.🇹🇭✯◐』", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                        else:
                            line.sendMessage(msg.to,"เปิดป้องกันกลุ่ม\n\n『◐✯ѕειт вот Armtheking.🇹🇭✯◐』", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                    if RfuProtect["Protectjoin"] == True:
                        if settings["lang"] == "JP":
                            line.sendMessage(msg.to,"เปิดป้องกันบุคคลภายน้อกเข้ากลุ่ม\n\n『◐✯ѕειт вот Armtheking.🇹🇭✯◐』", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                        else:
                            line.sendMessage(msg.to,"เปิดป้องกันบุคคลภายน้อกเข้ากลุ่ม\n\n『◐✯ѕειт вот Armtheking.🇹🇭✯◐』", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                    else:
                        RfuProtect["Protectjoin"] = True
                        if settings["lang"] == "JP":
                            line.sendMessage(msg.to,"เปิดป้องกันบุคคลภายน้อกเข้ากลุ่ม\n\n『◐✯ѕειт вот Armtheking.🇹🇭✯◐』", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                        else:
                            line.sendMessage(msg.to,"เปิดป้องกันบุคคลภายน้อกเข้ากลุ่ม\n\n『◐✯ѕειт вот Armtheking.🇹🇭✯◐』", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})

                elif msg.text.lower() == 'ปิดหมด':
                    if RfuProtect["inviteprotect"] == False:
                        if settings["lang"] == "JP":
                            line.sendMessage(msg.to,"✰ปิดป้องกันทั้งหมด✰\n\n『◐✯ѕειт вот Armtheking.🇹🇭✯◐』", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                        else:
                            line.sendMessage(msg.to,"✰ปิดป้องกันทั้งหมด✰\n\n『◐✯ѕειт вот Armtheking.🇹🇭✯◐』", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                    else:
                        RfuProtect["inviteprotect"] = False
                        if settings["lang"] == "JP":
                            line.sendMessage(msg.to,"ปิดป้องกันเชิญ\n\n『◐✯ѕειт вот Armtheking.🇹🇭✯◐』", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                    if RfuProtect["cancelprotect"] == False:
                        if settings["lang"] == "JP":
                            line.sendMessage(msg.to,"ปิดป้องกันยกเชิญ\n\n『◐✯ѕειт вот Armtheking.🇹🇭✯◐』", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                        else:
                            line.sendMessage(msg.to,"ปิดป้องกันยกเชิญ\n\n『◐✯ѕειт вот Armtheking.🇹🇭✯◐』", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                    else:
                        RfuProtect["cancelprotect"] = False
                        if settings["lang"] == "JP":
                            line.sendMessage(msg.to,"ปิดป้องกันยกเชิญ\n\n『◐✯ѕειт вот Armtheking.🇹🇭✯◐』", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                    if RfuProtect["protect"] == False:
                        if settings["lang"] == "JP":
                            line.sendMessage(msg.to,"ปิดป้องกันเตะ\n\n『◐✯ѕειт вот Armtheking.🇹🇭✯◐』", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                        else:
                            line.sendMessage(msg.to,"ปิดป้องกันเตะ\n\n『◐✯ѕειт вот Armtheking.🇹🇭✯◐』", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                    else:
                        RfuProtect["protect"] = False
                        if settings["lang"] == "JP":
                            line.sendMessage(msg.to,"ปิดป้องกันเตะ\n\n『◐✯ѕειт вот Armtheking.🇹🇭✯◐』", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                        else:
                            line.sendMessage(msg.to,"ปิดป้องกันเตะ\n\n『◐✯ѕειт вот Armtheking.🇹🇭✯◐』", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                    if RfuProtect["linkprotect"] == False:
                        if settings["lang"] == "JP":
                            line.sendMessage(msg.to,"ปิดป้องกันเปิดลิ้ง\n\n『◐✯ѕειт вот Armtheking.🇹🇭✯◐』", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                        else:
                            line.sendMessage(msg.to,"ปิดป้องกันเปิดลิ้ง\n\n『◐✯ѕειт вот Armtheking.🇹🇭✯◐』", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                    else:
                        RfuProtect["linkprotect"] = False
                        if settings["lang"] == "JP":
                            line.sendMessage(msg.to,"ปิดป้องกันเปิดลิ้ง\n\n『◐✯ѕειт вот Armtheking.🇹🇭✯◐』", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                        else:
                            line.sendMessage(msg.to,"ปิดป้องกันเปิดลิ้ง\n\n『◐✯ѕειт вот Armtheking.🇹🇭✯◐』", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                    if RfuProtect["Protectguest"] == False:
                        if settings["lang"] == "JP":
                            line.sendMessage(msg.to,"ปิดป้องกันกลุ่ม\n\n『◐✯ѕειт вот Armtheking.🇹🇭✯◐』", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                        else:
                            line.sendMessage(msg.to,"ปิดป้องกันกลุ่ม\n\n『◐✯ѕειт вот Armtheking.🇹🇭✯◐』", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                    else:
                        RfuProtect["Protectguest"] = False
                        if settings["lang"] == "JP":
                            line.sendMessage(msg.to,"ปิดป้องกันกลุ่ม\n\n『◐✯ѕειт вот Armtheking.🇹🇭✯◐』", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                        else:
                            line.sendMessage(msg.to,"ปิดป้องกันกลุ่ม\n\n『◐✯ѕειт вот Armtheking.🇹🇭✯◐』", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                    if RfuProtect["Protectjoin"] == False:
                        if settings["lang"] == "JP":
                            line.sendMessage(msg.to,"ปิดป้องกันบุคคลภายน้อกเข้ากลุ่ม\n\n『◐✯ѕειт вот Armtheking.🇹🇭✯◐』", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                        else:
                            line.sendMessage(msg.to,"ปิดป้องกันบุคคลภายน้อกเข้ากลุ่ม\n\n『◐✯ѕειт вот Armtheking.🇹🇭✯◐』", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                    else:
                        RfuProtect["Protectjoin"] = False
                        if settings["lang"] == "JP":
                            line.sendMessage(msg.to,"ปิดป้องกันบุคคลภายน้อกเข้ากลุ่ม\n\n『◐✯ѕειт вот Armtheking.🇹🇭✯◐』", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                        else:
                            line.sendMessage(msg.to,"ปิดป้องกันบุคคลภายน้อกเข้ากลุ่ม\n\n『◐✯ѕειт вот Armtheking.🇹🇭✯◐』", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})

#==============FINNISHING PROTECT========================#
                elif msg.text.lower() == 'เปิดรับแขก':
                        if settings["Wc"] == True:
                            if settings["lang"] == "JP":
                                line.sendMessage(to,"เปิดข้อความต้อนรับเมื่อมีสมาชิกเข้ากลุ่ม   \n\n『◐✯ѕειт вот Armtheking.🇹🇭✯◐』", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                        else:
                            settings["Wc"] = True
                            if settings["lang"] == "JP":
                                line.sendMessage(to,"เปิดข้อความต้อนรับเมื่อมีสมาชิกเข้ากลุ่ม   \n\n『◐✯ѕειт вот Armtheking.🇹🇭✯◐』", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                elif msg.text.lower() == 'ปิดรับแขก':
                        if settings["Wc"] == False:
                            if settings["lang"] == "JP":
                                line.sendMessage(to,"ปิดข้อความต้อนรับเมื่อมีสมาชิกเข้ากลุ่ม   \n\n『◐✯ѕειт вот Armtheking.🇹🇭✯◐』", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                        else:
                            settings["Wc"] = False
                            if settings["lang"] == "JP":
                                line.sendMessage(to,"ปิดข้อความต้อนรับเมื่อมีสมาชิกเข้ากลุ่ม  \n\n『◐✯ѕειт вот Armtheking.🇹🇭✯◐』 ", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                                
                elif msg.text.lower() == 'เปิดทักเตะ':
                        if settings["Nk"] == True:
                            if settings["lang"] == "JP":
                                line.sendMessage(to,"เปิดข้อความแจ้งเตือนเมื่อมีคนลบสมาชิกในกลุ่ม...\n\n『◐✯ѕειт вот Armtheking.🇹🇭✯◐』", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                        else:
                            settings["Nk"] = True
                            if settings["lang"] == "JP":
                                line.sendMessage(to,"เปิดข้อความแจ้งเตือนเมื่อมีคนลบสมาชิกในกลุ่ม...\n\n『◐✯ѕειт вот Armtheking.🇹🇭✯◐』", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                                
                elif msg.text.lower() == 'ปิดทักเตะ':
                        if settings["Nk"] == False:
                            if settings["lang"] == "JP":
                                line.sendMessage(to,"ปิดข้อความแจ้งเตือนเมื่อมีคนลบสมาชิกในกลุ่มแล้ว..\n\n『◐✯ѕειт вот Armtheking.🇹🇭✯◐』", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                        else:
                            settings["Nk"] = False
                            if settings["lang"] == "JP":
                                line.sendMessage(to,"เปิดข้อความแจ้งเตือนเมื่อมีคนลบสมาชิกในกลุ่มแล้ว...\n\n『◐✯ѕειт вот Armtheking.🇹🇭✯◐』", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})

                elif msg.text.lower() == 'เปิดส่งแขก':
                        if settings["Lv"] == True:
                            if settings["lang"] == "JP":
                                line.sendMessage(to,"เปิดข้อความอำลาเมื่อมีสมาชิกออกกลุ่ม   \n\n『◐✯ѕειт вот Armtheking.🇹🇭✯◐』", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                        else:
                            settings["Lv"] = True
                            if settings["lang"] == "JP":
                                line.sendMessage(to,"เปิดข้อความอำลาเมื่อมีสมาชิกออกกลุ่ม   \n\n『◐✯ѕειт вот Armtheking.🇹🇭✯◐』", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                elif msg.text.lower() == 'ปิดส่งแขก':
                        if settings["Lv"] == False:
                            if settings["lang"] == "JP":
                                line.sendMessage(to,"ปิดข้อความอำลาเมื่อมีสมาชิกออกกลุ่ม   \n\n『◐✯ѕειт вот Armtheking.🇹🇭✯◐』", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                        else:
                            settings["Lv"] = False
                            if settings["lang"] == "JP":
                                line.sendMessage(to,"ปิดข้อความอำลาเมื่อมีสมาชิกออกกลุ่ม   \n\n『◐✯ѕειт вот Armtheking.🇹🇭✯◐』", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                                
                elif msg.text.lower() == 'เปิดคท':
                        if settings["checkContact"] == True:
                            if settings["lang"] == "JP":
                                line.sendMessage(to,"เปิดระบบอ่านข้อมูลด้วยคอนแทคไว้อยู่แล้ว \n\n『◐✯ѕειт вот Armtheking.🇹🇭✯◐』", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                        else:
                            settings["checkContact"] = True
                            if settings["lang"] == "JP":
                                line.sendMessage(to,"เปิดระบบอ่านข้อมูลด้วยคอนแทค\n\n『◐✯ѕειт вот Armtheking.🇹🇭✯◐』", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                elif msg.text.lower() == 'ปิดคท':
                        if settings["checkContact"] == False:
                            if settings["lang"] == "JP":
                                line.sendMessage(to,"ปิดระบบอ่านข้อมูลด้วยคอนแทคไว้อยู่แล้ว \n\n『◐✯ѕειт вот Armtheking.🇹🇭✯◐』", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                        else:
                            settings["checkContact"] = False
                            if settings["lang"] == "JP":
                                line.sendMessage(to,"ปิดระบบอ่านข้อมูลด้วยคอนแทค\n\n『◐✯ѕειт вот Armtheking.🇹🇭✯◐』", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                elif msg.text.lower() == 'เปิดเช็คโพส':
                        if settings["checkPost"] == True:
                            if settings["lang"] == "JP":
                                line.sendMessage(to,"เปิดระบบเช็คโพสบนทามไลน์ไว้อยู่แล้ว \n\n『◐✯ѕειт вот Armtheking.🇹🇭✯◐』", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                        else:
                            settings["checkPost"] = True
                            if settings["lang"] == "JP":
                                line.sendMessage(to,"เปิดระบบเช็คโพสบนทามไลน์ \n\n『◐✯ѕειт вот Armtheking.🇹🇭✯◐』", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                elif msg.text.lower() == 'ปิดเช็คโพส':
                        if settings["checkPost"] == False:
                            if settings["lang"] == "JP":
                                line.sendMessage(to,"ปิดระบบเช็คโพสบนทามไลน์ไว้อยู่แล้ว \n\n『◐✯ѕειт вот Armtheking.🇹🇭✯◐』", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                        else:
                            settings["checkPost"] = False
                            if settings["lang"] == "JP":
                                line.sendMessage(to,"ปิดระบบเช็คโพสบนทามไลน์\n\n『◐✯ѕειт вот Armtheking.🇹🇭✯◐』", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                elif text.lower() == "แปลงโฉม":
                    settings["changePictureProfile"] = True
                    line.sendMessage(to, "ส่งรูปภาพลงมาได้เลยครับผม\n\n『◐✯ѕειт вот Armtheking.🇹🇭✯◐』", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                elif text.lower() == "อัพวีดีโอ" and sender == lineMID:
                    settings['changeProfileVideo']['status'] = True
                    settings['changeProfileVideo']['stage'] = 1
                    line.sendMessage(to, "「 ส่งวีดีโอลงมาเลยลูกพี่ \n\n『◐✯ѕειт вот Armtheking.🇹🇭✯◐』」\n•", "\nSend video !", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                elif text.lower() == "เปลี่ยนรูปกลุ่ม":
                    if msg.toType == 2:
                        if to not in settings["changeGroupPicture"]:
                            settings["changeGroupPicture"].append(to)
                        line.sendMessage(to, "ส่งรูปภาพลงมาไดเเลยครับผม", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                elif text.lower() == ".ไวรัส":
                        line.sendMessage(to, ".God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God .3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God .3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God.3.God")
                        line.sendMessage(to, "เข้านอนได้แล้วเด็กๆ")
                elif text.lower() == 'ของขวัญ':
                        line.sendGift(msg.to,'1002077','sticker')
                        line.sendGift(msg.to,'1002077','sticker')
                        line.sendGift(msg.to,'1002077','sticker')
                elif text.lower() == 'ลบรัน':
                    gid = line.getGroupIdsInvited()
                    start = time.time()
                    for i in gid:
                        line.rejectGroupInvitation(i)
                    elapsed_time = time.time() - start
                    line.sendMessage(to, "ลบรันเสร็จแล้วขอรับ", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                    line.sendMessage(to, "ระยะเวลาที่ใช้: %sวินาที" % (elapsed_time), contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
			
                elif "ลงดำ" in msg.text:
                  if msg._from in Family:
                      if msg.toType == 2:
                           print ("All Banlist")
                           _name = msg.text.replace("ลงดำ","")
                           gs = line.getGroup(msg.to)
                           line.sendMessage(msg.to,"แบนสมาชิกทุกคนในห้องนี้แล้ว＼（○＾ω＾○）／", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                           targets = []
                           for g in gs.members:
                               if _name in g.displayName:
                                    targets.append(g.mid)
                           if targets == []:
                                line.sendMessage(msg.to,"Maaf", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                           else:
                               for target in targets:
                                   if not target in Family:
                                       try:
                                           settings["blacklist"][target] = True
                                           f=codecs.open('st2__b.json','w','utf-8')
                                           json.dump(settings["blacklist"], f, sort_keys=True, indent=4,ensure_ascii=False)
                                       except:
                                           line.sentMessage(msg.to,"พบข้อผิดพลาดที่ไม่ทราบสาเหตุ", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
										   
                elif 'แบน' in text.lower():
                       targets = []
                       key = eval(msg.contentMetadata["MENTION"])
                       key["MENTIONEES"] [0] ["M"]
                       for x in key["MENTIONEES"]:
                           targets.append(x["M"])
                       for target in targets:
                           try:
                               settings["blacklist"][target] = True
                               f=codecs.open('st2__b.json','w','utf-8')
                               json.dump(settings["blacklist"], f, sort_keys=True, indent=4,ensure_ascii=False)
                               line.sendMessage(msg.to,"Succes added for the blacklist ", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                               print ("Banned User")
                           except:
                               line.sendMessage(msg.to,"Contact Not Found", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})

                elif 'ล้างแบน' in text.lower():
                       targets = []
                       key = eval(msg.contentMetadata["MENTION"])
                       key["MENTIONEES"] [0] ["M"]
                       for x in key["MENTIONEES"]:
                           targets.append(x["M"])
                       for target in targets:
                           try:
                               del settings["blacklist"][target]
                               f=codecs.open('st2__b.json','w','utf-8')
                               json.dump(settings["blacklist"], f, sort_keys=True, indent=4,ensure_ascii=False)
                               line.sendMessage(msg.to,"Succes unban from the blacklist. ", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                               print ("Unbanned User")
                           except:
                               line.sendMessage(msg.to,"Contact Not Found", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                
                elif msg.text in ["เช็คดำ"]:
                  if msg._from in Family:
                    if settings["blacklist"] == {}:
                        line.sendMessage(msg.to,"ไม่พบ", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'}) 
                    else:
                        line.sendMessage(msg.to,"รายชื่อผู้ติดดำ", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                        mc = "Blacklist User\n"
                        for mi_d in settings["blacklist"]:
                            mc += "[√] " + line.getContact(mi_d).displayName + " \n"
                        line.sendMessage(msg.to, mc + "")

                elif msg.text.lower().startswith("urban "):
                    sep = msg.text.split(" ")
                    judul = msg.text.replace(sep[0] + " ","")
                    url = "http://api.urbandictionary.com/v0/define?term="+str(judul)
                    with requests.session() as s:
                        s.headers["User-Agent"] = random.choice(settings["userAgent"])
                        r = s.get(url)
                        data = r.text
                        data = json.loads(data)
                        y = "[ Result Urban ]"
                        y += "\nTags: "+ data["tags"][0]
                        y += ","+ data["tags"][1]
                        y += ","+ data["tags"][2]
                        y += ","+ data["tags"][3]
                        y += ","+ data["tags"][4]
                        y += ","+ data["tags"][5]
                        y += ","+ data["tags"][6]
                        y += ","+ data["tags"][7]
                        y += "\n[1]\nAuthor: "+str(data["list"][0]["author"])
                        y += "\nWord: "+str(data["list"][0]["word"])
                        y += "\nLink: "+str(data["list"][0]["permalink"])
                        y += "\nDefinition: "+str(data["list"][0]["definition"])
                        y += "\nExample: "+str(data["list"][0]["example"])
                        line.sendMessage(to, str(y), contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})

            elif msg.contentType == 13:
                if settings["checkContact"] == True:
                    try:
                        contact = line.getContact(msg.contentMetadata["mid"])
                        if line != None:
                            cover = line.getProfileCoverURL(msg.contentMetadata["mid"])
                        else:
                            cover = "Tidak dapat masuk di line channel"
                        path = "http://dl.profile.line-cdn.net/{}".format(str(contact.pictureStatus))
                        try:
                            line.sendImageWithURL(to, str(path))
                        except:
                            pass
                        ret_ = "[ รายการทั้งหมดจากการสำรวจด้วย คท ]"
                        ret_ += "\n ชื่อ : {}".format(str(contact.displayName))
                        ret_ += "\n ไอดี : {}".format(str(msg.contentMetadata["mid"]))
                        ret_ += "\n ตัส : {}".format(str(contact.statusMessage))
                        ret_ += "\n รูปโปรไฟล : http://dl.profile.line-cdn.net/{}".format(str(contact.pictureStatus))
                        ret_ += "\n  รูปปก : {}".format(str(cover))
                        ret_ += "\n[ สิ้นสุดการสำรวจ ]"
                        line.sendMessage(to, str(ret_), contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                    except:
                        line.sendMessage(to, "เกิดข้อผิดพลาดในการสำรวจ")
            elif msg.contentType == 1:
                if settings["changePictureProfile"] == True:
                    path = line.downloadObjectMsg(msg_id)
                    settings["changePictureProfile"] = False
                    line.updateProfilePicture(path)
                    line.sendMessage(to, "ทำการแปลงโฉมเสร็จเรียบร้อย", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                if msg.toType == 2:
                    if to in settings["changeGroupPicture"]:
                        path = line.downloadObjectMsg(msg_id)
                        settings["changeGroupPicture"].remove(to)
                        line.updateGroupPicture(to, path)
                        line.sendMessage(to, "เปลี่ยนรูปภาพกลุ่มเรียบร้อยแล้ว", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
            elif msg.contentType == 1:
                if settings['changeProfileVideo']['status'] == True and sender == lineMID:
                    path = line.downloadObjectMsg(msg_id)
                    settings["changeProfileVideo"] = False
                    line.updateProfileVideo(to, path)
                    line.sendMessage(to, "ทำการอัพเดตวีดีโอโปรไฟลเสร็จเรียบร้อย", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                elif msg.contentType in [1,2]:
                    if sender in lineMID:
                        line.sendMessage(to, str(msg))
                if msg.contentType == 7:
                    if settings["messageSticker"]["addStatus"] == True:
                        name = settings["messageSticker"]["addName"]
                        if name != None and name in settings["messageSticker"]["listSticker"]:
                            settings["messageSticker"]["listSticker"][name] = {
                                "STKID": msg.contentMetadata["STKID"],
                                "STKVER": msg.contentMetadata["STKVER"],
                                "STKPKGID": msg.contentMetadata["STKPKGID"]
                            }
                            line.sendMessage(to, "Success Added " + name)
                        settings["messageSticker"]["addStatus"] = False
                        settings["messageSticker"]["addName"] = None
                    if settings["addSticker"]["status"] == True:
                        stickers[settings["addSticker"]["name"]]["STKVER"] = msg.contentMetadata["STKVER"]
                        stickers[settings["addSticker"]["name"]]["STKID"] = msg.contentMetadata["STKID"]
                        stickers[settings["addSticker"]["name"]]["STKPKGID"] = msg.contentMetadata["STKPKGID"]
                        f = codecs.open('sticker.json','w','utf-8')
                        json.dump(stickers, f, sort_keys=True, indent=4, ensure_ascii=False)
                        line.sendMessage(to, "Success Added sticker {}".format(str(settings["addSticker"]["name"])))
                        settings["addSticker"]["status"] = False
                        settings["addSticker"]["name"] = ""
                   
            elif msg.contentType == 7:
                if settings["checkSticker"] == True:
                    stk_id = msg.contentMetadata['STKID']
                    stk_ver = msg.contentMetadata['STKVER']
                    pkg_id = msg.contentMetadata['STKPKGID']
                    ret_ = "╔══[ Sticker Info ]"
                    ret_ += "\n╠ STICKER ID : {}".format(stk_id)
                    ret_ += "\n╠ STICKER PACKAGES ID : {}".format(pkg_id)
                    ret_ += "\n╠ STICKER VERSION : {}".format(stk_ver)
                    ret_ += "\n╠ STICKER URL : line://shop/detail/{}".format(pkg_id)
                    ret_ += "\n╚══[ Finish ]"
                    line.sendMessage(to, str(ret_))
              
#==============================================================================#
        if op.type == 19:
            if lineMID in op.param3:
                settings["blacklist"][op.param2] = True
        if op.type == 22:
            if settings['leaveRoom'] == True:
                line.leaveRoom(op.param1)              
        if op.type == 24:
            if settings['leaveRoom'] == True:
                line.leaveRoom(op.param1)             
#==============================================================================#
#==============================================================================#
        if op.type == 17:
            if op.param2 not in Family:
                if op.param2 in Family:
                    pass
            if RfuProtect["protect"] == True:
                if settings["blacklist"][op.param2] == True:
                    try:
                        line.kickoutFromGroup(op.param1,[op.param2])
                        G = line.getGroup(op.param1)
                        G.preventedJoinByTicket = True
                        line.updateGroup(G)
                    except:
                        try:
                            line.kickoutFromGroup(op.param1,[op.param2])
                            G = line.getGroup(op.param1)
                            G.preventedJoinByTicket = True
                            line.updateGroup(G)
                        except:
                            pass
        if op.type == 19:
            if op.param2 not in Family:
                if op.param2 in Family:
                    pass
                elif RfuProtect["protect"] == True:
                    settings ["blacklist"][op.param2] = True
                    random.choice(Rfu).kickoutFromGroup(op.param1,[op.param2])
                    random.choice(Rfu).inviteIntoGroup(op.param1,[op.param2])
        
        if op.type == 13:
            if op.param2 not in Family:
                if op.param2 in Family:
                    pass
                elif RfuProtect["inviteprotect"] == True:
                    settings ["blacklist"][op.param2] = True
                    random.choice(Rfu).cancelGroupInvitation(op.param1,[op.param3])
                    random.choice(Rfu).kickoutFromGroup(op.param1,[op.param2])
                    if op.param2 not in Family:
                        if op.param2 in Family:
                            pass
                        elif RfuProtect["inviteprotect"] == True:
                            settings ["blacklist"][op.param2] = True
                            random.choice(Rfu).cancelGroupInvitation(op.param1,[op.param3])
                            random.choice(Rfu).kickoutFromGroup(op.param1,[op.param2])
                            if op.param2 not in Family:
                                if op.param2 in Family:
                                    pass
                                elif RfuProtect["cancelprotect"] == True:
                                    settings ["blacklist"][op.param2] = True
                                    random.choice(Rfu).cancelGroupInvitation(op.param1,[op.param3])

        if op.type == 11:
            if op.param2 not in Family:
                if op.param2 in Family:
                    pass
                elif RfuProtect["linkprotect"] == True:
                    settings ["blacklist"][op.param2] = True
                    G = line.getGroup(op.param1)
                    G.preventedJoinByTicket = True
                    line.updateGroup(G)
                    random.choice(Rfu).kickoutFromGroup(op.param1,[op.param2])

        if op.type == 11:
            if RfuProtect["linkprotect"] == True:
                if op.param2 not in Family:
                    G = line.getGroup(op.param1)
                    G.preventedJoinByTicket = True
                    random.choice(Rfu).updateGroup(G)
                    random.choice(Rfu).kickoutFromGroup(op.param1,[op.param3])

        if op.type == 5:
            if RfuProtect["autoBlock"] == True:
                if (settings["message"] in [""," ","\n",None]):
                    pass
                else:
                    line.sendMessage(op.param1,str(settings["message"]))
        if op.type == 5:
            if RfuProtect["autoAdd"] == True:
                if (settings["comment1"] in [""," ","\n",None]):
                    pass
                else:
                    line.sendMessage(op.param1,str(settings["comment1"]))
        if op.type == 13:
           if RfuProtect["Protectguest"] == True:
               if op.param2 not in Family:
                  random.choice(Rfu).cancelGroupInvitation(op.param1,[op.param3])
                  random.choice(Rfu).kickoutFromGroup(op.param1,[op.param2])
        if op.type == 17:
            if op.param2 in settings["blacklist"] == {}:
                line.kickoutFromGroup(op.param1,[op.param2])
                now2 = datetime.datetime.now()
                nowT = datetime.datetime.strftime(now2,"%H")
                nowM = datetime.datetime.strftime(now2,"%M")
                nowS = datetime.datetime.strftime(now2,"%S")
                tm = "\n\n"+nowT+":"+nowM+":"+nowS
                line.sendText(op.param1,"สมาชิกที่ถูกแบนไม่ได้รับอนุญาตให้เข้าร่วมกลุ่ม （´・ω・｀）"+tm)
        if op.type == 17:
           if RfuProtect["Protectjoin"] == True:
               if op.param2 not in Family:
                   random.choice(Rfu).kickoutFromGroup(op.param1,[op.param2])

        if op.type == 1:
            if sender in Setmain["foto"]:
                path = line.downloadObjectMsg(msg_id)
                del Setmain["foto"][sender]
                line.updateProfilePicture(path)
                line.sendMessage(to,"Foto berhasil dirubah")
        if op.type == 25:
#            if settings ["mutebot2"] == True:
            msg = op.message
            text = msg.text
            msg_id = msg.id
            receiver = msg.to
            sender = msg._from
            if msg.toType == 0:
                if sender != line.profile.mid:
                    to = sender
                else:
                    to = receiver
            else:
                to = receiver
#========================================================================
                if msg.contentType == 7:
                    if settings["messageSticker"]["addStatus"] == True:
                        name = settings["messageSticker"]["addName"]
                        if name != None and name in settings["messageSticker"]["listSticker"]:
                            settings["messageSticker"]["listSticker"][name] = {
                                "STKID": msg.contentMetadata["STKID"],
                                "STKVER": msg.contentMetadata["STKVER"],
                                "STKPKGID": msg.contentMetadata["STKPKGID"]
                            }
                            line.sendMessage(to, "Success Added " + name)
                        settings["messageSticker"]["addStatus"] = False
                        settings["messageSticker"]["addName"] = None
                    if settings["addSticker"]["status"] == True:
                        stickers[settings["addSticker"]["name"]]["STKVER"] = msg.contentMetadata["STKVER"]
                        stickers[settings["addSticker"]["name"]]["STKID"] = msg.contentMetadata["STKID"]
                        stickers[settings["addSticker"]["name"]]["STKPKGID"] = msg.contentMetadata["STKPKGID"]
                        f = codecs.open('sticker.json','w','utf-8')
                        json.dump(stickers, f, sort_keys=True, indent=4, ensure_ascii=False)
                        line.sendMessage(to, "Success Added sticker {}".format(str(settings["addSticker"]["name"])))
                        settings["addSticker"]["status"] = False
                        settings["addSticker"]["name"] = ""
                            
        if op.type == 26:
            msg = op.message
            text = msg.text
            msg_id = msg.id
            receiver = msg.to
            sender = msg._from
            if msg.toType == 0 or msg.toType == 1 or msg.toType == 2:
                if msg.toType == 0:
                    if sender != line.profile.mid:
                        to = sender
                    else:
                        to = receiver
                elif msg.toType == 1:
                    to = receiver
                elif msg.toType == 2:
                    to = receiver
                if settings["autoRead"] == True:
                        line.sendChatChecked(to, msg_id)				
                if to in read["readPoint"]:
                    if sender not in read["ROM"][to]:
                        read["ROM"][to][sender] = True
                if sender in settings["mimic"]["target"] and settings["mimic"]["status"] == True and settings["mimic"]["target"][sender] == True:
                    text = msg.text
                    if text is not None:
                        line.sendMessage(msg.to,text)
                elif msg.contentType == 7:
                    if settings["checkSticker"] == True:
                        try:
                            stk_id = msg.contentMetadata['STKID']
                            stk_ver = msg.contentMetadata['STKVER']
                            pkg_id = msg.contentMetadata['STKPKGID']
                            ret_ = "「 Check Sticker 」\n"
                            ret_ += "\nSTKID : {}".format(stk_id)
                            ret_ += "\nSTKPKGID : {}".format(pkg_id)
                            ret_ += "\nSTKVER : {}".format(stk_ver)
                            ret_ += "\nLINK : line://shop/detail/{}".format(pkg_id)
                            print(msg)
                            line.sendImageWithURL(to, "http://dl.stickershop.line.naver.jp/products/0/0/"+msg.contentMetadata["STKVER"]+"/"+msg.contentMetadata["STKPKGID"]+"/WindowsPhone/stickers/"+msg.contentMetadata["STKID"]+".png")
                            line.sendMessage(to, str(ret_))                            
                        except Exception as error:
                            line.sendMessage(to, str(error))
                if msg.text:
                    if msg.text.lower().lstrip().rstrip() in wbanlist:
                        if msg.text not in lineMID:
                            try:
                                line.kickoutFromGroup(msg.to,[sender])
                                line.sendMessage("คุณพูดคำต้องห้าม จำเป็นต้องนำออก sorry(╯°□°）╯︵ ┻━┻", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                            except Exception as e:
                                print(e)
                    if "/ti/g/" in msg.text.lower():
                        if settings["autoJoinTicket"] == True:
                            link_re = re.compile('(?:line\:\/|line\.me\/R)\/ti\/g\/([a-zA-Z0-9_-]+)?')
                            links = link_re.findall(text)
                            n_links = []
                            for l in links:
                                if l not in n_links:
                                    n_links.append(l)
                            for ticket_id in n_links:
                                group = line.findGroupByTicket(ticket_id)
                                line.acceptGroupInvitationByTicket(group.id,ticket_id)
                                line.sendMessage(to, "🔰เข้าร่วมกลุ่ม🔰\n🔀👉 %s 👈 เรียบร้อยแล้ว\n🔷โดยผ่านการแชร์ด้วยลิ้งค์🔷" % str(group.name), contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                if msg.toType == 0 and settings["autoReply"] and sender != lineMID:
                    contact = line.getContact(sender)
                    rjct = ["auto", "ngetag"]
                    validating = [a for a in rjct if a.lower() in text.lower()]
                    if validating != []: return
                    if contact.attributes != 32:
                        msgSticker = settings["messageSticker"]["listSticker"]["sleepSticker"]
                        if msgSticker != None:
                            sid = msgSticker["STKID"]
                            spkg = msgSticker["STKPKGID"]
                            sver = msgSticker["STKVER"]
                            sendSticker(to, sver, spkg, sid)
                        if "@!" in settings["replyPesan"]:
                            msg_ = settings["replyPesan"].split("@!")
                            sendMention(to, sender, "Sleep Mode :\n" + msg_[0], msg_[1])
                        sendMention(to, sender, "Sleep Mode :\nว่าไงคับ", settings["replyPesan"])
                if 'MENTION' in msg.contentMetadata.keys()!= None:
                    if settings["detectMentionPM"] == True:
                        names = re.findall(r'@(\w+)', text)
                        mention = ast.literal_eval(msg.contentMetadata['MENTION'])
                        mentionees = mention['MENTIONEES']
                        for mention in mentionees:
                            if lineMID in mention["M"]:
                                sendMention(sender, sender, "「ตอบแทคอัตโนมัติ」\n", "\n" + str(settings["pmMessage"]))
                                break
                if msg.contentType == 0 and sender not in lineMID and msg.toType == 2:
                    if "MENTION" in msg.contentMetadata.keys() != None:
        	             if settings['kickMention'] == True:
        		             contact = line.getContact(msg._from)
        		             cName = contact.displayName
        		             balas = ["เนื่องจากตอนนี้ผมเปิดระบบเตะคนแทคไว้ " + "\n👉" + cName + "\n🙏ต้องขออภัยด้วยจริงๆ🙏Bye!!!"]
        		             ret_ = "" + random.choice(balas)                     
        		             name = re.findall(r'@(\w+)', msg.text)
        		             mention = ast.literal_eval(msg.contentMetadata["MENTION"])
        		             mentionees = mention["MENTIONEES"]
        		             for mention in mentionees:
        			               if mention['M'] in admin:
        				                  line.sendText(msg.to,ret_)
        				                  line.kickoutFromGroup(msg.to,[msg._from])
        				                  break                                  
        			               if mention['M'] in lineMID:
        				                  line.sendText(msg.to,ret_)
        				                  line.kickoutFromGroup(msg.to,[msg._from])
        				                  break
                if msg.contentType == 0 and sender not in lineMID and msg.toType == 2:
                    if "MENTION" in list(msg.contentMetadata.keys())!= None:
                         if settings['potoMention'] == True:
                             contact = line.getContact(msg._from)
                             cName = contact.pictureStatus
                             mi_d = contact.mid
                             balas = ["http://dl.profile.line-cdn.net/" + cName]
                             ret_ = random.choice(balas)
                             mention = ast.literal_eval(msg.contentMetadata["MENTION"])
                             mentionees = mention["MENTIONEES"]
                             for mention in mentionees:
                                   if mention["M"] in lineMID:
                                          line.sendImageWithURL(to,ret_)
                                          line.sendContact(msg.to, mi_d)
                                          break  
                if msg.contentType == 0 and sender not in lineMID and msg.toType == 2:
                    if "MENTION" in list(msg.contentMetadata.keys()) != None:
                         if settings['detectMention'] == True:
                             #icon = "http://dl.profile.line.naver.jp/"+lineProfile.pictureStatus
                             #name = "ข้อความคนแทค"                   
                             #link = "http://line.me/ti/p/~botline2034"
                             contact = line.getContact(msg._from)
                             cName = contact.displayName
                             balas = ["『 ตอบกลับคำแทคอัตโนมัติ』\n\n " + cName]
                             ret_ = "" + random.choice(balas)
                             name = re.findall(r'@(\w+)', msg.text)
                             mention = ast.literal_eval(msg.contentMetadata["MENTION"])
                             mentionees = mention['MENTIONEES']
                             for mention in mentionees:
                                   if mention['M'] in lineMID:
                                          line.sendMessage(to,ret_, contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                                          line.sendMessage(to,str(settings["Respontag"]), contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                                          msgSticker = settings["messageSticker"]["listSticker"]["responSticker"]
                                          if msgSticker != None:
                                              sid = msgSticker["STKID"]
                                              spkg = msgSticker["STKPKGID"]
                                              sver = msgSticker["STKVER"]
                                              sendSticker(to, sver, spkg, sid)
                if msg.contentType == 0 and sender not in lineMID and msg.toType == 2:
                    if "MENTION" in list(msg.contentMetadata.keys()) != None:
                         if settings['delayMention'] == True:
                             contact = line.getContact(msg._from)
                             cName = contact.displayName
                             name = re.findall(r'@(\w+)', msg.text)
                             mention = ast.literal_eval(msg.contentMetadata["MENTION"])
                             mentionees = mention['MENTIONEES']
                             for mention in mentionees:
                                   if mention['M'] in lineMID:
                                          sendMessageWithMention(to, contact.mid)
#                                          sendMessageWithMention(to, contact.mid)
#                                          sendMessageWithMention(to, contact.mid)
#                                          sendMessageWithMention(to, contact.mid)
#                                          sendMessageWithMention(to, contact.mid)
#                                          sendMessageWithMention(to, contact.mid)
#                                          sendMessageWithMention(to, contact.mid)
#                                          sendMessageWithMention(to, contact.mid)
#                                          sendMessageWithMention(to, contact.mid)
#                                          sendMessageWithMention(to, contact.mid)
                                          break

#===========ชุด API คำสั่งใช้งานบอทสิริเชนวี10 ========================== 
        if op.type == 26:
            msg = op.message
            if settings ["Aip"] == True:
            	if msg.text in ["cleanse","group cleansed.","mulai",".winebot",".kickall","mayhem","kick on","Kick","!kickall","nuke","บิน","Kick","กระเด็น","หวด","เซลกากจัง","เตะ",".","ปลิว"]:
                    line.kickoutFromGroup(receiver,[sender])
                    line.sendText(msg.to,"ตรวจพบคำสั่งของบอทลบกลุ่ม จำเป็นต้องนำออกเพื่อความปลอดภัยของสมาชิก (｀・ω・´)")
            if settings ["Aip"] == True:
                if msg.text in ["ควย","หี","แตด","เย็ดแม่","เย็ดเข้","ค.วย","สัส","เหี้ย","ไอ้เหี้ย","พ่อมึงตาย","ไอ้เลว","ระยำ","ชาติหมา","หน้าหี","เซลกาก","ไอ้เรส","ไอ้เหี้ยเรส","ไอ่เรส","พ่องตาย","ส้นตีน","แม่มึงอ่ะ","แม่มึงดิ","พ่อมึงดิ"]:
                    line.kickoutFromGroup(receiver,[sender])
                    line.sendText(msg.to,"ตรวจพบคำพูดหยาบคายไม่สุภาพ จำเป็นต้องนำออกเพื่อความสงบสุขของสมาชิก (｀・ω・´)")
            #if settings ["Api"] == True:
            #    if msg.text in ["ป๊า","ป๊าเรส","ลุง","เรส","นาย","เพื่อน","จาร์ย","อาจาร์ย","เฮีย"]:
            #        line.sendMessage(msg.to, str(settings["comment1"]))
#            if settings ["Api"] == True:
#                if msg.text in ["เซล","เซลบอท","selfbot","ขายบอท"]:
#                    line.sendMessage(msg.to, str(settings["comment"]))
#                    line.sendMessage(msg.to, None, contentMetadata={"STKID":"52114123","STKPKGID":"11539","STKVER":"1"}, contentType=7)
#            if settings ["Api"] == True:
#                if msg.text in ["55","555","5555","55555","55+","555+","5555+","ขำ",".ขำ"]:
#                    line.sendText(msg.to,"ฮ่าๆๆๆ..ขำไรจ๊ะ..\n😆มึงไปโดนตัวใหนมาเนี่ย😆")
#                    line.sendMessage(msg.to, None, contentMetadata={"STKID":"51626504","STKPKGID":"11538","STKVER":"1"}, contentType=7)
#            if settings ["Api"] == True:
#                if msg.text in ["ประกาศ","โฆษณา","ประชาสัมพัน","ประกาศ"]:
#                    line.sendMessage(msg.to, str(settings["comment1"]))
#                    line.sendMessage(msg.to, None, contentMetadata={"STKID":"52114123","STKPKGID":"11539","STKVER":"1"}, contentType=7)
#            if settings["Api"] == True:
#                if msg.text in ["กำ","กำหำ","กำหอย"]:
#                    line.sendText(msg.to,"กำเบาๆนะเค้าเจ็บ😁😁")
#                    line.sendMessage(msg.to, None, contentMetadata={"STKID":"51626498","STKPKGID":"11538","STKVER":"1"}, contentType=7)
#            if settings["Api"] == True:
#                if msg.text in ["งง","งงง",]:
#                    line.sendText(msg.to,"ไม่ต้องงงคับ ผมหล่อแบบนี้มาตั้งนานแล้ว😂😂")
#                    line.sendMessage(msg.to, None, contentMetadata={"STKID":"51626512","STKPKGID":"11538","STKVER":"1"}, contentType=7)
#            if settings["Api"] == True:
#                if msg.text in ["หรา","หราา",]:
#                    line.sendMessage(msg.to, None, contentMetadata={"STKID":"51626516","STKPKGID":"11538","STKVER":"1"}, contentType=7)
            if settings ["Api"] == True:
                if msg.text in ["อยู่ไหม","เช็คบอท","/เทส","ออนใหม","อย"]:
                    line.sendText(msg.to,"อยู่ตลอด 🕛")
#            if settings ["Api"] == True:
#                if msg.text in ["สวัดดี","หวัดดี","ดีจ้า","ดีครับ","ดี","สวัสดีครับ","สวัสดีค่ะ","ดีงับๆ","ดีงับ","หวัดดีงับๆ"]:
#                    line.sendText(msg.to,"สวัสดีครับ ผมชื่อตาต้อมนะ ยินดีที่ได้รู้จัก")
#            if settings ["Api"] == True:
#                if msg.text in ["/ตั้งเวลา",".ตั้งเวลา",".ตั้ง","/ตั้ง","/จับ"]:
#                    line.sendText(msg.to,"🔷กำลังรีเซ็ทระบบตั้งค่าคนอ่าน🔷")
#                    line.sendText(msg.to,"จับ")
#            if settings ["Api"] == True:
#                if msg.text in ["/อ่าน","คนอ่าน","/คนอ่าน","/ใครอ่าน","ใครอ่าน"]:
#                    line.sendText(msg.to,"🔷ตรวจสอบรายชือคนอ่าน🔷")
#                    line.sendText(msg.to,"อ่าน") 
        #if op.type in [25,26]:
        if op.type ==25:
            msg = op.message
            if settings ["Api"] == True:
                if msg.text in ["รองแอด","รอง","แอดรอง","แอดสำรอง","@2"]:
                    line.sendText(msg.to,"Siriv10:extracreator")
                    line.sendText(msg.to,"👆คนนี้คือแอดสำรองห้องนี้")#, contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})            
            if settings ["Api"] == True:
                if msg.text in ["เช็ค","เช็คตั้งค่า","ตั้งค่า"]:
                    line.sendText(msg.to,"Set:status")
                    line.sendText(msg.to,"เช็คการตั้งค่าบอทสิริ")                     
            if settings ["Api"] == True:
                if msg.text in ["ตั้งแอดรอง","ตั้งรอง","ตั้งแอดรอง"]:
                    line.sendText(msg.to,"設定:予備作者変更")
                    line.sendText(msg.to,"ลงคำสั่งแล้ว ส่ง คท. แอดรองลงครับ") 
            if settings ["Api"] == True:
                if msg.text in ["แอด","@","@1"]:
                    line.sendText(msg.to,"Siri:groupcreator")
                    line.sendText(msg.to,"👆คนนี้คือแอดมินกลุ่มนี้ ")
            if settings ["Api"] == True:
                if msg.text in ["สลับ","สลับแอด"]:
                    line.sendText(msg.to,"設定:作者交換")
                    line.sendText(msg.to,"คำสั่งนี้ใช้ได้เฉพาะแอดมินหลักกับรอง\nลงคำสั่ง 1 ครับพอนะครับ")     
            if settings ["Api"] == True:
                if msg.text in ["ปลดแอด","ปลดแอดมิน","ล้างแอด"]:
                    line.sendText(msg.to,"siri:forcerelease")
                    line.sendText(msg.to,"คำสั่งนี้ใช้ในกรณีที่แอดห้องลบบัญชี\nให้ลงคำสั่ง 1 ครั้ง\nแล้วรอ5นาทีแล้วเช็คแอดดูครับ ")       
            if settings ["Api"] == True:
                if msg.text in ["ทวิทเต้อ","ทวิท","ผูกทวิทเต้อ"]:
                    line.sendText(msg.to,"Siri:Twitter紐付け")
                    line.sendText(msg.to,"คำสั่งเฉพาะคนขายตั๋ว \nใช้ผูททวิทเต้อเพื่อซื้อตั๋ว")    
            if settings ["Api"] == True:
                if msg.text in ["ย้ายตั๋ว","ส่งตั๋ว","ขายตั๋ว"]:
                    line.sendText(msg.to,"Siri:招待券移行:1")
                    line.sendText(msg.to,"ใช้สำหรับส่งตั๋วเชิญบอทให้คนที่ซื้อ\nลงคำสั่ง1ครั้ง แล้วลง คท. ลูกค้าที่ซื้อตั๋ว 2 ครั้งครับ\n(สั่งในบอทสิริเซ็นเตอร์)")      
            if settings ["Api"] == True:
                if msg.text in ["กลับ","บอทกลับ","มา"]:
                    line.sendText(msg.to,"Siriv10:reinvite")
                    line.sendText(msg.to,"คำสั่งเรียกบอทกลับห้อง") 
            if settings ["Api"] == True:
                if msg.text in ["ชุดล็อค","ชุดล็อคen","ชุดล๊อคen"]:
                    line.sendText(msg.to,"Set:iconlock:on")
                    line.sendText(msg.to,"Set:blockinvite:on")
                    line.sendText(msg.to,"Set:ownerlock:on")
                    line.sendText(msg.to,"Set:changenamelock:on")
                    line.sendText(msg.to,"Siriv10:DenyURLInvite")
                    line.sendText(msg.to,"Set:StampLimitation:On")
                    line.sendText(msg.to,"ชุดล๊อคห้องสิริวี10 ให้คัดลอกคำสั่ง\nแล้วางลงห้องทีละคำครับ")            
            if settings ["Api"] == True:
                if msg.text in ["ดำ","สั่งดำ","เพิ่มดำ"]:
                    line.sendText(msg.to,"Set:addblacklist")
                    line.sendText(msg.to,"เพิ่มบัญชีดำ(วิธีสั่ง>ลงคำสั่ง+ส่งข้อมูล)")    
            if settings ["Api"] == True:
                if msg.text in ["ขาว","แก้ดำ","เพิ่มขาว"]:
                    line.sendText(msg.to,"Set:addwhitelist")
                    line.sendText(msg.to,"เพิ่มบัญชีขาว(วิธีสั่ง>ลงคำสั่ง+ส่งข้อมูล)")          
            if settings ["Api"] == True:
                if msg.text in ["ลบค้างเขิญ","ลบเชิญ","ยกิเชิญ"]:
                    line.sendText(msg.to,"Siriv10:cancelinvite")
                    line.sendText(msg.to,"ลบค้างเชิญ (สั่ง2ครั้ง)")    
            if settings ["Api"] == True:
                if msg.text in ["เปลี่ยนแอด","เปลี่ยนหัว","ตั้งแอด"]:
                    line.sendText(msg.to,"Set:changeowner")
                    line.sendText(msg.to,"เปลี่ยนหัวห้อง(วิธีสั่ง>ลงคำสั่ง+ส่งข้อมูล)")   
            if settings ["Api"] == True:
                if msg.text in ["ปิดลิ้ง","ปิดลิ้งค์"]:
                    line.sendText(msg.to,"Siriv10:DenyURLInvite")
                    line.sendText(msg.to,"คำสั่งปิดลิ้งห้อง")          
            if settings ["Api"] == True:
                if msg.text in ["ตั้งเวลา","ตั้งอ่าน","รีเซ็ท"]:
                    line.sendText(msg.to,"SetLastPoint")
                    line.sendText(msg.to,"กำลังตั่งค่าการอ่าน บอทสิริ.")   
            if settings ["Api"] == True:
                if msg.text in ["ใครอ่าน","อ่าน","คนแอบ"]:
                    line.sendText(msg.to,"Viewlastseen")
                    line.sendText(msg.to,"ดูคนที่กำลังอ่านตอนนี้")
            if settings ["Api"] == True:
                if msg.text in ["ล็อคแอด","ล๊อคแอด","ล๊อคแอดมิน"]:
                    line.sendText(msg.to,"設定:作成者ロック:オン")
                    line.sendText(msg.to,"คำสั่งใช้ล๊อคแอดมิน\nกันโดนเตะออกจากห้อง")
            if settings ["Api"] == True:
                if msg.text in ["ปิดการเชิญ","ปิดเชิญ"]:
                    line.sendText(msg.to,"設定:招待拒否:オン")
                    line.sendText(msg.to,"คำสั่งปฏิเสธการเชิญสมาชิกคนนอก")
            if settings ["Api"] == True:
                if msg.text in ["รันติก","ล๊อคติก","ล็อคติก"]:
                    line.sendText(msg.to,"Set:StampLimitation:On")
                    line.sendText(msg.to,"คำสั่งห้ามคนรันติกเก้อร์เกิน15ตัว")
            if settings ["Api"] == True:
                if msg.text in ["เปิดเชิญ","อนุญาติเชิญ"]:
                    line.sendText(msg.to,"設定:招待拒否:オフ")
                    line.sendText(msg.to,"อนุญาติการเชิญสมาชิกเข้าร่วมกลุ่ม")
            if settings ["Api"] == True:
                if msg.text in ["เปิดพูด","เปิดบอท","เปิดตอบ"]:
                    line.sendText(msg.to,"Siriv10:オン")
                    line.sendText(msg.to,"เปิดใช้งานบอทอ่าน")
            if settings ["Api"] == True:
                if msg.text in ["ปิดพูด","ปิดตอบ","ปิดบอท"]:
                    line.sendText(msg.to,"Siriv10:オフ")
                    line.sendText(msg.to,"คำสั่งปิดใช้งานบอทอ่านสิริ")
            if settings ["Api"] == True:
                if msg.text in ["คัดลอก",".Copy","copy"]:
                    line.sendText(msg.to,"Set:copyownlist")   
                    line.sendText(msg.to,"คำสั่งคัดลอกบัญชีห้อง")
            if settings ["Api"] == True:
                if msg.text in ["เซ็ตบัญชี","ลบรีส","ตั้งค่าบัญชี"]:
                    line.sendText(msg.to,"Set:deletelist")
                    line.sendText(msg.to,"คำสั่งตั้งค่าใหม่สำหรับ\nการคัดลอกครั้งใหม่")
            if settings ["Api"] == True:
                if msg.text in ["ปิดลิ้ง"]:
                    line.sendText(msg.to,"Siriv10:DenyURLInvite")
                    line.sendText(msg.to,"สั่งปิดลิ้งห้อง")
            if settings ["Api"] == True:
                if msg.text in ["เปิดลิ้งค์","เปิดลิ้ง"]:
                    line.sendText(msg.to,"Siriv10:inviteurl")
                    line.sendText(msg.to,"คำสั่งเปิดลิ้งห้อง")
            if settings ["Api"] == True:
                if msg.text in ["ล็อครูป","ล๊อครูป","ลอครูป"]:
                    line.sendText(msg.to,"Set:iconlock:on")
                    line.sendText(msg.to,"คำสั่งล็อครูปห้อง")
            if settings ["Api"] == True:
                if msg.text in ["ลอคชื่อ","ล็อคชื่อ","ล๊อคชื่อ"]:
                    line.sendText(msg.to,"Set:changenamelock:on")
                    line.sendText(msg.to,"คำสั่งล็อคชื่อห้อง")
            if settings ["Api"] == True:
                if msg.text in ["ล๊อคแอด","ลอคแอด","ล็อคแอด"]:
                    line.sendText(msg.to,"Set:ownerlock:on")
                    line.sendText(msg.to,"คำสั่งใช้ล๊อคแอดมินห้อง")
            if settings ["Api"] == True:
                if msg.text in ["ล๊อคเชิญ","ลอคเชิญ","ล็อคเชิญ"]:
                    line.sendText(msg.to,"Set:blockinvite:on")
                    line.sendText(msg.to,"คำสั่งล็อคการเชิญสมาชิก")
            if settings ["Api"] == True:
                if msg.text in ["ชุดล๊อคjp","ชุดล็อค2","ชุดล็อคjp"]:
                    line.sendText(msg.to,"設定:スタンプ規制:オン")
                    line.sendText(msg.to,"Siriv10:招待URL拒否")
                    line.sendText(msg.to,"設定:招待拒否:オン")
                    line.sendText(msg.to,"設定:アイコンロック:オン")
                    line.sendText(msg.to,"設定:グループ名ロック:オン")
                    line.sendText(msg.to,"設定:作成者ロック:オン")
                    line.sendText(msg.to,"ชุดคำสั่งล๊อคห้องภาษาญี่ปุ่น")
            if msg.contentType == 16:
                if settings["checkPost"] == True:
                        try:
                            ret_ = "[ ข้อมูลของโพสนี้ ]"
                            if msg.contentMetadata["serviceType"] == "GB":
                                contact = line.getContact(msg._from)
                                auth = "\n  ผู้เขียนโพส : {}".format(str(contact.displayName))
                            else:
                                auth = "\n  ผู้เขียนโพส : {}".format(str(msg.contentMetadata["serviceName"]))
                            purl = "\n  ลิ้งโพส : {}".format(str(msg.contentMetadata["postEndUrl"]).replace("line://","https://line.me/R/"))
                            ret_ += auth
                            ret_ += purl
                            if "mediaOid" in msg.contentMetadata:
                                object_ = msg.contentMetadata["mediaOid"].replace("svc=myhome|sid=h|","")
                                if msg.contentMetadata["mediaType"] == "V":
                                    if msg.contentMetadata["serviceType"] == "GB":
                                        ourl = "\n  Objek URL : https://obs-us.line-apps.com/myhome/h/download.nhn?tid=612w&{}".format(str(msg.contentMetadata["mediaOid"]))
                                        murl = "\n  Media URL : https://obs-us.line-apps.com/myhome/h/download.nhn?{}".format(str(msg.contentMetadata["mediaOid"]))
                                    else:
                                        ourl = "\n  Objek URL : https://obs-us.line-apps.com/myhome/h/download.nhn?tid=612w&{}".format(str(object_))
                                        murl = "\n  Media URL : https://obs-us.line-apps.com/myhome/h/download.nhn?{}".format(str(object_))
                                        ret_ += murl
                                else:
                                    if msg.contentMetadata["serviceType"] == "GB":
                                        ourl = "\n Objek URL : https://obs-us.line-apps.com/myhome/h/download.nhn?tid=612w&{}".format(str(msg.contentMetadata["mediaOid"]))
                                    else:
                                        ourl = "\n Objek URL : https://obs-us.line-apps.com/myhome/h/download.nhn?tid=612w&{}".format(str(object_))
                                ret_ += ourl
                            if "stickerId" in msg.contentMetadata:
                                stck = "\n  Stiker : https://line.me/R/shop/detail/{}".format(str(msg.contentMetadata["packageId"]))
                                ret_ += stck
                            if "text" in msg.contentMetadata:
                                text = "\n ข้อความโดยย่อ : {}".format(str(msg.contentMetadata["text"]))
                                ret_ += text
                            ret_ += "\n[ สิ้นสุดการเช็คโพส ]"
                            line.sendMessage(to, str(ret_), contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
                        except:
                            line.sendMessage(to, "เกิดข้อผิดะลาดในการเช็คโพสนี้", contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
        if op.type == 17:
           print ("ข้อความ สมาชิกเข้าร่วมกลุ่ม")
           if settings["Wc"] == True:
             if op.param2 in lineMID:
                 return
             #icon = "http://dl.profile.line.naver.jp/"+lineProfile.pictureStatus
             #name = "ข้อความต้อนรับ"                   
             #link = "http://line.me/ti/p/~tome2527"
             dan = line.getContact(op.param2)
             tgb = line.getGroup(op.param1)
             sendMessageWithMention(op.param1, op.param2)
             line.sendMessage(op.param1, str(settings["welcome"] +"\nสวัสดีจ้าคนมาใหม่\n╔┓┏╦━━╦┓╔┓╔━━╗╔╗\n║┗┛║┗━╣┃║┃║╯╰║║║\n║┏┓║┏━╣┗╣┗╣╰╯║╠╣\n╚┛┗╩━━╩━╩━╩━━╝╚╝\n 􀬁􀅳sparkle􏿿• 􂘁􀄗w􏿿􂘁􀄅e􏿿􂘁􀄌l􏿿􂘁􀄃c􏿿􂘁􀄏o􏿿􂘁􀄍m􏿿􂘁􀄅e􏿿 •􀬁􀅳sparkle􏿿\n🙏 {} 🙏\n❂➣ᵀᴼ ᴳᴿᴼᵁᴾ👉{}👈\n 􀼂􀅝church􏿿􀼂􀅜arbor􏿿﹏􀼂􀅞limo 1􏿿􀼂􀅟limo 2􏿿􀼂􀅠limo 3􏿿﹏􀼂􀅜arbor􏿿􀼂􀅝church􏿿\n\n🚸เข้ามาแล้วก็ทำตัวให้น่ารักๆน๊ะ\n🔇อย่าลืมปิดแจ้งตื่นกันด้วยนะจ๊ะ\n🎙มีข้อสงสัยติดต่อถามได้ที่แอดมินนนะจ๊ะ".format(str(dan.displayName),str(tgb.name))), contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})
             #line.sendMessage(op.param1,"สวัสดี🙏 {} 🙏 ยินดีต้อนรับสู่กลุ่ม {}\nนะ (｀・ω・´)".format(str(dan.displayName),str(tgb.name)) + str(settings["welcome"]))
             line.sendContact(op.param1, op.param2)
             #line.sendMessage(op.param1,"สเตตัส\n{}".format(str(dan.statusMessage)))
             line.sendImageWithURL(op.param1, "http://dl.profile.line-cdn.net{}".format(dan.picturePath))
        if op.type == 19:
           print ("ข้อความ เมื่อสมาชิกโดนเตะ")
           if settings["Nk"] == True:
             if op.param2 in lineMID:
                 return             
             dan = line.getContact(op.param2)
             tgb = line.getGroup(op.param1)
             sendMessageWithMention(op.param1, op.param2)
             line.sendMessage(op.param1, str(settings["kick"] +"\n▄︻̷̿ {} ┻̿═━一 ได้ทำการลบสมาชิกในกลุ่ม Σ(っﾟДﾟ；)っ ".format(str(dan.displayName))))
             line.sendContact(op.param1, op.param2)
             #line.sendMessage(op.param1,"สเตตัส\n{}".format(str(dan.statusMessage)))
             line.sendImageWithURL(op.param1, "http://dl.profile.line-cdn.net{}".format(dan.picturePath))
        if op.type == 15:
           print ("ข้อความสมาชิกออกห้อง")
           if settings["Lv"] == True:
             if op.param2 in lineMID:
                 return
             #icon = "http://dl.profile.line.naver.jp/"+lineProfile.pictureStatus
             #name = "ข้อความคนออก"                   
             #link = "http://line.me/ti/p/~tome2527"
             dan = line.getContact(op.param2)
             tgb = line.getGroup(op.param1)
             sendMessageWithMention(op.param1, op.param2)
             line.sendMessage(op.param1, str(settings["bye"] +"\n🌠สมาชิกชื่อว่า🌠\n👉  {}  👈\nได้ออกจากกลุ่ม\n👉 {} 👈\n✨🇬 🇴 🇴 🇩 🇧 🇾 🇪✨\nไปแล้ว  (｀・ω・´)👀ก็ขอให้โชคดีน๊ะจ๊ะ\n      􀼂􀅝church􏿿􀼂􀅜arbor􏿿﹏􀼂􀅞limo 1􏿿􀼂􀅟limo 2􏿿􀼂􀅠limo 3􏿿﹏􀼂􀅜arbor􏿿􀼂􀅝church􏿿".format(str(dan.displayName),str(tgb.name))), contentMetadata = {'AGENT_ICON': 'http://dl.profile.line-cdn.net/'+line.getContact(lineMID).pictureStatus, 'AGENT_NAME': 'Creator', 'AGENT_LINK': 'https://line.me/ti/p/Rvv5zHBLDO'})#,link ,icon,name)))
             line.sendContact(op.param1, op.param2)
             line.sendImageWithURL(op.param1, "http://dl.profile.line-cdn.net{}".format(dan.picturePath)) 
        if op.type == 55:
            try:
                if RfuCctv['cyduk'][op.param1]==True:
                    if op.param1 in RfuCctv['point']:
                        Name = line.getContact(op.param2).displayName
                        if Name in RfuCctv['sidermem'][op.param1]:
                            pass
                        else:
                            RfuCctv['sidermem'][op.param1] += "\n🔰" + Name
                            pref=['จ๊ะเอ๋','รู้นะว่าแอบอยู่','เล่นซ่อนแอบกันเหรอ','คิดว่าเป็นนินจารึไง','ว่าไง','อ่านอย่างเดียวเลยนะ','ออกมาคุยหน่อย','ออกมาเดี๋ยวนี้']
                            sendMessageWithMention(op.param1, op.param2)
                            line.sendMessage(op.param1, str(random.choice(pref)) + '\n♪ ♬ ヾ(´︶`♡)ﾉ ♬ ♪')
                            line.sendContact(op.param1, op.param2)
                            msgSticker = settings["messageSticker"]["listSticker"]["readerSticker"]
                            if msgSticker != None:
                                sid = msgSticker["STKID"]
                                spkg = msgSticker["STKPKGID"]
                                sver = msgSticker["STKVER"]
                                sendSticker(op.param1, sver, spkg, sid)
                    else:
                        pass
                else:
                    pass
            except:
                pass

        if op.type == 55:
            try:
                if RfuCctv['cyduk'][op.param1]==True:
                    if op.param1 in RfuCctv['point']:
                        Name = line.getContact(op.param2).displayName
                        if Name in RfuCctv['sidermem'][op.param1]:
                            pass
                        else:
                            RfuCctv['sidermem'][op.param1] += "\n⌬ " + Name + "\n╚════════════════┛"
                            if " " in Name:
                            	nick = Name.split(' ')
                            if len(nick) == 2:
                            	line.sendMessage(op.param1, "Nah " +nick[0])
                            summon(op.param1, [op.param2])
                    else:
                        pass
                else:
                    pass
            except:
                pass
        if op.type == 55:
            print ("✯ᴛᴏᴍᴇʙᴏᴛʟɪɴᴇ✯")
            try:
                if op.param1 in read['readPoint']:
                    if op.param2 in read['readMember'][op.param1]:
                        pass
                    else:
                        read['readMember'][op.param1] += op.param2
                    read['ROM'][op.param1][op.param2] = op.param2
                    backupData()
                else:
                   pass
            except:
                pass
    except Exception as error:
        logError(error)
#==============================================================================#
def a2():
    now2 = datetime.now()
    nowT = datetime.strftime(now2,"%M")
    if nowT[14:] in ["10","20","30","40","50","00"]:
        return False
    else:
        return True        

while True:
    try:
        ops = oepoll.singleTrace(count=5)
        if ops is not None:
            for op in ops:
                lineBot(op)
                oepoll.setRevision(op.revision)
    except Exception as e:
        logError(e)

def atend():
    print("Saving")
    with open("Log_data.json","w",encoding='utf8') as f:
        json.dump(msg_dict, f, ensure_ascii=False, indent=4,separators=(',', ': '))
    print("BYE")
atexit.register(atend)
