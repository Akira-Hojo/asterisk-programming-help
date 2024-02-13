; This is assuming you are using the default context of [to-outbound]
; In this example we have a simple office where we have to dial 9 before dialing an outside number.
; If you are handling 911 and using E911 make sure your calling details match when they go out!


[to-outbound]

; Handle 911 on TRUNK1 Trunk
exten => 911,1,NoOp(Outgoing EMERGENCY call on TRUNKNAME1 Trunk)
same => n,Set(CALLERID(num)=123456789) ; Outbound CID Number for 911 !!IMPORTANT!!
same => n,Set(CALLERID(name)=CALLEDIDNAME) ; Outbound CNAM Name For 911 !!IMPORTANT!!
same => n,Dial(PJSIP/911@SOME-ENDPOINT) ; Make the call, this could be to anywhere.

; Handle 711 TTY Relay on TRUNK1 Trunk
exten => 711,1,NoOp(Outgoing TTY RELAY call on Office Trunk)
same => n,Set(CALLERID(num)=123456789) ; Outbound CID Number
same => n,Set(CALLERID(name)=CALLEDIDNAMETTY) ; Outbound CNAM
same => n,Dial(PJSIP/123456789@SOME-ENDPOINT) ; Make the call. This might actually be 711, or it might be the national relay 1800 number.

; Trunk 1 - Dial 9 before. 7, 10, 11 digits
exten => _9NXXXXXX,1,NoOp (Outgoing call on TRUNK1 Trunk with 7 digits)
same => n,Set(CALLERID(num)=123456789) ; Outbound CID Number
same => n,Set(CALLERID(name)=CALLERIDNAME) ; Outbound CNAM
same => n,Dial(PJSIP/1555${EXTEN:1}@SOME-ENDPOINT) ; Strip off the 9 and prepend a US area code and a leading 1

exten => _9NXXNXXXXXX,1,NoOp(Outgoing call on OFFICE Trunk with 10 digits)
same => n,Set(CALLERID(num)=123456789) ; Outbound CID Number
same => n,Set(CALLERID(name)=CALLERIDNAME) ; Outbound CNAM
same => n,Dial(PJSIP/${EXTEN:1}@SOME-ENDPOINT) ; Strip off the 9

exten => _91NXXNXXXXXX,1,NoOp(Outgoing call on OFFICE Trunk with 11 digits)
same => n,Set(CALLERID(num)=8456004656) ; Outbound CID Number
same => n,Set(CALLERID(name)=HOJOWORKS) ; Outbound CNAM
same => n,Dial(PJSIP/${EXTEN:1}@SOME-ENDPOINT) ; Strip off the 9