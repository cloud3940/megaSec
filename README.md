# megaSec
megaSec API

安裝報價套件<br/>
pip install megaSec

#載入報價套件<br/>
from megaAPI.quote import UFIIS
import time


#初始化報價物件<br/>
q = UFIIS()

#登入驗證<br/>
#q.setInitialize("報價身份驗證SERVER IP",報價身份驗證SERVER PORT,"身份證字號","電子下單登入密碼")
print(q.setInitialize("1.0.0.0",1111,"P123456789","1234"))

#報價接收主機連線<br/>
#q.setConnect("報價接收主機連線SERVER IP",報價接收主機連線SERVER PORT)<br/>
print(q.setConnect("1.0.0.1",2222))

"""
證券0x01
期貨0x11
期貨盤後0x13
選擇權0x22
選擇權盤後0x24
外期0x12
"""
<br/>
#回補<br/>
q.setRequest("0x01","2886")

#接收回補資料<br/>
q.setRecv()

#取成交價tag 125<br/>
print(q.bufferDict.get('125'))

#Iterate over a dictionary<br/>
for tag,tagVal in q.bufferDict.items(): 
    print("{}={}".format(tag,tagVal)) 


#訂閱即時<br/>
q.setSubscribe("0x01","2886")

#取得即時行情<br/>
for i in range(1,20):
    
 #選擇性增加延遲<br/>   
 time.sleep(1)
 
 #收即時資料<br/>
 q.setRecv()
 
 #顯示收到資料<br/>
 if(q.bufferDict != None):
     print(q.bufferDict)

 
#釋放連線<br/>
q.setDisconnect()

#釋放資源<br/>
q.setDeinitialize()
