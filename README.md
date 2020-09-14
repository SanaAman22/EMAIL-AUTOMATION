# EMAIL-AUTOMATION
import smtplib
from email.mime.multipart import MIMEMultipart
from email.mime.text import MIMEText
from email.mime.base import MIMEBase
from email import encoders

"""initialising from addr and to addr"""
from_addr=' Alevender242 @gmail.com '
to_addr=[' saniya543@gmail.com ']

"""creating duplicate containers and adding from and to adress"""
msg=MIMEMultipart()
msg['From']=from_addr
msg['To']=" ,".join(to_addr)
msg['subject']='just to check'

body='hello world'
msg.attach(MIMEText(body,'plain'))
#attaching file by using MIMEBase
filename = 'code.pdf'
attachment = open(filename,'rb')

part = MIMEBase('application','octet-stream')
part.set_payload((attachment).read())
encoders.encode_base64(part)
part.add_header('Content-Disposition',"attachment;filename= "+filename)
"""login credentials"""
email=' Alevender242@gmail.com '
password=' 12354 '

"""connecting to server via local host and ip adress"""
msg.attach(part)
mail=smtplib.SMTP('smtp.gmail.com',587)
mail.ehlo()
mail.starttls()
mail.login(email,password)
text=msg.as_string()
mail.sendmail(from_addr,to_addr,text)
mail.quit()
