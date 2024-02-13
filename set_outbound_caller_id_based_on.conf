; Set an external caller ID based on an internal caller ID condition. 
; For example, maybe you want the internal extension LIVING ROOM 
; to have a certain ;caller ID when making a certain call. Or in 
; this case, we are handling a TTY and a FAX and setting the 
; caller ID based on that.

exten => 1234,1,NoOp(Called Extension That Changes Caller ID!)
same => n,NoOp(Original CallerID Name: ${CALLERID(name)})
same => n,NoOp(Original CallerID Number: ${CALLERID(num)})

; Check if Caller ID name contains FAX
same => n,GotoIf($[${REGEX("FAX" ${CALLERID(name)})}]?set_fax:set_phone)

; Check if Caller ID name contains TTY
same => n,GotoIf($[${REGEX("TTY" ${CALLERID(name)})}]?set_tty:set_phone)

; Set Caller ID for FAX
same => n(set_fax),NoOp(Setting FAX CallerID)
same => n,Set(CALLERID(num)=123456789) ; Replace with FAX CID Number
same => n,Set(CALLERID(name)=THE FAX) ; Replace with FAX CID Name
same => n,NoOp(New CallerID Name: ${CALLERID(name)}) ; Some helpful output
same => n,NoOp(New CallerID Number: ${CALLERID(num)})
same => n,Goto(dial_number) ; Jump to dial_number

; Set Caller ID for TTY
same => n(set_tty),NoOp(Setting TTY CallerID)
same => n,Set(CALLERID(num)=123456789) ; Replace with TTY CID Number
same => n,Set(CALLERID(name)=THE TTY) ; Replace with TTY CID Name
same => n,NoOp(New CallerID Name: ${CALLERID(name)}) ; Some helpful output
same => n,NoOp(New CallerID Number: ${CALLERID(num)})
same => n,Goto(dial_number) ; Jump to dial_number

; Set Caller ID for no matches, default Phone
same => n(set_phone),NoOp(Setting Phone Caller ID)
same => n,Set(CALLERID(num)=123456789) ; Replace with non-TTY CID Number
same => n,Set(CALLERID(name)=THE PHONE) ; Replace with non-TTY CID Name
same => n,NoOp(New CallerID Name: ${CALLERID(name)})
same => n,NoOp(New CallerID Number: ${CALLERID(num)})
; No need to jump here, since we fall through into the place we need to be.

; Dial the number dialtone extension
same => n(dial_number),NoOp(Dialing After Changing Caller ID)
same => n,Dial(PJSIP/1234@SOME_ENDPOINT)